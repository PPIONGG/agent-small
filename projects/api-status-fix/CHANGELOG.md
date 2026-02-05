# CHANGELOG - api-status-fix

## [Unreleased]

### 2026-02-05

#### Portal Frontend — Error Handling Fix

**ปัญหาเดิม:** ทุก API error (400, 401, 403, 500, network) ถูกแสดงเป็น "เกิดข้อผิดพลาดในการเชื่อมต่อ" หมด

**ไฟล์ที่แก้ไข:**

1. **`shared/src/services/httpClient.ts`** (Shared Library)
   - เพิ่ม `onUnauthorized` callback + interceptor ดัก 401
   - เพิ่ม `setOnUnauthorized()` method

2. **`shared/src/errors/`** (ย้ายจาก portal → shared เพื่อให้ทุก module ใช้ได้)
   - `errorConstants.ts` — `API_ERROR_MESSAGES` (SESSION_EXPIRED, FORBIDDEN, INVALID_CREDENTIALS, API_ERROR, CONNECTION_ERROR, UNKNOWN_ERROR)
   - `apiErrorUtils.ts` — `extractApiError()` แยก 400/401/403/500+/network + ใช้ apiMsg จาก backend
   - `index.ts` — barrel export
   - เพิ่ม export ใน `shared/src/index.ts` + `shared/package.json` (`./errors`)

3. **`portal/src/services/authHelpers.ts`**
   - `handleLogin()` catch: ใช้ `extractApiError()` จาก `@qerp/shared/errors`

4. **`portal/src/contexts/AuthContext.tsx`**
   - `updateCompany()` catch: แยก error + auto-logout ถ้า 401
   - เพิ่ม useEffect wire `httpClient.setOnUnauthorized()` → global auto-logout
   - import `extractApiError` จาก `@qerp/shared/errors`

5. **`portal/src/pages/Main.tsx`**
   - เพิ่ม `message.error(result.message)` ตอนเปลี่ยนบริษัทแล้ว error (แทน TODO comment)

#### Removed
- **`portal/src/utils/apiErrorUtils.ts`** — ลบ (ย้ายไป shared แล้ว)

#### Unit Tests
- 13 test cases ใน `portal/src/utils/__tests__/apiErrorUtils.test.ts`
- อัปเดต import ใช้ `@qerp/shared/errors`
- ครอบคลุม: 400 (มี/ไม่มี msg), 401, 403, 500+ (มี/ไม่มี msg), 503, 504, network error, string error, null error, 404, 409

#### Project Setup
- สร้าง project workspace เชื่อม QReact (Desktop) + QERPC-API
- กำหนด HTTP status code standards
- เขียน Gap Report: Portal module (reports/portal-gap-report.md)

---

#### Sales Analytics — Error Handling Fix

**ปัญหาเดิม:** ทุก API error แค่ `console.error` ผู้ใช้ไม่เห็นอะไรเลย (dashboard ว่างเปล่า)

**ไฟล์ที่แก้ไข:**

1. **`Q-ERPc/analytics/sales-analytics/src/hooks/useDashboard.ts`**
   - 4 catch blocks: เพิ่ม `extractApiError()` + `message.error()` ให้ครบทุก API
   - APIs: getCompanyGoLive, getSOSummary (×2), getSONotComplete

2. **`Q-ERPc/analytics/sales-analytics/src/contexts/PermissionContext.tsx`**
   - API error (code ≠ 0): เพิ่ม `message.error()`
   - Network/HTTP error: เพิ่ม `extractApiError()` + `message.error()`

---

#### Purchase Order — Error Handling Fix

**ปัญหาเดิม:** หลาย API catch blocks แค่ `console.error` ไม่แจ้งผู้ใช้ / บาง catch ใช้ hardcoded error message แทนที่จะใช้ msg จาก backend

**ไฟล์ที่แก้ไข (10 ไฟล์):**

1. **`Q-ERPc/purchase/purchase-order/src/hooks/useApprovedConfig.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

2. **`Q-ERPc/purchase/purchase-order/src/hooks/useMasterData.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

3. **`Q-ERPc/purchase/purchase-order/src/hooks/useSerieInfo.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

4. **`Q-ERPc/purchase/purchase-order/src/hooks/usePOFormData.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

5. **`Q-ERPc/purchase/purchase-order/src/hooks/usePOListData.ts`**
   - fetchDocTypes catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)
   - fetchPOHeaders catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

6. **`Q-ERPc/purchase/purchase-order/src/hooks/usePOEditData.ts`**
   - main catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

7. **`Q-ERPc/purchase/purchase-order/src/hooks/useCheckStatusModal.ts`**
   - catch: เปลี่ยนจาก hardcoded 'เกิดข้อผิดพลาด' → `extractApiError()` ใช้ msg จาก backend

8. **`Q-ERPc/purchase/purchase-order/src/hooks/useDocumentTypes.ts`**
   - catch: เปลี่ยนจาก `err instanceof Error ? err.message : 'Unknown error'` → `extractApiError()`

9. **`Q-ERPc/purchase/purchase-order/src/hooks/usePOFormSubmit.ts`**
   - catch: ลด manual AxiosError type checking → ใช้ `extractApiError()` แทน

10. **`Q-ERPc/purchase/purchase-order/src/contexts/PermissionContext.tsx`**
    - API error (code ≠ 0): เพิ่ม `message.error()`
    - Network/HTTP error: เพิ่ม `extractApiError()` + `message.error()`

