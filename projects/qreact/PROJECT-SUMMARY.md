# Project Summary: QReact (Q-ERP)

> Last updated: 2026-02-04
> Scanned by: Scout Agent
> Source: `project.json` → `c:\Users\Kongsit\Desktop\QReact`
> Scan mode: Module (9 modules)
> Total files scanned: ~283 files

## Overview

Micro-Frontend ERP System สำหรับจัดการงาน Purchase, Sales, Analytics และ Business Data Monitoring
ใช้ React 19 + TypeScript + Vite + Module Federation (@originjs/vite-plugin-federation)
แบ่งเป็น Host (Portal) + 6 Remote Modules + 1 External Module (QAI)

---

## Tech Stack

| Category | Technology | Version |
|----------|------------|---------|
| Framework | React | ^19.2.0 |
| Language | TypeScript | ~5.9.3 |
| Build Tool | Vite | ^7.2.4 |
| Module Federation | @originjs/vite-plugin-federation | ^1.4.1 |
| UI Library | Ant Design | ^6.1.0 |
| Icons | @ant-design/icons | ^6.1.0 |
| Routing | react-router-dom | ^7.10.1 |
| State Management | Zustand | ^5.0.9 |
| HTTP Client | Axios | ^1.13.2 |
| Linting | ESLint | ^9.39.1 |
| Package Manager | npm workspaces | - |

---

## Commands

| Command | Script | หน้าที่ |
|---------|--------|--------|
| `npm run dev` | `node scripts/dev.js` | Interactive mode (เลือก server + module) |
| `npm run dev:server` | `node scripts/dev.js server` | รันกับ Server API (192.168.0.131) |
| `npm run dev:local` | `node scripts/dev.js local` | รันกับ Local API (localhost) |
| `npm run dev:list` | `node scripts/dev.js --list` | ดู modules ทั้งหมด |
| `npm run build` | `node scripts/build.js` | Interactive build |
| `npm run build:cloud` | `node scripts/build.js cloud` | Build ไป cloud (203.150.53.240) |
| `npm run build:production` | `node scripts/build.js production` | Build ไป production |
| `npm run portal` | `cd portal && npm run dev` | รัน portal อย่างเดียว |
| `npm run generate-config` | `node scripts/generate-config.js` | สร้าง vite.config.ts จาก config.js |

**Open:** http://localhost:5000

---

## Project Structure

```
QReact/
├── portal/                         # Host App (Port 5000)
│   └── src/
│       ├── components/             # UI Components (ErrorBoundary, MainLayout, RemoteWrappers, etc.)
│       ├── constants/              # Constants (routes, auth, layout, modules, colors, errors)
│       ├── contexts/               # AuthContext
│       ├── hooks/                  # useAuth, useModuleVersions
│       ├── pages/                  # Login, Main, Unauthorized
│       ├── services/               # authService, httpClient, authHelpers
│       ├── types/                  # Auth types
│       ├── utils/                  # permissionUtils, logger
│       └── config/                 # Feature flags
│
├── Q-ERPc/
│   ├── purchase/
│   │   └── purchase-order/         # Purchase Order Module (Port 5002)
│   │       └── src/
│   │           ├── components/     # 19 components
│   │           ├── hooks/          # 18 hooks
│   │           ├── services/       # 15 services
│   │           ├── types/          # 15 type files
│   │           ├── pages/          # 3 pages (List, Detail, Print)
│   │           └── store/          # Zustand stores
│   ├── sales/
│   │   ├── sales-order/            # Sales Order Module (Port 5006)
│   │   │   └── src/                # (เหมือน PO แต่สำหรับ Sales)
│   │   │       ├── components/     # 23 components
│   │   │       ├── hooks/          # 17 hooks
│   │   │       ├── services/       # 16 services
│   │   │       ├── types/          # 17 type files
│   │   │       └── pages/          # 3 pages
│   │   └── sales-visitor/          # Sales Visitor Module (Port 5001)
│   │       └── src/                # Scaffold (mock data, ยังไม่ต่อ API)
│   └── analytics/
│       └── sales-analytics/        # Sales Analytics Module (Port 5005)
│           └── src/                # Dashboard + Charts
│
├── general/
│   └── dashboard/                  # Dashboard Module (Port 5003)
│       └── src/                    # Carousel landing page
│
├── business-data-monitoring/       # Business Data Module (Port 5004)
│   └── src/                        # Stub pages (4 placeholder routes)
│
├── shared/                         # @qerp/shared library
│   └── src/
│       ├── services/               # HttpClient (Axios wrapper)
│       ├── types/                  # API types (12+ interfaces)
│       └── components/             # ConfirmModal
│
├── scripts/                        # Central Build System
│   ├── config.js                   # 🔥 Central config (servers, modules, ports)
│   ├── dev.js                      # Dev server runner
│   ├── build.js                    # Production builder
│   └── generate-config.js          # vite.config.ts generator
│
└── package.json                    # Root workspace config
```

---

## Key Files

| File | Purpose |
|------|---------|
| `scripts/config.js` | Central config - servers, modules, ports ทุกอย่างมาจากที่นี่ |
| `portal/src/App.tsx` | Root component, AuthProvider wrapper, Login/Main routing |
| `portal/src/pages/Main.tsx` | Main layout with Routes to all remote modules |
| `portal/src/contexts/AuthContext.tsx` | 2-Tier JWT Authentication context |
| `portal/src/components/RemoteWrappers.tsx` | Lazy-load remote modules via federation |
| `portal/src/components/RouteGuard.tsx` | Permission-based route protection |
| `portal/src/constants/modules.ts` | Menu items and module mapping |
| `portal/src/config/features.ts` | Feature flags |
| `shared/src/services/httpClient.ts` | Axios wrapper ใช้ร่วมทุก module |
| `shared/src/types/index.ts` | Shared API types |

---

## Dependencies (สำคัญ)

### Production

| Package | Version | ใช้ทำอะไร |
|---------|---------|----------|
| react | ^19.2.0 | UI framework |
| react-dom | ^19.2.0 | DOM rendering |
| react-router-dom | ^7.10.1 | Routing (ทุก module) |
| antd | ^6.1.0 | UI component library (Thai locale) |
| @ant-design/icons | ^6.1.0 | Icon library |
| axios | ^1.13.2 | HTTP client |
| zustand | ^5.0.9 | State management (remote modules) |
| @qerp/shared | workspace | Shared library (HttpClient, types, components) |

### Dev

| Package | Version | ใช้ทำอะไร |
|---------|---------|----------|
| typescript | ~5.9.3 | Type checking |
| vite | ^7.2.4 | Build tool + dev server |
| @originjs/vite-plugin-federation | ^1.4.1 | Module Federation |
| @vitejs/plugin-react | ^5.1.1 | React Fast Refresh |
| eslint | ^9.39.1 | Linting |
| npm-run-all | ^4.1.5 | Run multiple scripts (dev:integrated) |

---

## Modules

### Module: Portal (Host)

