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

Legacy controllers: Dashboard, CustomerCategory, FGStock, Pallet, Serie*, TeamDelivery, TransactionCategory, TransactionContactOfMaster, Vehicle, WO

> *Serie controller มี endpoint `SeriesAndGroupDoc` ที่ใช้ ReturnMessageData (Pattern 1) ซึ่ง frontend เรียก

## 33 APIs ที่ Frontend เรียก

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
| 33 | GET /api/PaymentTerm/CalculatePayment | ReturnMessageData | SO form |

## Frontend Type Mapping

| Backend | Frontend | Success Check |
|---------|----------|---------------|
| ReturnMessageData | `ApiResponse<T>` | `response.code === 0` |
| ReturnPaginationData | `PaginatedApiResponse<T>` | `response.code === 0` |
| ReturnMessage | `ApiResponse<unknown>` | `response.code === 0` |
| ReturnAPI (legacy) | `ApiResponseAlt<T>` | `response.status === true` |

## Potential Mismatch

Approved endpoints (#14, #15) — backend ส่ง `ReturnMessageData` (code/msg/result) แต่ frontend PO+SO module ใช้ `ApiResponseAlt` (status/message/data) → ควรตรวจสอบเพิ่มเติม

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
Frontend สามารถใช้ errorCode เพื่อ handle business logic ได้ (แต่ยังไม่ค่อยใช้)
