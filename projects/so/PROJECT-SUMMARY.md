# Project Summary: Sales Order (SO)

> Last updated: 2026-02-05
> Scanned by: Scout Agent
> Source: `project.json` → `c:\Users\Kongsit\Desktop\QReact\Q-ERPc\sales\sales-order`
> Scan mode: Quick (single module focus)
> Total files scanned: ~96 files
> Parent project: QReact (Micro-Frontend ERP System)

## Overview

Sales Order Module เป็น Remote Module ของระบบ Q-ERP สำหรับจัดการใบสั่งขาย (SO)
รองรับ Create, Edit, View, Cancel, Multi-level Approval, VAT Calculation, PDF Report/Print
ทำงานเป็น Micro-Frontend ผ่าน Module Federation โดยมี Portal เป็น Host App

---

## Tech Stack

| Category | Technology | Version |
|----------|------------|---------|
| Framework | React | ^19.2.0 |
| Language | TypeScript | ~5.9.3 (strict mode) |
| Build Tool | Vite | ^7.2.4 |
| Module Federation | @originjs/vite-plugin-federation | ^1.4.1 |
| UI Library | Ant Design | ^6.1.0 |
| Icons | @ant-design/icons | ^6.1.0 |
| Routing | react-router-dom | ^7.10.1 |
| State Management | Zustand | ^5.0.9 |
| HTTP Client | Axios | ^1.13.2 |
| Date | dayjs (Thai locale) | - |
| Shared Library | @qerp/shared | workspace |
| Linting | ESLint | ^9.39.1 |

---

## Commands

| Command | Script | หน้าที่ |
|---------|--------|--------|
| `npm run dev` | `vite` | Dev server (port 5006) |
| `npm run dev:integrated` | `run-p build:watch preview` | Integrated dev with host |
| `npm run build` | `tsc -b && vite build` | Production build |
| `npm run build:cloud` | `tsc -b && vite build --mode cloud` | Cloud build |
| `npm run build:watch` | `vite build --watch --mode development` | Watch mode |
| `npm run lint` | `eslint .` | Lint check |
| `npm run preview` | `vite preview` | Preview build |

**Port:** 5006 (strict)
**Module Name:** `salesOrder`
**Remote Entry:** `remoteEntry.js`
**Exposes:** `./App` (App.tsx), `./version` (version.ts)
**Shared:** react, react-dom, react-router-dom, antd

---

## Project Structure