**Path:** `portal/src/`
**Port:** 5000
**Files:** ~44 files
**Role:** Host app - จัดการ Auth, Layout, Routing, โหลด Remote Modules

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| MainLayout | MainLayout.tsx | Layout หลัก (Sidebar + Content) |
| MainHeader | MainHeader.tsx | Header bar (title, company selector, user info) |
| AppSidebar | AppSidebar.tsx | Sidebar menu navigation |
| ErrorBoundary | ErrorBoundary.tsx | จับ error จาก remote modules |
| RouteGuard | RouteGuard.tsx | ตรวจ permission ก่อนเข้า route |
| ProtectedRoute | ProtectedRoute.tsx | ตรวจ authentication (redirect to login) |
| PublicRoute | PublicRoute.tsx | Route สำหรับ unauthenticated users |
| CompanySelector | CompanySelector.tsx | เปลี่ยน company (multi-company support) |
| PageTitleBar | PageTitleBar.tsx | แถบ title ของแต่ละหน้า |
| RemoteWrappers | RemoteWrappers.tsx | Lazy wrappers สำหรับทุก remote module |

#### Hooks

| Hook | File | หน้าที่ |
|------|------|--------|
| useAuth | useAuth.ts | จัดการ login/logout/token/permission |
| useModuleVersions | useModuleVersions.ts | ตรวจ version ของ remote modules |

#### Services

| Service | File | หน้าที่ |
|---------|------|--------|
| authService | authService.ts | API calls สำหรับ login, getPermission, getMenuJWT |
| authHelpers | authHelpers.ts | Helper functions สำหรับ auth flow |
| httpClient | httpClient.ts | Axios instance (portal-specific) |

#### Constants

| File | หน้าที่ |
|------|--------|
| routes.ts | Route paths, MENU_PATHS, PATH_PATTERNS, ROUTES |
| auth.ts | Auth-related constants |
| layout.ts | LAYOUT dimensions (HEADER_HEIGHT, etc.) |
| modules.ts | Menu items configuration, module mapping |
| moduleMapping.ts | Module key ↔ remote name mapping |
| colors.ts | Color constants |
| errors.ts | Error messages |

#### Patterns ที่ใช้

- **2-Tier JWT Authentication:**
  - Tier 1: LoginJWT → ได้ menu permission (เห็นเมนูอะไรบ้าง)
  - Tier 2: QERPcMenuJWT → ได้ route-level permission (เข้าได้ไหม)
- **Module Federation:** Portal เป็น host, โหลด remote modules ผ่าน `RemoteWrappers.tsx`
- **Feature Flags:** `config/features.ts` เปิด/ปิด feature
- **RouteGuard:** ตรวจ permission ก่อนให้เข้า route
- **Context API:** AuthContext สำหรับ global auth state
- **Multi-company:** รองรับหลาย company ต่อ user

#### Dependencies กับ Module อื่น

- โหลดทุก remote module ผ่าน Module Federation
- ใช้ `@qerp/shared` สำหรับ types

---

### Module: Purchase Order

**Path:** `Q-ERPc/purchase/purchase-order/src/`
**Port:** 5002
**Remote Name:** `purchaseOrder`
**Files:** ~73 files
**Version:** 1.4.0
**Role:** จัดการใบสั่งซื้อ (PO) - สร้าง, แก้ไข, อนุมัติ, พิมพ์

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| POSearchFilter | POSearchFilter.tsx | Filter/Search สำหรับ PO list |
| POHeader | POHeader.tsx | Header section ของ PO form |
| POLineItem | POLineItem.tsx | รายการสินค้าใน PO |
| POSummary | POSummary.tsx | สรุปยอด (subtotal, VAT, total) |
| POApprovalStatus | POApprovalStatus.tsx | แสดงสถานะการอนุมัติ |
| EditableTable | EditableTable.tsx | Ant Design Table ที่แก้ไขได้ inline |
| PrintPreview | PrintPreview.tsx | Preview ก่อนพิมพ์ |
| VATCalculator | VATCalculator.tsx | คำนวณ VAT |
| FileUpload | FileUpload.tsx | อัพโหลดไฟล์แนบ |
| ApprovalHistory | ApprovalHistory.tsx | ประวัติการอนุมัติ |
| + 9 more | | components ย่อยอื่นๆ |

#### Hooks

| Hook | File | หน้าที่ |
|------|------|--------|
| usePOColumns | usePOColumns.tsx | คอลัมน์ตาราง PO list |
| usePOForm | usePOForm.tsx | Form state + validation |
| usePOLineItems | usePOLineItems.tsx | จัดการรายการสินค้า |
| usePOApproval | usePOApproval.tsx | Flow อนุมัติ |
| usePOPrint | usePOPrint.tsx | สั่งพิมพ์ |
| usePOSearch | usePOSearch.tsx | ค้นหา PO |
| usePODetail | usePODetail.tsx | โหลด PO detail |
| usePOCreate | usePOCreate.tsx | สร้าง PO ใหม่ |
| usePOEdit | usePOEdit.tsx | แก้ไข PO |
| useVATCalculation | useVATCalculation.tsx | คำนวณ VAT |
| + 8 more | | hooks ย่อยอื่นๆ |

#### Services

| Service | File | หน้าที่ |
|---------|------|--------|
| poService | poService.ts | CRUD operations สำหรับ PO |
| poLineItemService | poLineItemService.ts | CRUD สำหรับ line items |
| poApprovalService | poApprovalService.ts | Submit/Approve/Reject PO |
| poSearchService | poSearchService.ts | Search + Filter PO |
| poPrintService | poPrintService.ts | Generate print data |
| vendorService | vendorService.ts | ดึงข้อมูล vendor |
| productService | productService.ts | ดึงข้อมูลสินค้า |
| uploadService | uploadService.ts | Upload files |
| + 7 more | | services ย่อยอื่นๆ |

#### Pages

| Page | File | หน้าที่ |
|------|------|--------|
| POList | POList.tsx | หน้ารายการ PO (ค้นหา, filter, table) |
| PODetail | PODetail.tsx | หน้ารายละเอียด PO (สร้าง/แก้ไข/ดู) |
| POPrint | POPrint.tsx | หน้าพิมพ์ PO |

#### Key Business Logic

- **Multi-level Approval:** 5 ระดับการอนุมัติ
- **VAT Calculation:** คำนวณ VAT 7% อัตโนมัติ
- **Editable Line Items:** แก้ไข inline ในตาราง
- **Print Preview:** Preview + สั่งพิมพ์ได้
- **File Upload:** แนบไฟล์กับ PO

#### Patterns ที่ใช้

- **Service Pattern:** API calls อยู่ใน `services/` แยกจาก UI
- **Hook Pattern:** Business logic ทั้งหมดอยู่ใน `hooks/`
- **Store Pattern:** Global state ด้วย Zustand
- **Barrel Exports:** ทุก folder มี `index.ts`
- **Type-first:** Type definitions ใน `types/` แยกจาก components

#### Dependencies กับ Module อื่น

- ใช้ `@qerp/shared` (HttpClient, types, ConfirmModal)
- รับ `username`, `accessToken`, `companyCode` จาก Portal (commonProps)

---

### Module: Sales Order

**Path:** `Q-ERPc/sales/sales-order/src/`
**Port:** 5006
**Remote Name:** `salesOrder`
**Files:** ~104 files
**Role:** จัดการใบสั่งขาย (SO) - สร้าง, แก้ไข, อนุมัติ, พิมพ์

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| SOSearchFilter | SOSearchFilter.tsx | Filter/Search สำหรับ SO list |
| SOHeader | SOHeader.tsx | Header section ของ SO form |
| SOLineItem | SOLineItem.tsx | รายการสินค้าใน SO |
| SOSummary | SOSummary.tsx | สรุปยอด |
| SOApprovalStatus | SOApprovalStatus.tsx | สถานะอนุมัติ |
| EditableTable | EditableTable.tsx | Ant Design Table แก้ไข inline |
| PrintPreview | PrintPreview.tsx | Preview ก่อนพิมพ์ |
| CustomerInfo | CustomerInfo.tsx | ข้อมูลลูกค้า |
| + 15 more | | components ย่อยอื่นๆ |

