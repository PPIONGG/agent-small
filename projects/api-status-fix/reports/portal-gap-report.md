# Gap Report: Portal Module — Frontend vs Backend

> Scanned: 2026-02-05
> Frontend: `c:\Users\Kongsit\Desktop\QReact` (Desktop version)

---

## Architecture Overview

```
Shared HttpClient (shared/src/services/httpClient.ts)
  ↓ interceptor: แค่ log error, ไม่ handle
Portal httpClient instance (portal/src/services/httpClient.ts)
  ↓ createHttpClient() จาก @qerp/shared/services
authService (portal/src/services/authService.ts)
  ↓ เรียก API, ไม่มี try/catch, throw ต่อ
authHelpers (portal/src/services/authHelpers.ts)
  ↓ try/catch แต่จับ error เป็น generic ทั้งหมด
AuthContext (portal/src/contexts/AuthContext.tsx)
  ↓ อีก try/catch, จับ error เป็น CONNECTION_ERROR
UI → เห็นแค่ "เกิดข้อผิดพลาดในการเชื่อมต่อ"
```

---

## Portal APIs

| # | Method | Endpoint | Callers |
|---|--------|----------|---------|
| 1 | POST | `/api/Login/LoginJWT` | `authService.login()` → `authHelpers.handleLogin()` → `AuthContext.login()` |
| 2 | POST | `/api/JWT/QERPcMenuJWT` | `authService.getMenuJWT()` → `authHelpers`, `AuthContext.updateCompany()`, `permissionUtils` |

---

## API 1: POST /api/Login/LoginJWT

### Backend ส่งอะไรได้

| HTTP Status | เงื่อนไข | Body |
|-------------|---------|------|
| 200 OK | Login สำเร็จ | `{ code: 0, result: { accessToken, permission } }` |
| 200 OK | code != 0 (ถ้ามี) | `{ code: X, msg: "..." }` |
| 400 BadRequest | User ไม่พบ / ข้อมูลผิด | `{ code: 404, msg: "ไม่พบผู้ใช้งาน" }` |
| 500 (unhandled) | Exception (ไม่มี try/catch ใน controller) | ASP.NET generic error |

### Frontend Error Flow

```
authService.login() → ไม่มี try/catch
  ↓
กรณี 200 + code != 0:
  → authHelpers: return { success: false, message: response.msg } ✅ ทำงานถูกต้อง

กรณี HTTP 400 (axios throws):
  → authService throws AxiosError
  → authHelpers outer catch → ERROR_MESSAGES.CONNECTION_ERROR ❌
  → User เห็น "เกิดข้อผิดพลาดในการเชื่อมต่อ" แทน "ไม่พบผู้ใช้งาน"

กรณี HTTP 500 (axios throws):
  → authHelpers outer catch → ERROR_MESSAGES.CONNECTION_ERROR ❌
  → ไม่แยก server error vs network error

กรณี Network error:
  → authHelpers outer catch → ERROR_MESSAGES.CONNECTION_ERROR ✅ พอใช้ได้
```

### Gap

| ปัญหา | ระดับ | ฝั่ง |
|--------|-------|------|
| Backend ส่ง HTTP 400 + body `code: 404` → ควรส่ง 200 + code หรือ HTTP 404 ตรงๆ | สูง | Backend |
| Frontend: HTTP 400 "ไม่พบผู้ใช้งาน" ถูกแสดงเป็น "เกิดข้อผิดพลาดในการเชื่อมต่อ" | สูง | Frontend |
| Backend: LoginController ไม่มี try/catch | สูง | Backend |
| Frontend: ไม่แยก 400 (ข้อมูลผิด) vs 500 (server) vs network error | กลาง | Frontend |

---

## API 2: POST /api/JWT/QERPcMenuJWT

### Backend ส่งอะไรได้

| HTTP Status | เงื่อนไข | Body |
|-------------|---------|------|
| 200 OK | สำเร็จ | `{ code: 0, result: { accessToken, permission } }` |
| 400 BadRequest | errCode > 0 | `{ code: errCode, msg: errMsg }` |
| 401 Unauthorized | [Authorize] middleware - token invalid/expired | ASP.NET 401 |
| 403 Forbidden | PolicyMode.Menu - ไม่มีสิทธิ์ | ASP.NET 403 |
| 500 (unhandled) | Exception (ไม่มี try/catch ใน controller) | ASP.NET generic error |

### Frontend Error Flow

**เรียกจาก authHelpers.handleLogin() (ระหว่าง login):**
```
authService.getMenuJWT() → ไม่มี try/catch
  ↓
กรณี 200 + code != 0:
  → authHelpers: log warning, return response ✅ แต่ไม่ได้แสดง error ให้ user

กรณี HTTP 401/403/400/500 (axios throws):
  → nested catch → logger.error, continue ⚠️
  → Login ยังสำเร็จ แต่ไม่มี menu permission
```