```
sales-order/
├── src/
│   ├── App.tsx                    # Module entry point (exposed via federation)
│   ├── App.css                    # Global styles (legacy)
│   ├── main.tsx                   # Standalone dev entry (BrowserRouter + dev props)
│   ├── index.css                  # Global CSS + utility classes
│   ├── version.ts                 # Module version export
│   │
│   ├── components/                # 21 UI Components
│   │   ├── index.ts               # Barrel export
│   │   ├── ApprovalStatusTag.tsx   # Dropdown badge สถานะอนุมัติ
│   │   ├── CancelSOModal.tsx       # Modal ยืนยันยกเลิก SO
│   │   ├── CheckStatusModal.tsx    # State machine modal (confirm/loading/warning/error)
│   │   ├── ColumnSelector.tsx      # Popover เลือกคอลัมน์ที่แสดง
│   │   ├── CustomerSearchModal.tsx # Modal ค้นหาลูกค้า (paginated)
│   │   ├── CustomerSection.tsx     # Form ข้อมูลลูกค้า 5 rows
│   │   ├── CustomerSection.module.css
│   │   ├── EditableDiscountCell.tsx # Editable cell ส่วนลด (%, cascading %)
│   │   ├── EditableNumberCell.tsx   # Editable cell ตัวเลข (commas, precision)
│   │   ├── ErrorModal.tsx          # Generic error/warning dialog
│   │   ├── ItemSearchModal.tsx     # Modal ค้นหาสินค้า (paginated)
│   │   ├── PrintFormSelectModal.tsx # เลือกรูปแบบพิมพ์ + สร้าง PDF
│   │   ├── RejectReasonModal.tsx   # Modal รับเหตุผลไม่อนุมัติ
│   │   ├── SalesmanSearchModal.tsx  # Modal ค้นหาพนักงานขาย
│   │   ├── SaveStatusModal.tsx     # Modal สถานะบันทึก (saving/success/error)
│   │   ├── SOFormHeader.tsx        # Header ฟอร์ม (title + serie badge + buttons)
│   │   ├── SOFormTabs.tsx          # Tabs: สถานที่เก็บ + หมายเหตุ/บันทึก
│   │   ├── SOLineItemsSection.tsx  # Wrapper section รายการสินค้า
│   │   ├── SOLineItemsSection.module.css
│   │   ├── SOLineItemTable.tsx     # ตารางรายการสินค้า (inline edit)
│   │   ├── SOSearchFilter.tsx      # Search bar + document type dropdown
│   │   ├── SOSummarySection.tsx    # Summary card (totals/discount/VAT)
│   │   ├── SOSummarySection.module.css
│   │   └── TransportationSearchModal.tsx # Modal ค้นหาที่จัดส่ง
│   │
│   ├── hooks/                     # 17 Custom Hooks
│   │   ├── index.ts               # Barrel export
│   │   ├── useApprovalModal.ts     # จัดการ modal อนุมัติ/ปฏิเสธ
│   │   ├── useApprovedConfig.ts    # ดึงการตั้งค่า approval levels
│   │   ├── useCheckStatusModal.ts  # ตรวจสถานะก่อน edit/cancel
│   │   ├── useCustomerHandlers.ts  # ค้นหา/เลือกลูกค้า + คำนวณวันครบชำระ
│   │   ├── useDeleteLineValidation.ts # จำลองลบ → คำนวณ VAT ใหม่
│   │   ├── useDocumentTypes.ts     # ดึงประเภทเอกสาร
│   │   ├── useLineItemHandlers.ts  # CRUD รายการสินค้า + unit conversion
│   │   ├── useMasterData.ts        # ดึง master data (payment, currency, warehouse, company)
│   │   ├── usePermission.ts        # Context wrapper สำหรับ action permission
│   │   ├── usePrintModal.ts        # จัดการ print preview + form selection
│   │   ├── useSerieInfo.ts         # ดึงเลขที่ SO ถัดไป
│   │   ├── useSOColumns.tsx        # Generate dynamic table columns
│   │   ├── useSOFormData.ts        # Compose hook (master + serie + edit data)
│   │   ├── useSOFormSubmit.ts      # Submit form (insert/update) + validation
│   │   ├── useSOListData.ts        # ข้อมูลหน้า list (doc types, headers, pagination)
│   │   └── useVATCalculation.ts    # Debounced VAT calculation via API + rollback
│   │
│   ├── services/                  # 18 Service Files (API calls)
│   │   ├── index.ts               # Barrel export
│   │   ├── httpClient.ts          # HttpClient instance จาก @qerp/shared
│   │   ├── soService.ts           # Core SO CRUD (6 endpoints)
│   │   ├── customerService.ts     # Customer list + detail (2 endpoints)
│   │   ├── salesmanService.ts     # Salesman list + detail (2 endpoints)
│   │   ├── transportationService.ts # Transportation list + detail (2 endpoints)
│   │   ├── itemService.ts         # Item list + unit conversion (2 endpoints)
│   │   ├── approvalService.ts     # Submit approval/rejection (1 endpoint)
│   │   ├── approvedConfigService.ts # Approval config (1 endpoint)
│   │   ├── calculateService.ts    # VAT calculation (1 endpoint)
│   │   ├── companyService.ts      # Company info (1 endpoint)
│   │   ├── currencyService.ts     # Currency + exchange rate (2 endpoints)
│   │   ├── documentService.ts     # Document types (1 endpoint)
│   │   ├── paymentTermService.ts  # Payment terms + due date calc (2 endpoints)
│   │   ├── permissionService.ts   # Action permission Tier 3 (1 endpoint)
│   │   ├── printFormService.ts    # Print forms + PDF generation (2 endpoints)
│   │   ├── serieService.ts        # Document series numbering (1 endpoint)
│   │   └── warehouseService.ts    # Warehouse list (1 endpoint)
│   │
│   ├── types/                     # 18 Type Definition Files
│   │   ├── index.ts               # Barrel export
│   │   ├── soHeader.ts            # SOHeader, SOOrder, SODetail, SOLineItem (CORE)
│   │   ├── customer.ts            # Customer, CustomerDetail
│   │   ├── salesman.ts            # Salesman
│   │   ├── transportation.ts      # Transportation
│   │   ├── item.ts                # ItemListItem, UnitConversion
│   │   ├── approval.ts            # ApprovalRequest, ApprovalResponse
│   │   ├── approvedConfig.ts      # ApprovedLevel, ApprovedAction, ApprovedConfigData
│   │   ├── calculate.ts           # CalculateHeader, CalculateDetail, CalculateVatRequest
│   │   ├── checkStatus.ts         # CheckStatusRequest, CheckStatusResult
│   │   ├── company.ts             # CompanyInfo (VAT rate, noDigit settings)
│   │   ├── currency.ts            # Currency, ExchangeRate
│   │   ├── documentType.ts        # DocumentType
│   │   ├── paymentTerm.ts         # PaymentTerm
│   │   ├── permission.ts          # ActionPermission, Permission, Company
│   │   ├── printForm.ts           # PrintForm, SOReportPDFRequest
│   │   ├── serie.ts               # SeriesAndGroupDocResult
│   │   └── warehouse.ts           # Warehouse
│   │
│   ├── stores/                    # 2 Zustand Stores
│   │   ├── index.ts               # Barrel export + selector hooks
│   │   ├── authStore.ts           # Auth state + action permission
│   │   └── soStore.ts             # SO list state (doc types, headers, pagination)
│   │
│   ├── contexts/                  # Permission Context (3 files)
│   │   ├── index.ts               # Barrel export
│   │   ├── permissionContextValue.ts # PermissionContextValue type + createContext
│   │   └── PermissionContext.tsx   # PermissionProvider (fetches Tier 3 JWT)
│   │
│   ├── utils/                     # 5 Utility Files
│   │   ├── index.ts               # Barrel export
│   │   ├── calculations.ts        # Discount parsing, line amount, VAT calc
│   │   ├── formatters.ts          # Number/date formatting (commas, decimals)
│   │   ├── statusHelpers.ts       # Approval/record status → text + color
│   │   └── errorHelpers.ts        # API error extraction + handling
│   │
│   ├── constants/                 # 1 Constants File
│   │   └── index.ts               # DEFAULT_PAGE_SIZE, SEARCH_DELAY, TABLE_SCROLL_OFFSET, etc.
│   │
│   ├── styles/
│   │   └── printPreview.css       # Print stylesheet
│   │
│   └── assets/
│       └── react.svg
│
├── package.json
├── vite.config.ts
├── tsconfig.json
├── tsconfig.app.json
└── tsconfig.node.json
```

