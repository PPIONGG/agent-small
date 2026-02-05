# Specs - api-status-fix

## Overview
แก้ไข API error/success status codes ให้ถูกต้องตามมาตรฐาน HTTP ระหว่าง QReact (Frontend) และ QERPC-API (Backend)

## Workspace
| Side | Repo | Path |
|------|------|------|
| Frontend | QReact | `c:\Users\Kongsit\Desktop\QReact` |
| Backend | QERPC-API | `c:\GitHub\QERPC-API` |

## Frontend Architecture
- **Shared Library**: `shared/src/services/httpClient.ts` — HttpClient class ใช้ร่วมทุก module
- **Portal Auth**: `portal/src/services/authService.ts` — Login, JWT, permission
- **Module Pattern**: แต่ละ module สร้าง httpClient instance จาก `@qerp/shared/services`
- **Total Service Files**: ~39 ไฟล์ใน 5 modules

### Modules
| Module | Service Files | Path |
|--------|--------------|------|
| Portal | 2 | `portal/src/services/` |
| Purchase Order | 11 | `Q-ERPc/purchase/purchase-order/src/services/` |
| Sales Order | 13 | `Q-ERPc/sales/sales-order/src/services/` |
| Sales Visitor | 1 | `Q-ERPc/sales/sales-visitor/src/services/` |
| Sales Analytics | 3 | `Q-ERPc/analytics/sales-analytics/src/services/` |

## HTTP Status Code Standards

| Status | Meaning | ใช้เมื่อ |
|--------|---------|---------|
| 200 | OK | GET สำเร็จ, PUT/PATCH สำเร็จ |
| 201 | Created | POST สร้างข้อมูลสำเร็จ |
| 204 | No Content | DELETE สำเร็จ |
| 400 | Bad Request | Input ไม่ถูกต้อง, Validation fail |
| 401 | Unauthorized | ไม่ได้ login / token หมดอายุ |
| 403 | Forbidden | ไม่มีสิทธิ์เข้าถึง |
| 404 | Not Found | ไม่พบข้อมูล |
| 409 | Conflict | ข้อมูลซ้ำ / conflict |
| 422 | Unprocessable Entity | Business logic validation fail |
| 500 | Internal Server Error | Server error |

## Scope
ทำทีละ module — เริ่มจาก Portal → เทียบกับ Backend → แก้ไข → scan module ถัดไป