#### Hooks (17 hooks)

- เหมือนรูปแบบ PO: `useSOColumns`, `useSOForm`, `useSOLineItems`, `useSOApproval`, `useSOPrint`, `useSOSearch`, `useSODetail`, `useSOCreate`, `useSOEdit`, etc.

#### Services (16 services)

- เหมือนรูปแบบ PO: `soService`, `soLineItemService`, `soApprovalService`, `soSearchService`, `soPrintService`, `customerService`, `productService`, etc.
- **26 API endpoints** (มากกว่า PO เพราะมี customer-related APIs เพิ่ม)

#### Pages

| Page | File | หน้าที่ |
|------|------|--------|
| SOList | SOList.tsx | หน้ารายการ SO |
| SODetail | SODetail.tsx | หน้ารายละเอียด SO |
| SOPrint | SOPrint.tsx | หน้าพิมพ์ SO |

#### Key Business Logic

- **เหมือน PO Module** ในเรื่อง structure และ patterns
- เพิ่ม Customer management (แทน Vendor)
- มี Sales-specific calculations

#### Patterns ที่ใช้

- เหมือน PO Module ทุกประการ (Service, Hook, Store, Barrel, Type-first)

#### Dependencies กับ Module อื่น

- ใช้ `@qerp/shared` (HttpClient, types, ConfirmModal)
- รับ `username`, `accessToken`, `companyCode`, `permission` จาก Portal

---

### Module: Sales Visitor

**Path:** `Q-ERPc/sales/sales-visitor/src/`
**Port:** 5001
**Remote Name:** `salesVisitor`
**Files:** ~16 files
**Role:** ระบบบันทึก Sales Visit (scaffold - ยังไม่เสร็จ)

#### สถานะ: Early Scaffold

- ใช้ **mock data** ยังไม่ต่อ API จริง
- โครงสร้างพื้นฐานมี components, hooks, types
- ยังไม่มี services ที่ต่อ backend

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| VisitorForm | VisitorForm.tsx | Form บันทึก visit |
| VisitorList | VisitorList.tsx | รายการ visits |
| VisitorCard | VisitorCard.tsx | Card แสดง visit info |

#### Patterns ที่ใช้

- เหมือน PO/SO แต่ยังไม่ implement ครบ
- Mock data อยู่ใน constants

---

### Module: Sales Analytics

**Path:** `Q-ERPc/analytics/sales-analytics/src/`
**Port:** 5005
**Remote Name:** `salesAnalytics`
**Files:** ~24 files
**Role:** Dashboard วิเคราะห์ยอดขาย (charts, tables)

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| Dashboard | Dashboard.tsx | หน้า dashboard หลัก |
| SalesChart | SalesChart.tsx | กราฟยอดขาย |
| YearSelector | YearSelector.tsx | เลือกปี (dynamic range จาก go-live date) |
| SearchTable | SearchTable.tsx | ตาราง search ข้อมูล |
| SummaryCards | SummaryCards.tsx | Cards สรุปตัวเลข |

#### Hooks

| Hook | File | หน้าที่ |
|------|------|--------|
| useDashboard | useDashboard.tsx | โหลดข้อมูล dashboard |
| useYearRange | useYearRange.tsx | คำนวณ year range |

#### Services

| Service | File | หน้าที่ |
|---------|------|--------|
| analyticsService | analyticsService.ts | API calls สำหรับ analytics data |

#### API Endpoints (4)

| Method | Endpoint | หน้าที่ |
|--------|----------|--------|
| GET | /api/sales-analytics/dashboard | ข้อมูล dashboard |
| GET | /api/sales-analytics/summary | สรุปยอดขาย |
| GET | /api/sales-analytics/chart | ข้อมูลกราฟ |
| GET | /api/sales-analytics/search | ค้นหาข้อมูล |

#### Patterns ที่ใช้

- Service + Hook pattern (เหมือน modules อื่น)
- Dynamic year range จาก go-live date (register version)
- Zustand สำหรับ state

---

### Module: Dashboard

**Path:** `general/dashboard/src/`
**Port:** 5003
**Remote Name:** `dashboard`
**Files:** ~6 files
**Role:** หน้า Landing Page (Carousel)

#### สถานะ: Minimal

- แสดง Carousel สำหรับหน้า home
- ไม่มี business logic ซับซ้อน

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| DashboardPage | DashboardPage.tsx | หน้า carousel landing page |

---

### Module: Business Data Monitoring

**Path:** `business-data-monitoring/src/`
**Port:** 5004
**Remote Name:** `businessDataMonitoring`
**Files:** ~9 files
**Role:** Monitor ข้อมูลธุรกิจ (stub)

#### สถานะ: Stub / Placeholder

- มี 4 placeholder routes
- ยังไม่ implement จริง

#### Pages (stubs)

| Page | Route | หน้าที่ |
|------|-------|--------|
| Dashboard | /dashboard | (stub) |
| Reports | /dashboard/reports | (stub) |
| Settings | /dashboard/settings | (stub) |
| Analytics | /dashboard/analytics | (stub) |

---

### Module: Shared (@qerp/shared)

**Path:** `shared/src/`
**Package:** `@qerp/shared`
**Files:** ~7 files
**Role:** Shared library ใช้ร่วมทุก module

#### Services

| Service | File | หน้าที่ |
|---------|------|--------|
| HttpClient | httpClient.ts | Axios wrapper (interceptors, token, error handling) |

#### Components

| Component | File | หน้าที่ |
|-----------|------|--------|
| ConfirmModal | ConfirmModal.tsx | Modal ยืนยัน (ใช้ร่วมทุก module) |

#### Types (12+ interfaces)

| Type | หน้าที่ |
|------|--------|
| ApiResponse<T> | Generic API response wrapper |
| PaginatedResponse<T> | Paginated list response |
| LoginRequest / LoginResponse | Auth request/response |
| Permission | User permissions |
| MenuPermission | Menu-level permissions |
| Company | Company info |
| UserInfo | User information |
| ErrorResponse | API error format |
| และอื่นๆ | |

#### Exports

```typescript
// Entry points
"." → "./src/index.ts"           // ทุกอย่าง
"./services" → "./src/services/index.ts"  // HttpClient
"./types" → "./src/types/index.ts"        // Types only
```

#### Dependencies กับ Module อื่น

- **ทุก module** import จาก `@qerp/shared`
- HttpClient ถูกใช้เป็น base สำหรับทุก service

---

### Module: Scripts (Build System)

**Path:** `scripts/`
**Files:** 4 files
**Role:** Central build/dev orchestration

#### Files

| File | หน้าที่ |
|------|--------|
| config.js | 🔥 Central config - servers, modules, ports ทุกอย่างอยู่ที่นี่ |
| dev.js | Dev server runner (interactive mode, เปลี่ยน API URL อัตโนมัติ) |
| build.js | Production build (สร้าง .env → build → copy ไป deploy/) |
| generate-config.js | สร้าง vite.config.ts จาก config.js |

