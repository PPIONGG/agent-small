# Backend API Response Patterns — Full Reference

> Source: `c:\GitHub\QERPC-API\QercAPI\`

## Return Models (C#)

### Pattern 1: Standard (ทุก API ที่ frontend เรียก)

```csharp
// ReturnMessageData — single object
{ Code: int, Msg: string?, ErrorCode: string?, Result: dynamic? }

// ReturnPaginationData<T> — list + pagination
{ Code: int, Msg: string?, ErrorCode: string?, Result: List<T>?, TotalCount, Page, PageSize, TotalPages }

// ReturnMessage — write operations (no result)
{ Code: int, Msg: string?, ErrorCode: string? }
```

### Pattern 2: Legacy (10 controllers — frontend ไม่ได้เรียก)

```csharp
// ReturnAPI
{ Status: bool?, Message: string?, MessageE: string?, data: dynamic? }
```

Legacy controllers: Dashboard, CustomerCategory, FGStock, Pallet, Serie*, TeamDelivery, TransactionCategory, TransactionContactOfMaster, Vehicle, WO, **SalesVisitor**

> *Serie controller มี endpoint `SeriesAndGroupDoc` ที่ใช้ ReturnMessageData (Pattern 1) ซึ่ง frontend เรียก

## Sales Visitor APIs (Legacy Pattern — ยังไม่ได้เรียกจาก Frontend)

| # | Endpoint | Return Type | Notes |
|---|----------|-------------|-------|
| - | GET /api/SalesVisitor/Customer | ReturnAPI | Legacy |
| - | GET /api/SalesVisitor/CustomerDetails/{id}/{type} | ReturnAPI | Legacy |
| - | GET /api/SalesVisitor/ListVisited/{salescode} | ReturnAPI | Legacy |
| - | GET /api/SalesVisitor/VisitDetails/{id} | ReturnAPI | Legacy |
| - | POST /api/SalesVisitor/Create | ReturnAPI | Legacy |
| - | POST /api/SalesVisitor/Update | ReturnAPI | Legacy |
| - | POST /api/SalesVisitor/CancelOrRestore | ReturnAPI | Legacy |
| - | POST /api/SalesVisitor/ApprovePettyCash | ReturnAPI | Legacy |

> **หมายเหตุ:** Frontend Sales Visitor module ยังใช้ mock data อยู่ ยังไม่เรียก API จริง แต่ local `types/api.ts` กำหนดเป็น Pattern 1 ซึ่งจะ **ไม่ match** กับ backend เมื่อเชื่อมต่อจริง

## 36 APIs ที่ Frontend เรียก (Pattern 1)

### Shared (Portal + SA + ทุก module)

| # | Endpoint | Return Type | Notes |
|---|----------|-------------|-------|
| 1 | POST /api/Login/LoginJWT | ReturnMessageData | Portal login |
| 2 | POST /api/JWT/QERPcMenuJWT | ReturnMessageData | Portal menu JWT |
| 3 | GET /api/Company/ComapyGoLive | ReturnMessageData | SA dashboard |
| 4 | GET /api/PivotSO/SOSummary | ReturnMessageData | SA dashboard |
| 5 | GET /api/PivotSO/SONotComplete | ReturnPaginationData | SA dashboard |
| 6 | GET /api/JWT/QERPcMenuActionJWT/{module} | ReturnMessageData | Permission (ทุก module) |
| 7 | GET /api/Document/DocumentTypeRightList | ReturnMessageData | PO+SO list |
| 8 | GET /api/PaymentTerm/PaymentTermList | ReturnMessageData | PO+SO master |
| 9 | GET /api/Currency/GetCurrency | ReturnMessageData | PO+SO master |
| 10 | GET /api/Warehouse/GetListWarehouse | ReturnMessageData | PO+SO master |
| 11 | GET /api/Company/ComapyInfo | ReturnMessageData | PO+SO master |
| 12 | GET /api/Serie/SeriesAndGroupDoc | ReturnMessageData | PO+SO form |
| 13 | GET /api/ItemUnit/UnitConversionList | ReturnMessageData | PO+SO form |
| 14 | GET /api/Approved/Config/{moduleCode} | ReturnMessageData | PO+SO approval config |
| 15 | POST /api/Approved/Approve | ReturnMessageData | PO+SO approval action |

### Purchase Order

| # | Endpoint | Return Type | Notes |
|---|----------|-------------|-------|
| 16 | GET /api/PO/POHeaderList | ReturnPaginationData | PO list |
| 17 | GET /api/PO/POOrder | ReturnMessageData | PO edit |
| 18 | POST /api/PO/POInsert | ReturnMessage | PO form (no result) |
| 19 | POST /api/PO/POUpdate | ReturnMessage | PO form (no result) |
| 20 | POST /api/PO/CheckStatus | ReturnMessageData | PO check before edit/cancel |
| 21 | POST /api/PO/POCancel | ReturnMessage | PO cancel (no result) |
| 22 | GET /api/Supplier/SupplierList | ReturnPaginationData | PO form |
| 23 | GET /api/Supplier/GetSupplier | ReturnMessageData | PO form |

### Sales Order

| # | Endpoint | Return Type | Notes |
|---|----------|-------------|-------|
| 24 | GET /api/SO/SOHeaderList | ReturnPaginationData | SO list |
| 25 | GET /api/SO/SOOrder | ReturnMessageData | SO edit |
| 26 | POST /api/SO/SOInsert | ReturnMessage | SO form (no result) |
| 27 | POST /api/SO/SOUpdate | ReturnMessage | SO form (no result) |
| 28 | POST /api/SO/CheckStatus | ReturnMessageData | SO check before edit/cancel |
| 29 | POST /api/SO/SOCancel | ReturnMessage | SO cancel (no result) |
| 30 | GET /api/Customer/CustomerList | ReturnPaginationData | SO form |
| 31 | GET /api/Customer/GetCustomer | ReturnMessageData | SO form |
| 32 | GET /api/Salesman/SalesmanList | ReturnPaginationData | SO form |
| 33 | GET /api/Salesman/GetSalesman | ReturnMessageData | SO form |
| 34 | GET /api/PaymentTerm/CalculatePayment | ReturnMessageData | SO form |
| 35 | GET /api/Transportation/TransportationList | ReturnPaginationData | SO form |
| 36 | GET /api/Transportation/GetTransportation | ReturnMessageData | SO form |

## Frontend Type Mapping

| Backend | Frontend | Success Check |
|---------|----------|---------------|
| ReturnMessageData | `ApiResponse<T>` | `response.code === 0` |
| ReturnPaginationData | `PaginatedApiResponse<T>` | `response.code === 0` |
| ReturnMessage | `ApiResponse<unknown>` | `response.code === 0` |
| ReturnAPI (legacy) | `ApiResponseAlt<T>` | `response.status === true` |

## Fixed Mismatch (2026-02-05)

### Fix 1: Approved endpoints (#14, #15)
backend ส่ง `ReturnMessageData` (code/msg/result) แต่ frontend PO+SO module ใช้ `ApiResponseAlt` (status/message/data)

**ยืนยันจาก actual API response:** backend ส่ง `{ code: 0, msg, errorCode, result }` (Pattern 1)

**แก้ไขแล้ว:** เปลี่ยน frontend ทั้ง PO + SO ให้ใช้ `ApiResponse<T>` + เช็ค `response.code === 0` + ใช้ `response.result`/`response.msg`

## Fixed Mismatch (2026-02-06)

### Fix 2: Salesman + Transportation Info endpoints (#33, #36)
backend ส่ง `ReturnMessageData` (code/msg/result) แต่ frontend SO module types ใช้ `status/message/data` pattern

**ไฟล์ที่แก้ไข (3 ไฟล์):**
1. **`Q-ERPc/sales/sales-order/src/types/salesman.ts`** — `SalesmanInfoResponse` เปลี่ยนจาก `status/message/data` → `code/msg/result`
2. **`Q-ERPc/sales/sales-order/src/types/transportation.ts`** — `TransportationInfoResponse` เปลี่ยนจาก `status/message/data` → `code/msg/result`
3. **`Q-ERPc/sales/sales-order/src/pages/SOForm.tsx`** — 4 จุดที่เช็ค `response.status && response.data` → `response.code === 0 && response.result`

**ผลกระทบก่อนแก้:** ข้อมูล Salesman และ Transportation ไม่ถูก populate ลง form เพราะเช็ค `response.status` (undefined) แทน `response.code === 0`

## GlobalExceptionMiddleware

เมื่อเกิด unhandled exception → middleware จับแล้วส่ง:
```json
{ "Code": statusCode, "Msg": "Thai message", "ErrorCode": "ERROR_CODE", "Result": null }
```

HTTP Status mapping:
- SQL Timeout → 504 + DATABASE_TIMEOUT
- SQL Connection → 503 + DATABASE_UNAVAILABLE
- HttpClient Timeout → 504 + EXTERNAL_SERVICE_TIMEOUT
- Other → 500 + SERVER_INTERNAL

## ErrorCodes (c:\GitHub\QERPC-API\QercAPI\Utility\ErrorCodes.cs)

Categories: AUTH_*, VALIDATION_*, DATA_*, BUSINESS_*, SERVER_*, DATABASE_*, EXTERNAL_*

### AUTH ErrorCodes ที่ Frontend ใช้

| errorCode | HTTP Status | Meaning | Frontend Handling |
|-----------|-------------|---------|-------------------|
| `AUTH_TOKEN_INVALID` | 401 | Token หมดอายุ/ถูกยกเลิก | httpClient swallow + Modal → logout |
| `AUTH_LOGIN_FAILED` | 401 | ชื่อผู้ใช้/รหัสผ่านผิด | error propagate → login form แสดง msg |

> **สำคัญ:** httpClient interceptor เช็ค `errorCode === 'AUTH_TOKEN_INVALID'` เท่านั้นถึงจะ dispatch event + swallow error อื่นๆ ปล่อยไปปกติ
