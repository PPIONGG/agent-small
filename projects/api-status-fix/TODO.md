# TODO - api-status-fix

## Objective
แก้ไข API error status codes ให้ถูกต้องตามมาตรฐาน HTTP ทั้ง Frontend (QReact) และ Backend (QERPC-API)

> ⚠️ Frontend path: `c:\Users\Kongsit\Desktop\QReact` (ไม่ใช่ c:\GitHub\QReact)

---

## Done

- [x] Scout: scan Portal (Desktop) — APIs + error handling pattern
- [x] Scout: scan Backend 2 endpoints (LoginJWT, QERPcMenuJWT)
- [x] สรุป Gap Report: Portal (reports/portal-gap-report.md)
- [x] Developer: แก้ไข Portal Frontend error handling (4 ไฟล์)
  - `shared/src/services/httpClient.ts` — เพิ่ม onUnauthorized callback + interceptor ดัก 401
  - `portal/src/utils/apiErrorUtils.ts` — **ไฟล์ใหม่** extractApiError() แยก 400/401/403/500/network
  - `portal/src/services/authHelpers.ts` — ใช้ extractApiError แทน generic CONNECTION_ERROR
  - `portal/src/contexts/AuthContext.tsx` — updateCompany แยก error + wire onUnauthorized auto-logout
- [x] ตรวจสอบ Backend: พบ GlobalExceptionMiddleware ดัก exception อยู่แล้ว → ไม่ต้องเพิ่ม try/catch
- [x] Hotfix: 500+ ใช้ apiMsg จาก backend แทน hardcode API_ERROR
- [x] เพิ่ม `message.error()` ใน Main.tsx ตอนเปลี่ยนบริษัทแล้ว error
- [x] ย้าย `extractApiError()` + `API_ERROR_MESSAGES` ไป `@qerp/shared/errors` เพื่อให้ทุก module ใช้ได้
  - สร้าง `shared/src/errors/` (errorConstants.ts, apiErrorUtils.ts, index.ts)
  - เพิ่ม export ใน `shared/src/index.ts` + `shared/package.json`
  - อัปเดต import ใน Portal (authHelpers.ts, AuthContext.tsx, test)
  - ลบ `portal/src/utils/apiErrorUtils.ts` (ย้ายไป shared แล้ว)

---

- [x] Scout: scan Sales Analytics module (4 APIs, 2 ไฟล์ที่ต้องแก้)
- [x] Developer: แก้ไข Sales Analytics error handling (2 ไฟล์)
  - `Q-ERPc/analytics/sales-analytics/src/hooks/useDashboard.ts` — 4 catch blocks: เพิ่ม extractApiError + message.error
  - `Q-ERPc/analytics/sales-analytics/src/contexts/PermissionContext.tsx` — เพิ่ม extractApiError + message.error

---

- [x] Scout: scan Purchase Order module (22+ catch blocks, 10 ไฟล์ที่ต้องแก้)
- [x] Developer: แก้ไข Purchase Order error handling (10 ไฟล์)
  - `hooks/useApprovedConfig.ts` — silent catch → extractApiError + message.error
  - `hooks/useMasterData.ts` — silent catch → extractApiError + message.error
  - `hooks/useSerieInfo.ts` — silent catch → extractApiError + message.error
  - `hooks/usePOFormData.ts` — silent catch → extractApiError + message.error
  - `hooks/usePOListData.ts` — 2 silent catches (fetchDocTypes, fetchPOHeaders) → extractApiError + message.error
  - `hooks/usePOEditData.ts` — main catch → extractApiError + message.error
  - `hooks/useCheckStatusModal.ts` — hardcoded error msg → extractApiError
  - `hooks/useDocumentTypes.ts` — generic error → extractApiError
  - `hooks/usePOFormSubmit.ts` — manual AxiosError extraction → simplified with extractApiError
  - `contexts/PermissionContext.tsx` — เพิ่ม extractApiError + message.error

  **ไม่แก้ (already handled):**
  - `hooks/usePOListData.ts` cancelPO, handleApprovalAction — ใช้ ErrorModal อยู่แล้ว
  - `hooks/useVATCalculation.ts` — complex rollback logic, already shows message.error
  - `hooks/useDeleteLineValidation.ts` — already shows message.error
  - `hooks/useLineItemHandlers.ts`, `hooks/useSupplierHandlers.ts` — nested non-critical catches

---

- [x] Scout: scan Sales Order module (23 catch blocks, 7 ไฟล์ที่ต้องแก้)
- [x] Developer: แก้ไข Sales Order error handling (7 ไฟล์)
  - `hooks/useApprovedConfig.ts` — silent catch → extractApiError + message.error
  - `hooks/useSOFormData.ts` — silent catch → extractApiError + message.error
  - `hooks/useCheckStatusModal.ts` — hardcoded error msg → extractApiError
  - `hooks/useDocumentTypes.ts` — generic error (instanceof Error) → extractApiError
  - `hooks/useSOEditData.ts` — main catch: hardcoded msg → extractApiError; 2 nested catches: extractApiError + message.warning; 1 loop catch: extractApiError logging
  - `hooks/useCustomerHandlers.ts` — 2 silent catches → extractApiError + message.warning; 1 hardcoded catch → extractApiError + message.error
  - `contexts/PermissionContext.tsx` — เพิ่ม extractApiError + message.error

  **ไม่แก้ (already handled):**
  - `hooks/useSOListData.ts` cancelSO, handleApprovalAction — ใช้ ErrorModal อยู่แล้ว
  - `hooks/useSOFormSubmit.ts` — already uses extractApiError / ErrorModal

---

## In Progress

(ยังไม่มี)

---

## Backlog

- [ ] Scout: scan module Sales Visitor