#### Servers (จาก config.js)

| Key | Name | API URL | ใช้เมื่อ |
|-----|------|---------|---------|
| local | Local | https://localhost:7199 | Dev local |
| server | Server | http://192.168.0.131:1003 | Dev server |
| production | Production | http://192.168.0.131:1003 | Production deploy |
| cloud | Cloud | http://203.150.53.240:2007 | Cloud deploy |
| lertvilai | Lertvilai | http://10.20.0.230:1001 | Customer deploy |
| yawata | Yawata | http://192.168.1.251:1001 | Customer deploy |

#### Module Registry (จาก config.js)

| Key | Name | Dir | Port | Remote Name |
|-----|------|-----|------|-------------|
| portal | Portal (Host) | portal | 5000 | - (host) |
| sv | Sales Visitor | Q-ERPc/sales/sales-visitor | 5001 | salesVisitor |
| po | Purchase Order | Q-ERPc/purchase/purchase-order | 5002 | purchaseOrder |
| dashboard | Dashboard | general/dashboard | 5003 | dashboard |
| businessData | Business Data | business-data-monitoring | 5004 | businessDataMonitoring |
| sa | Sales Analytics | Q-ERPc/analytics/sales-analytics | 5005 | salesAnalytics |
| so | Sales Order | Q-ERPc/sales/sales-order | 5006 | salesOrder |
| qai | Q-AI Chat | C:/GitHub/qai_react (external) | 3000 | qai |

---

## Existing Components (รวมทุก module)

### Layout Components (Portal)

- MainLayout, MainHeader, AppSidebar, PageTitleBar

### Auth Components (Portal)

- ProtectedRoute, PublicRoute, RouteGuard, CompanySelector

### Utility Components (Portal + Shared)

- ErrorBoundary, RemoteWrappers (6 wrappers), ConfirmModal

### Business Components (PO/SO)

- SearchFilter, Header, LineItem, Summary, ApprovalStatus
- EditableTable, PrintPreview, FileUpload, ApprovalHistory, VATCalculator

### Analytics Components (SA)

- Dashboard, SalesChart, YearSelector, SearchTable, SummaryCards

---

## Code Conventions

### Naming

| Type | Pattern | Example |
|------|---------|---------|
| Component | PascalCase | `POSearchFilter.tsx` |
| Hook | camelCase + "use" | `usePOColumns.tsx` |
| Service | camelCase + "Service" | `poService.ts` |
| Type | PascalCase | `POHeader` |
| Constant file | camelCase | `routes.ts` |
| CSS Module | Component.module.css | `Main.module.css` |

### Patterns

- **Service Pattern:** API calls ใน `services/` → export functions ที่ return Promise
- **Hook Pattern:** Business logic ใน `hooks/` → เรียก services + จัดการ state
- **Store Pattern:** Global state ด้วย Zustand (remote modules)
- **Context Pattern:** AuthContext (portal only)
- **Barrel Exports:** ทุก folder มี `index.ts`
- **Type-first:** สร้าง types ก่อน → ใช้ใน services → ใช้ใน hooks → ใช้ใน components

### File Structure (ทุก remote module)

```
src/
├── components/     # UI Components
│   └── index.ts    # Barrel export
├── hooks/          # Custom hooks (business logic)
│   └── index.ts
├── services/       # API calls
│   └── index.ts
├── types/          # TypeScript interfaces
│   └── index.ts
├── pages/          # Page components
│   └── index.ts
├── store/          # Zustand stores
├── constants/      # Constants
└── App.tsx         # Module entry point (exposed via federation)
```

### Language Convention

- **UI Text:** Thai (ทุก label, message, tooltip)
- **Code:** English (variable names, function names, comments)

---

## Routes / Pages

| Route | Module | Component | หน้าที่ |
|-------|--------|-----------|--------|
| `/` | Portal | → redirect | Redirect ไป home |
| `/home` | Dashboard | DashboardPageWrapper | หน้า landing (carousel) |
| `/purchase/purchase-order/*` | Purchase Order | PurchaseOrderPageWrapper | จัดการ PO |
| `/purchase/purchase-order/` | PO | POList | รายการ PO |
| `/purchase/purchase-order/:id` | PO | PODetail | รายละเอียด PO |
| `/purchase/purchase-order/:id/print` | PO | POPrint | พิมพ์ PO |
| `/sales/sales-order/*` | Sales Order | SalesOrderPageWrapper | จัดการ SO |
| `/sales/sales-order/` | SO | SOList | รายการ SO |
| `/sales/sales-order/:id` | SO | SODetail | รายละเอียด SO |
| `/sales/sales-order/:id/print` | SO | SOPrint | พิมพ์ SO |
| `/sales/sales-visitor/*` | Sales Visitor | SalesVisitorPageWrapper | บันทึก visit |
| `/analytics/sales-analytics/*` | Sales Analytics | SalesAnalyticsPageWrapper | Dashboard ยอดขาย |
| `/dashboard/*` | Business Data | BusinessDataMonitoringPageWrapper | Monitor ข้อมูล |
| `/qai/*` | Q-AI Chat | QaiPageWrapper | AI Chat (external module) |
| `/unauthorized` | Portal | Unauthorized | ไม่มีสิทธิ์ |

---

## API Endpoints (สรุปทุก module — 53 endpoints)

> Scanned จาก codebase จริง (2026-02-05)

### Auth & Permission (Portal)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| POST | `/api/Login/LoginJWT` | authService.ts | Login (ได้ Tier 1 JWT + menu items) |
| POST | `/api/JWT/QERPcMenuJWT` | authService.ts | ขอ menu permission สำหรับ company ที่เลือก (Tier 2 JWT) |
| GET | `/api/JWT/QERPcMenuActionJWT/{moduleCode}` | permissionService.ts | ขอ action-level permission (Tier 3 — insert/edit/print) |

> Module codes ที่ใช้: `PO`, `SO`, `ANALYSIS_SO`

### Purchase Order (24 endpoints)

#### Core PO Operations

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/PO/POHeaderList` | poService.ts | รายการ PO (paginated, search, filter by DocumentTypeCode) |
| POST | `/api/PO/POInsert` | poService.ts | สร้าง PO ใหม่ |
| GET | `/api/PO/POOrder` | poService.ts | ดึง PO detail สำหรับแก้ไข |
| POST | `/api/PO/POUpdate` | poService.ts | อัพเดท PO |
| POST | `/api/PO/POCancel` | poService.ts | ยกเลิก PO |
| POST | `/api/PO/CheckStatus` | poService.ts | ตรวจ status ก่อน edit/cancel |

#### PO Master Data

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/Supplier/SupplierList` | supplierService.ts | รายการ suppliers (paginated, search) |
| GET | `/api/Supplier/GetSupplier` | supplierService.ts | รายละเอียด supplier ตาม code |
| GET | `/api/Item/ItemList` | itemService.ts | รายการสินค้า (paginated, search) |
| GET | `/api/ItemUnit/UnitConversionList` | itemService.ts | แปลงหน่วยสินค้า |
| GET | `/api/PaymentTerm/PaymentTermList` | paymentTermService.ts | เงื่อนไขการชำระเงิน |
| GET | `/api/PaymentTerm/CalculatePayment` | paymentTermService.ts | คำนวณวันครบกำหนดชำระ |
| GET | `/api/Currency/GetCurrency` | currencyService.ts | รายการสกุลเงิน |
| GET | `/api/Currency/GetExchangeRatePurchase` | currencyService.ts | อัตราแลกเปลี่ยน (ซื้อ) |
| GET | `/api/Warehouse/GetListWarehouse` | warehouseService.ts | รายการคลังสินค้า |
| GET | `/api/Company/ComapyInfo` | companyService.ts | ข้อมูลบริษัท + noDigit settings |
| GET | `/api/Document/DocumentTypeRightList` | documentService.ts | ประเภทเอกสารที่มีสิทธิ์ |
| GET | `/api/Serie/SeriesAndGroupDoc` | serieService.ts | เลขที่เอกสาร running number + series |

