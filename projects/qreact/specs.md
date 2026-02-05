# Specs - QReact (Q-ERP)

> Last updated: 2026-02-05

---

## Existing Features (Implemented)

### 1. Authentication & Authorization

- 3-Tier JWT authentication (Login → Menu → Action)
- Multi-company support (เลือก company หลัง login)
- Route-level permission (RouteGuard)
- Action-level permission (insert/edit/print per module)

### 2. Purchase Order (PO)

- CRUD: สร้าง, แก้ไข, ยกเลิก PO
- 5-Level Approval workflow
- Editable line items (inline editing)
- VAT 7% calculation
- Print preview + PDF export
- File upload
- Search + Filter by document type
- Column visibility customization

### 3. Sales Order (SO)

- CRUD: สร้าง, แก้ไข, ยกเลิก SO
- 5-Level Approval workflow
- Customer, Salesman, Transportation management
- เหมือน PO ในเรื่อง line items, VAT, print, approval

### 4. Sales Analytics

- Dashboard สรุปยอดขาย (ตามปี)
- Dynamic year range จาก go-live date
- SO ที่ยังไม่เสร็จ (paginated)

### 5. Dashboard

- Carousel landing page

### 6. Portal (Host)

- Sidebar + Header layout (responsive)
- Module Federation host
- Company selector
- Feature flags

---

## Pending Features (Not Implemented)

### Sales Visitor

- สถานะ: Scaffold (mock data)
- ต้องทำ: ต่อ API จริง, implement CRUD

### Business Data Monitoring

- สถานะ: Stub (placeholder pages)
- ต้องทำ: implement ทุกหน้า

---

## Specs สำหรับ Features ใหม่

_(รอ PM สร้าง specs)_