**เรียกจาก AuthContext.updateCompany() (เปลี่ยนบริษัท):**
```
authService.getMenuJWT() → ไม่มี try/catch
  ↓
กรณี 200 + code != 0:
  → return { success: false, message: response.msg } ✅

กรณี HTTP 401 (token expired):
  → catch → ERROR_MESSAGES.CONNECTION_ERROR ❌
  → ไม่ auto-logout, ไม่บอก user ว่า session หมดอายุ

กรณี HTTP 403 (no permission):
  → catch → ERROR_MESSAGES.CONNECTION_ERROR ❌
  → ไม่บอก user ว่าไม่มีสิทธิ์
```

**เรียกจาก permissionUtils.checkRoutePermission():**
```
authService.getMenuJWT() → throws
  → catch → return { hasAccess: false, error } ⚠️
  → ไม่แยกว่า error เพราะไม่มีสิทธิ์ หรือเพราะ network ล่ม
```

### Gap

| ปัญหา | ระดับ | ฝั่ง |
|--------|-------|------|
| 401 (token expired) ถูกแสดงเป็น "เกิดข้อผิดพลาดในการเชื่อมต่อ" | สูง | Frontend |
| ไม่มี auto-logout เมื่อ token หมดอายุ | สูง | Frontend |
| 403 (no permission) ไม่ถูกแยกจาก error อื่น | กลาง | Frontend |
| Backend: JWTController ไม่มี try/catch | สูง | Backend |

---

## Shared HttpClient — ปัญหาร่วม

| ปัญหา | ผลกระทบ | สถานะ |
|--------|---------|-------|
| Interceptor แค่ `console.error` | ทุก module ต้อง handle error เอง | ✅ เพิ่ม 401 handling (AUTH_TOKEN_INVALID → event + swallow) |
| ไม่มี `onUnauthorized` callback | ไม่มี global 401 auto-logout | ✅ ใช้ `qerp:session-expired` event + SessionExpiredModal |
| ไม่มี error normalization | แต่ละที่จัดการ AxiosError ต่างกัน | ✅ ใช้ `extractApiError()` จาก `@qerp/shared/errors` |

---

## Error Messages ที่มีแต่ไม่ได้ใช้

`portal/src/constants/errors.ts` มี constants พร้อมแล้ว:

| Constant | Value | ใช้อยู่? |
|----------|-------|---------|
| `SESSION_EXPIRED` | "เซสชันหมดอายุ กรุณาเข้าสู่ระบบใหม่" | ❌ ไม่เคยใช้กับ 401 |
| `INVALID_CREDENTIALS` | "ชื่อผู้ใช้หรือรหัสผ่านไม่ถูกต้อง" | ❌ ไม่ใช้เมื่อ backend ส่ง 400 |
| `NETWORK_ERROR` | "ไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้" | ❌ ไม่แยกจาก CONNECTION_ERROR |
| `API_ERROR` | "เกิดข้อผิดพลาดในการเรียก API" | ❌ ไม่เคยใช้ |

---

## สรุปปัญหาทั้งหมด (เรียงตามความสำคัญ)

| # | ปัญหา | ระดับ | ฝั่ง | แนวทางแก้ | สถานะ |
|---|--------|-------|------|-----------|-------|
| 1 | HTTP 400 "ไม่พบผู้ใช้งาน" แสดงเป็น "เกิดข้อผิดพลาดในการเชื่อมต่อ" | สูง | Frontend | authHelpers: ดึง error.response.data.msg จาก AxiosError | ✅ |
| 2 | 401 token expired ไม่ auto-logout | สูง | Frontend | httpClient: เช็ค errorCode + SessionExpiredModal | ✅ |
| 3 | Backend ส่ง HTTP 400 + body code:404 | สูง | Backend | ส่ง HTTP status ตรง หรือ ส่ง 200 + code | ⏳ |
| 4 | LoginController ไม่มี try/catch | สูง | Backend | เพิ่ม try/catch + return 500 | ⏳ |
| 5 | JWTController ไม่มี try/catch | สูง | Backend | เพิ่ม try/catch + return 500 | ⏳ |
| 6 | 403 ไม่แยกจาก error อื่น | กลาง | Frontend | authHelpers: เช็ค status 403 | ✅ |
| 7 | ไม่ใช้ error constants ที่มีอยู่แล้ว | ต่ำ | Frontend | ใช้ SESSION_EXPIRED, INVALID_CREDENTIALS | ✅ |
| 8 | httpClient interceptor แค่ log | กลาง | Shared | เพิ่ม global error handling + AUTH_TOKEN_INVALID check | ✅ |