#### PO Approval, Calculation & Report

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| POST | `/api/Calculate/CalculateVatAmount` | calculateService.ts | คำนวณ VAT |
| POST | `/api/Approved/Approve` | approvalService.ts | อนุมัติ/ปฏิเสธ |
| GET | `/api/Approved/Config/PO` | approvedConfigService.ts | ตั้งค่าระดับอนุมัติ PO |
| GET | `/api/Report/PrintFormList` | printFormService.ts | รายการฟอร์มพิมพ์ตามประเภทเอกสาร |
| POST | `/api/Report/POReportPDF` | printFormService.ts | สร้าง PO report เป็น PDF (Blob) |
| GET | `/api/JWT/QERPcMenuActionJWT/PO` | permissionService.ts | Permission ระดับ action (insert/edit/print) |

### Sales Order (28 endpoints)

#### Core SO Operations

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/SO/SOHeaderList` | soService.ts | รายการ SO (paginated, search, filter) |
| POST | `/api/SO/SOInsert` | soService.ts | สร้าง SO ใหม่ |
| GET | `/api/SO/SOOrder` | soService.ts | ดึง SO detail สำหรับแก้ไข |
| POST | `/api/SO/SOUpdate` | soService.ts | อัพเดท SO |
| POST | `/api/SO/SOCancel` | soService.ts | ยกเลิก SO |
| POST | `/api/SO/CheckStatus` | soService.ts | ตรวจ status ก่อน edit/cancel |

#### SO Master Data (เฉพาะ SO — นอกจากนี้ใช้ร่วมกับ PO)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/Customer/CustomerList` | customerService.ts | รายการลูกค้า (paginated, search) |
| GET | `/api/Customer/GetCustomer` | customerService.ts | รายละเอียดลูกค้าตาม code |
| GET | `/api/Salesman/SalesmanList` | salesmanService.ts | รายการพนักงานขาย (paginated, search) |
| GET | `/api/Salesman/GetSalesman` | salesmanService.ts | รายละเอียดพนักงานขาย |
| GET | `/api/Transportation/TransportationList` | transportationService.ts | รายการวิธีขนส่ง (paginated) |
| GET | `/api/Transportation/GetTransportation` | transportationService.ts | รายละเอียดขนส่งตาม code |

#### SO Shared Master Data (ใช้ร่วมกับ PO)

> Item, ItemUnit, PaymentTerm, Currency, Warehouse, Company, Document, Serie — endpoint เดียวกับ PO

#### SO Approval, Calculation & Report

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| POST | `/api/Calculate/CalculateVatAmount` | calculateService.ts | คำนวณ VAT |
| POST | `/api/Approved/Approve` | approvalService.ts | อนุมัติ/ปฏิเสธ |
| GET | `/api/Approved/Config/SO` | approvedConfigService.ts | ตั้งค่าระดับอนุมัติ SO |
| GET | `/api/Report/PrintFormList` | printFormService.ts | รายการฟอร์มพิมพ์ |
| POST | `/api/Report/SOReportPDF` | printFormService.ts | สร้าง SO report เป็น PDF (Blob) |
| GET | `/api/JWT/QERPcMenuActionJWT/SO` | permissionService.ts | Permission ระดับ action |

### Sales Analytics (4 endpoints)

| Method | Endpoint | Service | หน้าที่ |
|--------|----------|---------|--------|
| GET | `/api/Company/ComapyGoLive` | dashboardService.ts | วันที่บริษัท Go-Live (ใช้คำนวณ year range) |
| GET | `/api/PivotSO/SOSummary` | dashboardService.ts | สรุปยอดขายตามปี |
| GET | `/api/PivotSO/SONotComplete` | dashboardService.ts | SO ที่ยังไม่เสร็จ (paginated) |
| GET | `/api/JWT/QERPcMenuActionJWT/ANALYSIS_SO` | permissionService.ts | Permission ระดับ action |

### Sales Visitor — ยังไม่มี API (scaffold, ใช้ mock data)

### Business Data Monitoring — ยังไม่มี API (stub pages)

### API Response Convention

```
code: 0 = success → ใช้ response.result
code: non-0 = error → แสดง response.msg
```

### Blob Endpoints (PDF Download)

| Endpoint | Module |
|----------|--------|
| `/api/Report/POReportPDF` | PO |
| `/api/Report/SOReportPDF` | SO |

---

## Environment Variables

| Variable | ใช้ทำอะไร | Required | ตั้งค่าโดย |
|----------|----------|----------|-----------|
| VITE_API_BASE_URL | API base URL | Yes | scripts/dev.js (auto) |
| VITE_IIS_BASE_URL | IIS base URL สำหรับ federation remotes | Yes | scripts/dev.js (auto) |
| VITE_APP_VERSION | App version (cache busting) | No | scripts/build.js |

> **Note:** `.env` ถูกสร้างอัตโนมัติโดย `scripts/dev.js` - ไม่ต้องแก้มือ

---

## Architecture: Module Federation

```
┌─────────────────────────────────────────────────┐
│                  Portal (Host)                   │
│                  Port: 5000                      │
│  ┌──────────┐  ┌──────────┐  ┌───────────────┐  │
│  │ Auth     │  │ Router   │  │ RemoteWrappers│  │
│  │ Context  │  │ (Main)   │  │ (Lazy Load)   │  │
│  └──────────┘  └──────────┘  └───────────────┘  │
└──────────┬──────────┬──────────┬────────────────┘
           │          │          │
    ┌──────▼───┐ ┌────▼────┐ ┌──▼──────────┐
    │ PO :5002 │ │ SO :5006│ │ SA :5005    │
    │ Module   │ │ Module  │ │ Module      │
    └──────────┘ └─────────┘ └─────────────┘
    ┌──────────┐ ┌─────────┐ ┌─────────────┐
    │ SV :5001 │ │ DB :5003│ │ BDM :5004   │
    │ Module   │ │ Module  │ │ Module      │
    └──────────┘ └─────────┘ └─────────────┘
    ┌──────────┐
    │QAI :3000 │  (External)
    │ Module   │
    └──────────┘

    ┌──────────────────────────────┐
    │     @qerp/shared library     │
    │  HttpClient | Types | Modal  │
    └──────────────────────────────┘
```

### Data Flow: Host → Remote

```
Portal (Host)
  │
  ├─ commonProps = { username, accessToken, companyCode }
  │
  ├─ <PurchaseOrderPageWrapper {...commonProps} permission={permission} />
  ├─ <SalesOrderPageWrapper {...commonProps} permission={permission} />
  ├─ <SalesVisitorPageWrapper {...commonProps} permission={permission} />
  ├─ <SalesAnalyticsPageWrapper {...commonProps} />
  ├─ <BusinessDataMonitoringPageWrapper {...commonProps} />
  ├─ <DashboardPageWrapper {...commonProps} />
  └─ <QaiPageWrapper {...commonProps} />
```