---

## Key Files

| File | Purpose |
|------|---------|
| `src/App.tsx` | Module entry point - sync Portal props → Zustand, PermissionProvider, Routes |
| `src/main.tsx` | Standalone dev entry (BrowserRouter + dev mock props) |
| `src/pages/SOList.tsx` | หน้ารายการ SO (search, filter, table, approval actions) |
| `src/pages/SOForm.tsx` | หน้าสร้าง/แก้ไข SO (form, line items, VAT calc, modals) |
| `src/pages/SOPrintPreview.tsx` | หน้าพิมพ์ SO (portal to document.body) |
| `src/stores/authStore.ts` | Auth + permission state (Zustand) |
| `src/stores/soStore.ts` | SO list state (Zustand) + logout listener |
| `src/contexts/PermissionContext.tsx` | Tier 3 JWT permission provider |
| `src/services/soService.ts` | Core SO API: list, insert, update, cancel, checkStatus |
| `src/hooks/useSOFormData.ts` | Compose hook: master data + serie + edit data |
| `src/hooks/useVATCalculation.ts` | Debounced VAT calculation with rollback |
| `vite.config.ts` | Module Federation config (name: salesOrder, port: 5006) |

---

## Routes / Pages

| Route | Component | หน้าที่ | Props |
|-------|-----------|--------|-------|
| `/` (index) | SOList | หน้ารายการใบสั่งขาย | canInsert, canEdit |
| `/create` | SOForm | สร้างใบสั่งขายใหม่ | canEdit (=canInsert) |
| `/edit/:id` | SOForm | แก้ไขใบสั่งขาย | canEdit |
| `/edit/:id?view=true` | SOForm | ดูรายละเอียด (read-only) | - |
| `/edit/:id?print=true&view=true` | SOForm | Auto-print mode | - |

**Host Route (Portal):** `/sales/sales-order/*`

---

## API Endpoints (28 endpoints)