**ไม่แก้ไข (already handled properly):**
- `usePOListData.ts` cancelPO/handleApprovalAction — ใช้ ErrorModal แสดง error อยู่แล้ว
- `useVATCalculation.ts` — complex rollback + message.error อยู่แล้ว
- `useDeleteLineValidation.ts` — message.error อยู่แล้ว
- `useLineItemHandlers.ts`/`useSupplierHandlers.ts` — nested non-critical catches

---

#### Sales Order — Error Handling Fix

**ปัญหาเดิม:** หลาย catch blocks แค่ `console.error` ไม่แจ้งผู้ใช้ / บาง catch ใช้ hardcoded error message / บาง catch ใช้ `instanceof Error` แทน extractApiError

**ไฟล์ที่แก้ไข (7 ไฟล์):**

1. **`Q-ERPc/sales/sales-order/src/hooks/useApprovedConfig.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

2. **`Q-ERPc/sales/sales-order/src/hooks/useSOFormData.ts`**
   - catch: เพิ่ม `extractApiError()` + `message.error()` (เดิมแค่ console.error)

3. **`Q-ERPc/sales/sales-order/src/hooks/useCheckStatusModal.ts`**
   - catch: เปลี่ยนจาก hardcoded 'เกิดข้อผิดพลาดในการตรวจสอบสถานะ' → `extractApiError()` ใช้ msg จาก backend

4. **`Q-ERPc/sales/sales-order/src/hooks/useDocumentTypes.ts`**
   - catch: เปลี่ยนจาก `err instanceof Error ? err.message : 'Unknown error'` → `extractApiError()`

5. **`Q-ERPc/sales/sales-order/src/hooks/useSOEditData.ts`**
   - main catch: เปลี่ยนจาก hardcoded 'ไม่สามารถโหลดข้อมูลใบสั่งขายได้' → `extractApiError()`
   - nested catch (getCustomer): เพิ่ม `extractApiError()` + `message.warning()`
   - nested catch (getSalesmanList): เพิ่ม `extractApiError()` + `message.warning()`
   - nested catch (getUnitConversionList): เพิ่ม `extractApiError()` logging (อยู่ใน loop, ไม่ toast)

6. **`Q-ERPc/sales/sales-order/src/hooks/useCustomerHandlers.ts`**
   - calculatePaymentDueDate catch: เพิ่ม `extractApiError()` + `message.warning()` (เดิมแค่ console.error)
   - handleCustomerSelect catch: เพิ่ม `extractApiError()` + `message.warning()` (เดิมแค่ console.error, มี graceful fallback)
   - handleCustomerCodeSearch catch: เปลี่ยนจาก hardcoded msg → `extractApiError()` + `message.error()`

7. **`Q-ERPc/sales/sales-order/src/contexts/PermissionContext.tsx`**
   - Network/HTTP error: เพิ่ม `extractApiError()` + `message.error()` (เดิมใช้ instanceof Error)

**ไม่แก้ไข (already handled properly):**
- `useSOListData.ts` cancelSO/handleApprovalAction — ใช้ ErrorModal แสดง error อยู่แล้ว
- `useSOFormSubmit.ts` — already uses extractApiError / ErrorModal

---

#### Session Expired Modal — 401 AUTH_TOKEN_INVALID Handling

**ปัญหาเดิม:** เมื่อ token หมดอายุ (401) → auto-logout เงียบๆ redirect ไป /login โดยไม่บอก user ว่าเกิดอะไรขึ้น + หน้า login ก็ได้รับ 401 (AUTH_LOGIN_FAILED) แต่ถูก swallow ไปด้วย

**ไฟล์ที่แก้ไข (6 ไฟล์):**

1. **`shared/src/services/httpClient.ts`**
   - interceptor: เช็ค `errorCode === 'AUTH_TOKEN_INVALID'` เท่านั้น → dispatch `qerp:session-expired` event + swallow error
   - `AUTH_LOGIN_FAILED` หรือ 401 อื่นๆ → ปล่อย error propagate ปกติ

2. **`shared/src/errors/apiErrorUtils.ts`**
   - 401: เปลี่ยนจาก hardcode `SESSION_EXPIRED` → `apiMsg || SESSION_EXPIRED` (ใช้ msg จาก backend)

3. **`portal/src/contexts/authTypes.ts`**
   - เพิ่ม `sessionExpired: boolean`, `sessionExpiredMessage: string | null` ใน AuthState
   - เพิ่ม `confirmSessionExpired: () => void` ใน AuthContextType

4. **`portal/src/contexts/AuthContext.tsx`**
   - ลบ `httpClient.setOnUnauthorized()` callback → เปลี่ยนเป็นฟัง `qerp:session-expired` event
   - เพิ่ม `useRef` กัน duplicate (หลาย API อาจ 401 พร้อมกัน)
   - เพิ่ม `confirmSessionExpired()` → logout + reset modal state
   - ลบ auto-logout ใน `updateCompany` catch (interceptor จัดการแทน)

5. **`portal/src/components/SessionExpiredModal.tsx`** (ไฟล์ใหม่)
   - Ant Design Modal: `closable=false`, `maskClosable=false`, `keyboard=false`
   - แสดง `sessionExpiredMessage` จาก backend
   - ปุ่มเดียว "เข้าสู่ระบบใหม่" → `confirmSessionExpired()` + `navigate('/login')`

6. **`portal/src/App.tsx`**
   - วาง `<SessionExpiredModal />` ใน Router (ก่อน Routes)