### Auth Flow (3-Tier JWT)

```
User Login
  │
  ▼
POST /api/Login/LoginJWT
  │
  ▼
LoginJWT (Tier 1)  ──→  ได้ menu items (เห็นเมนูอะไรบ้าง)
  │
  ▼
POST /api/JWT/QERPcMenuJWT (companyCode)
  │
  ▼
QERPcMenuJWT (Tier 2)  ──→  ได้ route-level permission
  │
  ▼
RouteGuard  ──→  ตรวจ permission ก่อนให้เข้า route
  │
  ▼
GET /api/JWT/QERPcMenuActionJWT/{MODULE}
  │
  ▼
ActionJWT (Tier 3)  ──→  ได้ action permission (insert/edit/print)
```

---

## For Each Role

### PM Should Know

- **Existing features:** PO, SO, Sales Visitor (scaffold), Sales Analytics, Dashboard, Business Data (stub)
- **Multi-company:** รองรับหลาย company ต่อ user
- **Approval workflow:** PO/SO มี 5-level approval
- **External module:** QAI Chat อยู่คนละ repo
- **Modules ที่ยังไม่เสร็จ:** Sales Visitor (mock data), Business Data (stub)

### Designer Should Know

- **UI Library:** Ant Design 6 (Thai locale)
- **Icons:** @ant-design/icons 6
- **Styling:** CSS Modules (Component.module.css)
- **Layout:** Sidebar + Header + Content (responsive, mobile support)
- **Existing components ที่ reuse ได้:** EditableTable, SearchFilter, PrintPreview, ConfirmModal, CompanySelector, PageTitleBar
- **Color system:** ดูที่ `portal/src/constants/colors.ts`

### Developer Should Know

- **Architecture:** Micro-Frontend (Module Federation) + Host/Remote pattern
- **State management:** Zustand (remote modules), Context API (portal auth)
- **API layer:** Service Pattern → `@qerp/shared` HttpClient (Axios)
- **Shared library:** `@qerp/shared` - ต้อง import types/services จากที่นี่
- **Code conventions:** Service → Hook → Component, Barrel exports, Type-first
- **เพิ่ม module ใหม่:** แก้ `scripts/config.js` → รัน `generate-config.js` → เพิ่ม type declaration + route
- **PO/SO เป็น reference:** module ใหม่ที่เป็น CRUD ควรดู PO/SO เป็นตัวอย่าง

### QA Should Know

- **Test framework:** ไม่มี test setup ในปัจจุบัน (ไม่มี test files)
- **Manual testing:** ต้อง test ผ่าน browser
- **Dev server:** `npm run dev:server` แล้วเปิด http://localhost:5000
- **Multi-company testing:** ต้อง test หลาย company
- **Approval flow:** PO/SO มี 5-level ต้อง test ทุก level

### DevOps Should Know

- **Build:** `node scripts/build.js {target}` (cloud, production, lertvilai, yawata)
- **Deploy target:** IIS Server (Windows)
- **Output:** `deploy/output-{target}/` (มี web.config สำหรับ IIS)
- **Servers:** 4 deployment targets (production, cloud, lertvilai, yawata)
- **CI/CD:** ไม่มี automated CI/CD (manual build + deploy)
- **ENV:** สร้างอัตโนมัติโดย scripts - ไม่ต้อง manage มือ
- **Backend:** C# .NET (separate repo), SQL Server

---

## Code Patterns (with Examples)

> Section นี้แสดง code จริงจาก project เพื่อให้ agent เขียนโค้ดตรง pattern ได้ทันที

### Pattern 1: Type Definition

ไฟล์ type อยู่ใน `types/` แยก 1 ไฟล์ต่อ 1 entity, barrel export ผ่าน `index.ts`

```typescript
// types/poHeader.ts
export interface POHeader {
  documentModuleCode: string
  documentTypeCode: string
  runNo: number
  yyear: number
  pono: string
  podate: string
  supplierCode: string
  supplierName: string
  // ... approval levels, amounts, audit fields
  approvalStatuses: ApprovalStatus[]
}

// types/index.ts (barrel export)
export * from './poHeader'
export * from './supplier'
export * from './item'
export * from './approval'
// ... export ทุกไฟล์
```

---

### Pattern 2: HttpClient (จาก @qerp/shared)

ทุก module สร้าง httpClient instance จาก shared library เหมือนกันหมด:

```typescript
// services/httpClient.ts (ทุก module ใช้ไฟล์เดียวกัน)
import { HttpClient, createHttpClient } from '@qerp/shared/services'
import type { ApiConfig, RequestOptions } from '@qerp/shared/services'

export type { ApiConfig, RequestOptions }
export { HttpClient }

export const httpClient = createHttpClient({
  baseUrl: import.meta.env.VITE_API_BASE_URL || '',
  defaultToken: import.meta.env.VITE_API_TOKEN_BEARER || '',
  defaultPackage: import.meta.env.VITE_API_DEFAULT_PACKAGE || '',
})
```

**HttpClient API:**

```typescript
httpClient.get<T>(endpoint, { accessToken, packageCode, params })
httpClient.post<T>(endpoint, body, { accessToken, packageCode })
httpClient.put<T>(endpoint, body, { accessToken, packageCode })
httpClient.delete<T>(endpoint, { accessToken, packageCode })
httpClient.postBlob(endpoint, body, { accessToken, packageCode })
```

- `accessToken` → ใส่ใน header `Authorization: Bearer {token}`
- `packageCode` → ใส่ใน header `X-PACKAGE: {companyCode}`
- return `response.data` (unwrapped จาก Axios)

---

### Pattern 3: Service

Service เป็น async functions ที่รับ `accessToken` + `packageCode` เสมอ, export ทั้ง individual functions และ named object:

```typescript
// services/poService.ts
import { httpClient } from './httpClient'
import type { POHeaderListResponse, POInsertRequest, POInsertResponse } from '../types'

export async function getPOHeaderList(
  documentTypeCode: string,
  page: number,
  pageSize: number,
  search: string | undefined,
  accessToken: string,
  packageCode: string
): Promise<POHeaderListResponse> {
  const params: Record<string, string | number | boolean> = {
    DocumentTypeCode: documentTypeCode, page, pageSize,
  }
  if (search) { params.search = search }
  return httpClient.get<POHeaderListResponse>('/api/PO/POHeaderList', {
    accessToken, packageCode, params,
  })
}

export async function poInsert(
  request: POInsertRequest,
  accessToken: string,
  packageCode: string
): Promise<POInsertResponse> {
  return httpClient.post<POInsertResponse>('/api/PO/POInsert', request, {
    accessToken, packageCode,
  })
}

// Export as named object
export const poService = { getPOHeaderList, poInsert, /* ... */ }
```

**สำคัญ:** API response ใช้ `code: 0` = success, `code: non-0` = error

```typescript
// ตรวจ response
if (response.code === 0) {
  // success - ใช้ response.result
} else {
  // error - แสดง response.msg
}
```

---

### Pattern 4: Zustand Store

แต่ละ module มี 2 stores: `authStore` (เหมือนกันทุก module) และ `xxStore` (เฉพาะ module)