### Core SO Operations (6)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/SO/SOHeaderList` | soService | รายการ SO (paginated, search, filter) |
| POST | `/api/SO/SOInsert` | soService | สร้าง SO ใหม่ |
| GET | `/api/SO/SOOrder` | soService | ดึง SO detail สำหรับ edit/view |
| POST | `/api/SO/SOUpdate` | soService | อัพเดท SO |
| POST | `/api/SO/SOCancel` | soService | ยกเลิก SO |
| POST | `/api/SO/CheckStatus` | soService | ตรวจ status ก่อน edit/cancel |

### SO-Specific Master Data (6)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/Customer/CustomerList` | customerService | รายการลูกค้า (paginated) |
| GET | `/api/Customer/GetCustomer` | customerService | รายละเอียดลูกค้า (credit, delivery) |
| GET | `/api/Salesman/SalesmanList` | salesmanService | รายการพนักงานขาย |
| GET | `/api/Salesman/GetSalesman` | salesmanService | รายละเอียดพนักงานขาย |
| GET | `/api/Transportation/TransportationList` | transportationService | รายการวิธีขนส่ง |
| GET | `/api/Transportation/GetTransportation` | transportationService | รายละเอียดขนส่ง |

### Shared Master Data (10)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/Item/ItemList` | itemService | รายการสินค้า (paginated) |
| GET | `/api/ItemUnit/UnitConversionList` | itemService | แปลงหน่วยสินค้า |
| GET | `/api/PaymentTerm/PaymentTermList` | paymentTermService | เงื่อนไขชำระเงิน |
| GET | `/api/PaymentTerm/CalculatePayment` | paymentTermService | คำนวณวันครบกำหนดชำระ |
| GET | `/api/Currency/GetCurrency` | currencyService | รายการสกุลเงิน |
| GET | `/api/Currency/GetExchangeRatePurchase` | currencyService | อัตราแลกเปลี่ยน (date format: MM-DD-YYYY) |
| GET | `/api/Warehouse/GetListWarehouse` | warehouseService | รายการคลังสินค้า |
| GET | `/api/Company/ComapyInfo` | companyService | ข้อมูลบริษัท + noDigit + VAT rate |
| GET | `/api/Document/DocumentTypeRightList` | documentService | ประเภทเอกสารที่มีสิทธิ์ |
| GET | `/api/Serie/SeriesAndGroupDoc` | serieService | เลขที่เอกสาร running number |

### Approval, Calculation & Report (6)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| POST | `/api/Calculate/CalculateVatAmount` | calculateService | คำนวณ VAT (debounced) |
| POST | `/api/Approved/Approve` | approvalService | อนุมัติ/ปฏิเสธ SO |
| GET | `/api/Approved/Config/SO` | approvedConfigService | ตั้งค่าระดับอนุมัติ |
| GET | `/api/Report/PrintFormList` | printFormService | รายการฟอร์มพิมพ์ |
| POST | `/api/Report/SOReportPDF` | printFormService | สร้าง PDF (Blob) |
| GET | `/api/JWT/QERPcMenuActionJWT/SO` | permissionService | Permission Tier 3 |

### API Response Formats

| Format | ใช้กับ |
|--------|--------|
| `ApiResponse<T>` `{code, msg, result}` | SO CRUD, Item, Warehouse, Company, Calculate, PaymentTerm, Currency, Serie, Document, Permission, PrintForm |
| `PaginatedApiResponse<T>` `{code, msg, result, totalCount, page, pageSize, totalPages}` | SOHeaderList, CustomerList, ItemList, SalesmanList, TransportationList |
| `ApiResponseAlt<T>` `{status, message, data}` | Salesman detail, Transportation detail, Approval, ApprovedConfig |
| Blob | SOReportPDF |

**Success convention:** `code === 0` → success, use `result`; `code !== 0` → error, show `msg`

---

## Modules / Functional Areas

### 1. SOList Page — หน้ารายการ

**Components Used:** SOSearchFilter, ColumnSelector (via useSOColumns), CheckStatusModal, CancelSOModal, SOPrintPreview, RejectReasonModal, ConfirmModal, PrintFormSelectModal

**Hooks Used:** useSOListData, useApprovedConfig, useCheckStatusModal, usePrintModal, useApprovalModal, useSOColumns

**Features:**
- Document type dropdown filter
- Search by SO number / customer name
- Paginated table (10/20/50/100 per page)
- Dynamic approval columns from API config
- Column visibility selector (persisted to localStorage)
- Responsive table scroll height
- Row highlighting: cancelled (red), selected (blue)
- Approval actions: approve/reject/wait/request per level
- Check status before edit/cancel
- Print form selection + PDF generation/viewing
- Cancel SO with confirmation

### 2. SOForm Page — หน้าสร้าง/แก้ไข

**Components Used:** SOFormHeader, CustomerSection, SOFormTabs, SOLineItemsSection, SOSummarySection, CustomerSearchModal, SalesmanSearchModal, TransportationSearchModal, ItemSearchModal, ConfirmModal, SaveStatusModal, ErrorModal

**Hooks Used:** useSOFormData, useVATCalculation, useCustomerHandlers, useLineItemHandlers, useSOFormSubmit

**Features:**
- **Customer Section:** ค้นหา/เลือกลูกค้า, ที่จัดส่ง, พนักงานขาย, เงื่อนไขชำระ, สกุลเงิน, อัตราแลกเปลี่ยน
- **Tabs Section:** คลังสินค้า (billing address auto-fill), หมายเหตุ, บันทึก
- **Line Items Section:** Inline editable table (item code search, quantity, unit, price, discount, note)
- **Summary Section:** Subtotal, discount (fixed/%), amount after discount, VAT, tax base, grand total
- Expand/collapse line items section
- Auto VAT calculation (debounced 300ms via API)
- Exchange rate auto-fetch on currency/date change
- Serie info badge (next SO number)
- Form validation before submit
- Confirm modal before save/cancel
- Save status modal (saving/success/error)
- beforeunload warning for unsaved changes
- View mode (read-only)
- Auto-print mode (?print=true&view=true)

### 3. SOPrintPreview — หน้าพิมพ์

**Rendered as:** React Portal to document.body (z-index 1000)

**Features:**
- Fetches SO data + customer detail for print
- Full document layout: header, customer info, items table, summary, signatures
- Min 8 rows in items table (fills empty rows)
- Print/Close toolbar (hidden during print)
- Hard-coded company info (Flag Victory Co., Ltd.)

---

## Stores (Zustand)

### authStore

| Field | Type | หน้าที่ |
|-------|------|--------|
| username | string | ชื่อผู้ใช้ |
| accessToken | string | Tier 2 JWT |
| companyCode | string | รหัสบริษัท |
| permission | Permission \| null | Menu permission |
| actionPermission | ActionPermission \| null | Tier 3 action permission |
| actionAccessToken | string \| null | Tier 3 JWT |
| canInsert | boolean | สิทธิ์สร้าง |
| canEdit | boolean | สิทธิ์แก้ไข |
| canPrint | boolean | สิทธิ์พิมพ์ |

**Actions:** setAuth, setActionPermission, reset

### soStore

| Field | Type | หน้าที่ |
|-------|------|--------|
| documentTypes | DocumentType[] | ประเภทเอกสาร |
| selectedDocumentTypeCode | string \| undefined | ประเภทที่เลือก |
| soHeaders | SOHeader[] | รายการ SO |
| pagination | {current, pageSize, total} | Pagination state |
| searchText | string | คำค้นหา |

**Actions:** setDocumentTypes, setSelectedDocumentTypeCode, setSOHeaders, setPagination, setSearchText, reset

**Selector Hooks:** useDocumentTypes(), useSelectedDocumentType(), useSOHeaders(), usePagination(), useSearchText()

**Logout Listener:** ฟัง `window.qerp:logout` event → reset store

---

## Permission System (3-Tier JWT)

```
Portal (Host)
  │
  ├─ Tier 1: LoginJWT → ได้ menu items + companies
  ├─ Tier 2: QERPcMenuJWT → ได้ route permission per company
  │
  └─ Props to SO: { username, accessToken(T2), companyCode, permission }
       │
       ▼
  SO App.tsx → sync to authStore
       │
       ▼
  PermissionProvider → GET /api/JWT/QERPcMenuActionJWT/SO
       │
       ▼
  Tier 3: ActionJWT → { accessToken(T3), actionPermission }
       │                  insert: Y/N
       │                  edit: Y/N
       │                  print: Y/N
       ▼
  authStore → canInsert, canEdit, canPrint
       │
       ▼
  Hooks ใช้ T3 token เรียก API
```

---

## Constants