```typescript
// stores/authStore.ts (เหมือนกันทุก module - copy ได้เลย)
import { create } from 'zustand'

interface AuthState {
  username: string
  accessToken: string
  companyCode: string
  permission: Permission | null
  actionPermission: ActionPermission | null
  actionAccessToken: string | null
  canInsert: boolean
  canEdit: boolean
  canPrint: boolean
  setAuth: (auth: Partial<AuthState>) => void
  setActionPermission: (ap: ActionPermission | null, token?: string | null) => void
  reset: () => void
}

export const useAuthStore = create<AuthState>((set) => ({
  username: '', accessToken: '', companyCode: '',
  permission: null, actionPermission: null, actionAccessToken: null,
  canInsert: false, canEdit: false, canPrint: false,

  setAuth: (auth) => set((state) => ({
    ...state,
    username: auth.username ?? state.username,
    accessToken: auth.accessToken ?? state.accessToken,
    companyCode: auth.companyCode ?? state.companyCode,
    permission: auth.permission !== undefined ? auth.permission : state.permission,
  })),

  setActionPermission: (actionPermission, actionAccessToken) => set({
    actionPermission,
    actionAccessToken: actionAccessToken ?? null,
    canInsert: actionPermission?.insert === 'Y',
    canEdit: actionPermission?.edit === 'Y',
    canPrint: actionPermission?.print === 'Y',
  }),

  reset: () => set({ /* initial state */ }),
}))
```

```typescript
// stores/poStore.ts (เฉพาะ module)
import { create } from 'zustand'

interface POState {
  documentTypes: DocumentType[]
  selectedDocumentTypeCode: string | undefined
  poHeaders: POHeader[]
  isLoadingPOHeaders: boolean
  pagination: PaginationState
  searchText: string
  // Actions
  setPOHeaders: (headers: POHeader[]) => void
  setIsLoadingPOHeaders: (loading: boolean) => void
  // ... setters สำหรับทุก field
}

export const usePOStore = create<POState>((set) => ({ /* ... */ }))

// Selector hooks (ใช้แทน direct access เพื่อ performance)
export const useDocumentTypes = () => usePOStore((state) => state.documentTypes)
export const useSelectedDocumentType = () => usePOStore((state) => state.selectedDocumentTypeCode)
export const usePOHeaders = () => usePOStore((state) => state.poHeaders)
export const usePagination = () => usePOStore((state) => state.pagination)
```

**สำคัญ:** ทุก module ฟัง logout event จาก Portal:

```typescript
if (typeof window !== 'undefined') {
  window.addEventListener('qerp:logout', () => {
    usePOStore.getState().reset()
  })
}
```

---

### Pattern 5: Hook (Business Logic)

Hooks อยู่ใน `hooks/` แยกตามหน้าที่ ไม่เรียก service ตรงจาก component

```typescript
// hooks/usePOListData.ts
export function usePOListData() {
  const { actionAccessToken, companyCode } = useAuthStore()
  const poHeaders = usePOHeaders()
  const pagination = usePagination()
  const { setPOHeaders, setIsLoadingPOHeaders, setPagination } = usePOStore()

  const fetchPOHeaders = useCallback(async (
    documentTypeCode: string, page: number, pageSize: number, search?: string
  ) => {
    if (!actionAccessToken || !companyCode) return
    setIsLoadingPOHeaders(true)
    try {
      const response = await getPOHeaderList(
        documentTypeCode, page, pageSize, search,
        actionAccessToken, companyCode
      )
      if (response.code === 0) {
        setPOHeaders(response.result || [])
        setPagination({ total: response.totalCount, current: page, pageSize })
      }
    } catch (error) {
      handleApiError(error)
    } finally {
      setIsLoadingPOHeaders(false)
    }
  }, [actionAccessToken, companyCode])

  return { poHeaders, pagination, fetchPOHeaders, /* ... */ }
}
```

**Composition Hook** (รวม sub-hooks):

```typescript
// hooks/usePOFormData.ts
export function usePOFormData({ form, isEditMode, id, poDate }) {
  const { username, actionAccessToken, companyCode } = useAuthStore()

  // Compose sub-hooks
  const { paymentTerms, currencies, warehouses, companyInfo } = useMasterData()
  const { serieInfo, isLoading: isLoadingSerie } = useSerieInfo({ form, isEditMode, poDate })
  const { isEditDataLoaded } = usePOEditData({ form, isEditMode, id, warehouses, setLineItems })

  const [lineItems, setLineItems] = useState<POLineItem[]>([
    { key: '1', noLine: 1, vline: 1, transactionCode: '', quantity: 0, /* ... */ statusRow: 'N' },
  ])

  return {
    username, actionAccessToken, companyCode,
    paymentTerms, currencies, warehouses, companyInfo,
    serieInfo, isLoadingSerie,
    lineItems, setLineItems, isEditDataLoaded,
  }
}
```

**Convention สำคัญใน Hooks:**
- ใช้ `useCallback` สำหรับทุก handler function
- ใช้ `useMemo` สำหรับทุก computed value
- ใช้ `useRef` ป้องกัน duplicate API calls (`hasFetchedDocTypes`, `prevAuthRef`)

---

### Pattern 6: App.tsx (Remote Module Entry)

ทุก remote module มี App.tsx โครงสร้างเหมือนกัน:

```typescript
// App.tsx
const MODULE_CODE = 'PO'  // เปลี่ยนตาม module

interface AppProps {
  username?: string
  accessToken?: string
  companyCode?: string
  permission?: Permission | null
}

function PurchaseOrderContent() {
  const { canInsert, canEdit } = usePermission()
  return <PurchaseOrderUI canInsert={canInsert} canEdit={canEdit} />
}

function PurchaseOrderUI({ canInsert, canEdit }: { canInsert: boolean; canEdit: boolean }) {
  return (
    <div style={{ width: '100%' }}>
      <Routes>
        <Route index element={<POList canInsert={canInsert} canEdit={canEdit} />} />
        <Route path="create" element={<POForm canEdit={canInsert} />} />
        <Route path="edit/:id" element={<POForm canEdit={canEdit} />} />
      </Routes>
    </div>
  )
}

function App({ username, accessToken, companyCode, permission }: AppProps = {}) {
  const setAuth = useAuthStore((state) => state.setAuth)
  const prevAuthRef = useRef<string | null>(null)

  // Sync Portal props → Zustand store (เฉพาะเมื่อเปลี่ยนจริง)
  useEffect(() => {
    const authKey = `${username}|${accessToken}|${companyCode}|${JSON.stringify(permission)}`
    if (prevAuthRef.current !== authKey) {
      prevAuthRef.current = authKey
      setAuth({ username, accessToken, companyCode, permission })
    }
  }, [username, accessToken, companyCode, permission, setAuth])

  if (!accessToken || !companyCode) return <PurchaseOrderUI />

  return (
    <PermissionProvider moduleCode={MODULE_CODE} accessToken={accessToken}
      companyCode={companyCode} permission={permission}>
      <PurchaseOrderContent />
    </PermissionProvider>
  )
}

export default App
```

**Token Flow ทั้งระบบ:**