| Constant | Value | ใช้ทำอะไร |
|----------|-------|----------|
| DEFAULT_PAGE_SIZE | 20 | Pagination default |
| SEARCH_DELAY | 500 | Debounce delay (ms) |
| TABLE_SCROLL_OFFSET | 370 | Table height calc offset (px) |
| MIN_TABLE_HEIGHT | 200 | Minimum table height (px) |
| LOADING_SPIN_HEIGHT | 400 | Spinner height (px) |
| BUDDHIST_YEAR_OFFSET | 543 | Thai calendar offset |
| DEFAULT_CURRENCY_CODE | 'THB' | Default currency |
| DEFAULT_EXCHANGE_RATE | 1 | Default exchange rate |
| DEFAULT_VAT_RATE | 7 | Default VAT % |
| MIN_PRINT_TABLE_ROWS | 8 | Min rows in print table |
| VISIBLE_COLUMNS_STORAGE_KEY | 'so-list-visible-columns' | localStorage key |

---

## Code Conventions

### Naming

| Type | Pattern | Example |
|------|---------|---------|
| Component | PascalCase | `SOSearchFilter.tsx` |
| Hook | camelCase + "use" | `useSOColumns.tsx` |
| Service | camelCase + "Service" | `soService.ts` |
| Type | PascalCase | `SOHeader` |
| Store | camelCase + "Store" | `authStore.ts` |
| Store Hook | use + PascalCase | `useAuthStore()` |
| Selector Hook | use + PascalCase | `useDocumentTypes()` |
| Constant | UPPER_SNAKE_CASE | `DEFAULT_PAGE_SIZE` |
| CSS Module | Component.module.css | `SOList.module.css` |

### Patterns

1. **Service Pattern** — API calls ใน `services/`, async functions รับ accessToken + packageCode
2. **Hook Pattern** — Business logic ใน `hooks/`, เรียก services + จัดการ state
3. **Store Pattern** — Global state ด้วย Zustand + selector hooks
4. **Compose Hook Pattern** — useSOFormData รวม useMasterData + useSerieInfo + useSOEditData
5. **Barrel Exports** — ทุก folder มี `index.ts`
6. **Type-first** — สร้าง types ก่อน → services → hooks → components
7. **useRef Duplicate Prevention** — ป้องกัน StrictMode double-fetch
8. **Debounced API** — useVATCalculation (300ms), search modals (500ms)
9. **State Machine Modals** — CheckStatusModal, SaveStatusModal (confirm/loading/warning/error)
10. **Soft Delete** — Line items: statusRow='D' (existing) vs remove (new)

### Language

- **UI Text:** Thai
- **Code:** English

---

## Key Patterns with Context

### Search Modal Pattern (4 modals)

CustomerSearchModal, ItemSearchModal, SalesmanSearchModal, TransportationSearchModal ใช้ pattern เดียวกัน:
- useAuthStore สำหรับ token/company
- Debounced search (500ms) ด้วย useRef
- prevOpenRef tracking ป้องกัน duplicate fetch
- Pagination [10, 20, 50, 100]
- Double-click row to select
- Error Alert display

### VAT Calculation Flow

```
Form value เปลี่ยน (lineItems, discount, vatRate, etc.)
  → useVATCalculation (debounced 300ms)
  → POST /api/Calculate/CalculateVatAmount
  → อัพเดท form fields + lineItems
  → Error? → rollback to last valid state + show ErrorModal
```

### Token Flow

```
Portal → App.tsx props → authStore.setAuth()
  → PermissionProvider → /api/JWT/QERPcMenuActionJWT/SO
  → authStore.setActionPermission(T3 token)
  → All hooks read T3 from authStore
  → All services use T3 as Authorization header
```

---

## For Each Role

### PM Should Know

- **Existing features:** Create, Edit, View, Cancel SO, Multi-level Approval (1-5 levels), VAT Calculation, PDF Report/Print, Document Series
- **Entity relationships:** Customer, Salesman, Transportation, Item, Warehouse, PaymentTerm, Currency
- **Multi-company:** รองรับหลาย company ต่อ user
- **Approval workflow:** 1-5 level (configurable from backend)
- **Print:** PDF generation + preview + direct print
- **Not implemented:** Delivery tracking, Invoice linking

### Designer Should Know

- **UI Library:** Ant Design 6 (Thai locale)
- **Icons:** @ant-design/icons 6
- **Styling:** CSS Modules + global utility classes in index.css
- **Color system:**
  - Primary blue: #1890ff
  - Success green: #52c41a
  - Error red: #ff4d4f
  - Warning orange: #faad14
  - Cancelled row: #ffccc7
  - Selected row: #bae0ff
  - Summary card: #f0f5ff (light blue)
  - Total row: #1e3a5f (dark blue)