```
Portal AuthContext (Tier 1+2 JWT)
  │
  ├─ props: { username, accessToken(T2), companyCode, permission }
  │
  ▼
Remote App.tsx
  │
  ├─ Sync to Zustand authStore
  ├─ PermissionProvider calls /api/JWT/QERPcMenuActionJWT/{MODULE}
  │   → ได้ accessToken(T3) + actionPermission (insert/edit/print)
  │
  ▼
Hooks อ่าน T3 จาก authStore
  │
  ▼
Services ใช้ T3 เรียก API: httpClient.get('/api/XX/...', { accessToken: T3, packageCode })
```

---

### Pattern 7: Page (List Page)

```typescript
// pages/POList.tsx
export function POList({ canInsert, canEdit }: POListProps) {
  const navigate = useNavigate()
  const [visibleColumns, setVisibleColumns] = useState<string[]>(loadVisibleColumns)
  const [cancelModalOpen, setCancelModalOpen] = useState(false)

  // Hooks (business logic)
  const { documentTypeOptions, poHeaders, pagination, fetchPOHeaders } = usePOListData()
  const { configuredLevels, actionsByLevel } = useApprovedConfig()
  const checkStatusModal = useCheckStatusModal({ onCancelProceed: (po) => { /* ... */ } })
  const printModal = usePrintModal()
  const approvalModal = useApprovalModal({ onApprovalAction: handleApprovalAction })
  const columns = usePOColumns({ onEdit, onView, onCancel, onPrint, /* ... */ })

  return (
    <Card>
      <Flex justify="space-between">
        <Title level={4}>ใบสั่งซื้อ</Title>
        {canInsert && <Button type="primary" onClick={() => navigate('create')}>สร้างใบสั่งซื้อ</Button>}
      </Flex>

      <POSearchFilter /* ... */ />

      <Table
        columns={columns}
        dataSource={poHeaders}
        pagination={pagination}
        /* ... */
      />

      {/* Modals */}
      <CheckStatusModal /* ... */ />
      <ConfirmModal /* ... */ />
      <PrintFormSelectModal /* ... */ />
    </Card>
  )
}
```

---

## Blueprint: สร้าง Module ใหม่ (PO/SO เป็น Template)

> PO กับ SO มี code ซ้ำกัน ~80% ต่างกันแค่ชื่อ entity, API path, และ domain-specific fields
> Module ใหม่ที่เป็น CRUD ให้ใช้ PO/SO เป็นต้นแบบ

### ไฟล์ที่ Copy ได้เลย (ไม่ต้องแก้)

| ไฟล์ | หน้าที่ |
|------|--------|
| `services/httpClient.ts` | HttpClient instance |
| `stores/authStore.ts` | Auth state |
| `contexts/PermissionContext.tsx` | Permission provider |
| Shared types: `approval.ts`, `calculate.ts`, `company.ts`, `currency.ts`, `documentType.ts`, `item.ts`, `paymentTerm.ts`, `permission.ts`, `printForm.ts`, `serie.ts`, `warehouse.ts` | Infrastructure types |
| Shared services: `approvalService.ts`, `calculateService.ts`, `companyService.ts`, `currencyService.ts`, `documentService.ts`, `paymentTermService.ts`, `permissionService.ts`, `printFormService.ts`, `serieService.ts`, `warehouseService.ts` | Infrastructure services |
| Shared hooks: `useMasterData.ts`, `useSerieInfo.ts`, `useVATCalculation.ts`, `useApprovedConfig.ts`, `useDeleteLineValidation.ts`, `useCheckStatusModal.ts`, `usePrintModal.ts`, `useApprovalModal.ts`, `usePermission.ts`, `useDocumentTypes.ts` | Infrastructure hooks |
| Shared components: `ApprovalStatusTag.tsx`, `CheckStatusModal.tsx`, `ColumnSelector.tsx`, `EditableDiscountCell.tsx`, `EditableNumberCell.tsx`, `ErrorModal.tsx`, `ItemSearchModal.tsx`, `PrintFormSelectModal.tsx`, `RejectReasonModal.tsx`, `SaveStatusModal.tsx` | Infrastructure UI |

### ไฟล์ที่ต้อง Find-and-Replace

| สิ่งที่ต้องเปลี่ยน | PO | SO | Module ใหม่ (XX) |
|-------------------|----|----|-----------------|
| Module code | `'PO'` | `'SO'` | `'XX'` |
| API path | `/api/PO/` | `/api/SO/` | `/api/XX/` |
| Header type | `POHeader` | `SOHeader` | `XXHeader` |
| Order type | `POOrder` | `SOOrder` | `XXOrder` |
| Detail type | `PODetail` | `SODetail` | `XXDetail` |
| Store name | `usePOStore` | `useSOStore` | `useXXStore` |
| Entity type | `Supplier` | `Customer` | (domain entity) |
| Entity service | `supplierService` | `customerService` | (domain service) |
| Form data hook | `usePOFormData` | `useSOFormData` | `useXXFormData` |
| List data hook | `usePOListData` | `useSOListData` | `useXXListData` |
| Columns hook | `usePOColumns` | `useSOColumns` | `useXXColumns` |
| Submit hook | `usePOFormSubmit` | `useSOFormSubmit` | `useXXFormSubmit` |
| Unit field | `purchaseUnitCode` | `salesUnitCode` | (domain field) |
| Thai label | `ใบสั่งซื้อ` | `ใบสั่งขาย` | (Thai name) |
| Storage key | `po-list-visible-columns` | `so-list-visible-columns` | `xx-list-visible-columns` |

### ไฟล์ที่ต้องเขียนใหม่ (domain-specific)

| ไฟล์ | ทำไม |
|------|------|
| `types/xxHeader.ts` | Field เฉพาะ domain (เช่น SO มี customerCode, PO มี supplierCode) |
| `types/xxOrder.ts` | Detail line item fields ต่างกัน |
| `types/{entity}.ts` | Entity เฉพาะ (Customer, Supplier, etc.) |
| `services/xxService.ts` | API endpoints เฉพาะ |
| `services/{entity}Service.ts` | Entity API เฉพาะ |
| `hooks/useXXColumns.tsx` | คอลัมน์ตารางต่างกัน |
| `components/{Entity}Section.tsx` | UI เฉพาะ entity |

### ขั้นตอนสร้าง Module ใหม่

```
1. เพิ่มใน scripts/config.js → modules object
2. รัน node scripts/generate-config.js
3. Copy โครงสร้างจาก PO (หรือ SO)
4. Find-and-replace ตามตาราง
5. เขียน domain-specific files (header type, entity, columns)
6. เพิ่ม type declaration ใน portal/src/vite-env.d.ts
7. เพิ่ม RemoteWrapper ใน portal/src/components/RemoteWrappers.tsx
8. เพิ่ม Route ใน portal/src/pages/Main.tsx
9. เพิ่ม menu item ใน portal/src/constants/modules.ts
```

---

## Notes / Technical Debt

1. **ไม่มี Test:** ไม่มี test framework หรือ test files ในทุก module
2. **Sales Visitor ยัง scaffold:** ใช้ mock data, ยังไม่ต่อ API จริง
3. **Business Data ยัง stub:** มีแค่ placeholder pages
4. **Dashboard minimal:** แค่ carousel landing page
5. **ไม่มี CI/CD:** Build + deploy ต้องทำ manual
6. **QAI อยู่คนละ repo:** `C:/GitHub/qai_react` - external module
7. **Backend อยู่คนละ repo:** C# .NET - ไม่อยู่ใน scan scope
8. **PO/SO code ซ้ำกันมาก:** มี pattern เหมือนกัน อาจ extract shared logic ได้