- **Existing components ที่ reuse ได้:** EditableNumberCell, EditableDiscountCell, SOSearchFilter, ColumnSelector, ApprovalStatusTag, ErrorModal, SaveStatusModal, CheckStatusModal
- **Layout:** SOForm = vertical flex (header + scrollable form content)
- **Form layout:** CustomerSection (Card) → SOFormTabs (Card) → SOLineItemsSection (Card, expandable) → SOSummarySection

### Developer Should Know

- **Architecture:** Micro-Frontend Remote Module (Module Federation)
- **State management:** Zustand (authStore, soStore) + React Context (PermissionContext)
- **API layer:** Service Pattern → httpClient จาก @qerp/shared
- **Hook composition:** useSOFormData = useMasterData + useSerieInfo + useSOEditData
- **VAT calculation:** API-based (not client-side), debounced 300ms, state rollback on error
- **Line items:** Soft delete (statusRow='D'), inline editing, auto unit conversion
- **Date format ระวัง:** Exchange rate API ใช้ MM-DD-YYYY (ต่างจาก API อื่น)
- **API response format:** มี 3 แบบ (ApiResponse, PaginatedApiResponse, ApiResponseAlt) ดูตาราง
- **Company Info API typo:** `/api/Company/ComapyInfo` (ComaPy ไม่ใช่ ComPany)
- **Approval actions:** Y=Complete, W=Process, N=UnComplete, P=Request
- **Form Enter key:** ถูก prevent ยกเว้น TEXTAREA fields

### QA Should Know

- **Test framework:** ไม่มี (ไม่มี test files)
- **Manual testing:** `npm run dev` → http://localhost:5006
- **Dev mock data:** main.tsx มี dev props (username: "สมชาย ทดสอบ", DEV-TOKEN-999)
- **Critical paths to test:**
  1. Create SO (form validation, line items, VAT calc, submit)
  2. Edit SO (load existing data, modify, update)
  3. Cancel SO (check status → confirm → cancel)
  4. Approval workflow (all 5 levels, approve/reject/wait/request)
  5. Print (form selection, PDF generation, preview, direct print)
  6. Search modals (customer, salesman, transportation, item)
  7. Currency + exchange rate change
  8. Discount formats (fixed amount, %, cascading %)
  9. Line item delete/undo
  10. beforeunload warning

### DevOps Should Know

- **Build:** `npm run build` (tsc + vite build)
- **Build output:** Module Federation remote entry (remoteEntry.js)
- **Port:** 5006 (strict)
- **Module name:** salesOrder
- **Shared libs:** react, react-dom, react-router-dom, antd
- **Deploy:** ผ่าน QReact parent project scripts
- **ENV:** VITE_API_BASE_URL, VITE_API_TOKEN_BEARER, VITE_API_DEFAULT_PACKAGE (set by parent scripts)

---

## Dependencies with Other Modules

| Module | Relationship |
|--------|-------------|
| **Portal (Host)** | รับ props: username, accessToken, companyCode, permission |
| **@qerp/shared** | ใช้ HttpClient, createHttpClient, ApiResponse types, ConfirmModal, extractApiError |
| **Backend (.NET)** | เรียก 28 API endpoints |

---

## Notes / Technical Debt

1. **ไม่มี Test:** ไม่มี test framework หรือ test files
2. **App.css ผิด module:** มี Sales Visitor styles แทน SO styles
3. **Hard-coded company info ในหน้า Print:** ควรดึงจาก API
4. **Print page numbering:** Hard-coded "หน้า 1/1"
5. **Salesman/Transportation detail ใช้ ApiResponseAlt:** ต่างจาก API อื่นที่ใช้ ApiResponse — อาจเกิด confusion
6. **Exchange rate date format:** ใช้ MM-DD-YYYY ต่างจาก API อื่น (ISO) — ต้องระวัง
7. **Company API typo:** ComapyInfo (backend ต้องแก้)
8. **ConfirmModal import path:** SOForm.tsx import จาก relative path `../../../../../shared/src` แทน `@qerp/shared` — ควรแก้
9. **PO/SO code ซ้ำกันมาก:** ~80% structure เหมือนกัน อาจ extract shared logic ได้
