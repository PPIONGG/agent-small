# Sales Analytics Revamp

> Created: 2026-02-04
> Owner: @PM
> Status: Design
> Module: `Q-ERPc/analytics/sales-analytics/`

---

## Overview

ปรับปรุง Sales Analytics Dashboard ให้ข้อมูลเพียงพอสำหรับผู้บริหาร พร้อม redesign UI ให้สวยงามและใช้งานง่ายขึ้น

### เป้าหมาย

1. **ข้อมูลครบถ้วน** - เพิ่ม KPI ที่ขาด (AOV, Growth, Top Customers, Top Products)
2. **Comparison ได้** - เทียบ YoY, เห็น trend ชัดเจน
3. **UI/UX ดีขึ้น** - ใช้ chart library จริง, layout สวยงาม, responsive
4. **Export ได้** - ส่งรายงานให้ผู้บริหารได้

---

## Current State (สถานะปัจจุบัน)

### มีอยู่แล้ว
- 4 Stat Cards: ยอดขายรวม, จำนวน SO, ยอดปกติ, ยอดยกเลิก
- Horizontal Bar Chart (custom CSS): รายเดือน / รายไตรมาส
- ตาราง SO Not Complete: search + pagination
- Year selector, Refresh button
- Permission system, Auth store

### API ที่มีอยู่
| Endpoint | ข้อมูล |
|----------|--------|
| `GET /api/Company/ComapyGoLive` | วันที่เริ่มใช้งาน (สร้าง year range) |
| `GET /api/PivotSO/SOSummary?year=` | ยอดรวม, จำนวน SO, ปกติ/ยกเลิก, รายเดือน, รายไตรมาส |
| `GET /api/PivotSO/SONotComplete?year=&page=&pageSize=&search=` | รายการ SO ที่ยังไม่เสร็จ |

---

## Proposed Features (แบ่งเป็น Phase)

### Phase 1: เพิ่มข้อมูลที่ขาด + ปรับ UI (Priority: 🔴 High)

#### F1.1 - ปรับปรุง Stat Cards

**ปัจจุบัน:** 4 cards แสดงตัวเลขอย่างเดียว
**เปลี่ยนเป็น:** 4 cards พร้อม trend indicator

| Card | ข้อมูลหลัก | เพิ่มใหม่ |
|------|-----------|----------|
| ยอดขายรวม | ฿ amount | +/- % เทียบปีก่อน (YoY), sparkline mini chart |
| จำนวน SO | จำนวน | +/- % เทียบปีก่อน |
| ยอดเฉลี่ยต่อใบ (AOV) | **ใหม่** ยอดรวม / จำนวน SO | +/- % เทียบปีก่อน |
| อัตราสำเร็จ | **ใหม่** % ปกติ vs ยกเลิก | Progress ring แสดงสัดส่วน |

> **Note:** ย้าย "ยอดปกติ" และ "ยอดยกเลิก" ไปรวมเป็น metric ใน card "อัตราสำเร็จ" แทน เพราะแสดงเป็น % ให้ insight มากกว่า

**Acceptance Criteria:**
- [ ] แสดง 4 cards ตาม design ใหม่
- [ ] YoY % มีลูกศรขึ้น/ลง สีเขียว/แดง
- [ ] AOV คำนวณจาก totalAmount / soDocQuantity
- [ ] อัตราสำเร็จแสดงเป็น % พร้อม Progress ring
- [ ] Loading ใช้ Skeleton แทน Spin

#### F1.2 - ใช้ Chart Library แทน Custom CSS

**ปัจจุบัน:** Horizontal bar chart ทำจาก div + CSS
**เปลี่ยนเป็น:** ใช้ `@ant-design/charts` (Column chart)

**Chart ที่ต้องมี:**
1. **Column Chart (main)** - ยอดขายรายเดือน/รายไตรมาส
   - Tooltip แสดงรายละเอียดเมื่อ hover
   - Animation เมื่อ load/เปลี่ยนข้อมูล
   - สลับ เดือน/ไตรมาส ได้ (Segmented - มีอยู่แล้ว)

2. **Donut Chart (secondary)** - สัดส่วนยอดปกติ vs ยกเลิก
   - แสดง % ตรงกลาง
   - Legend ด้านล่าง

**Acceptance Criteria:**
- [ ] ติดตั้ง `@ant-design/charts`
- [ ] Column chart แสดงข้อมูลรายเดือน/ไตรมาส
- [ ] Donut chart แสดงสัดส่วนปกติ/ยกเลิก
- [ ] Charts มี tooltip, animation, responsive
- [ ] ลบ custom CSS bar chart ออก

#### F1.3 - Redesign Layout (2-Column Grid)

**Layout ใหม่:**

```
┌──────────────────────────────────────────────────────┐
│ Header: "ภาพรวมยอดใบสั่งขาย" | วันที่ | ปี | Refresh │
├──────────────────────────────────────────────────────┤
│ [Card 1]     [Card 2]     [Card 3]     [Card 4]     │  ← Row 1: KPI Cards
├──────────────────────────────────────────────────────┤
│ [Column Chart: ยอดขายรายเดือน]   │ [Donut: สัดส่วน]  │  ← Row 2: Charts
│ (Col: 16)                        │ (Col: 8)          │
├──────────────────────────────────────────────────────┤
│ [Table: SO ยังไม่เสร็จ + search + pagination]        │  ← Row 3: Detail
└──────────────────────────────────────────────────────┘
```

**Responsive:**
- Desktop (>1200px): 4 cards, charts 2 คอลัมน์
- Tablet (768-1200px): 2 cards/row, charts stack
- Mobile (<768px): 1 card/row, charts stack

**Acceptance Criteria:**
- [ ] Layout ตาม wireframe
- [ ] ใช้ Ant Design Row/Col กับ gutter={[16, 16]}
- [ ] Responsive ทุก breakpoint
- [ ] Card height เท่ากันในแต่ละ row
- [ ] Spacing สม่ำเสมอ (16px gap)

---

### Phase 2: เพิ่ม Ranking + Filter (Priority: 🟡 Medium)

#### F2.1 - Top Customers / Top Products

**เพิ่ม Row ใหม่ระหว่าง Charts กับ Table:**

```
├──────────────────────────────────────────────────────┤
│ [Top 5 Customers by Revenue]  │ [Top 5 Products]     │  ← Row 3: Rankings
│ (Horizontal Bar)              │ (Horizontal Bar)      │
├──────────────────────────────────────────────────────┤
```

**ข้อมูลที่ต้องการ:**
- Top 5 ลูกค้ายอดขายสูงสุด (ชื่อ + ยอดเงิน + % ของยอดรวม)
- Top 5 สินค้ายอดขายสูงสุด (ชื่อ + ยอดเงิน + % ของยอดรวม)

**API ที่ต้องเพิ่ม (Backend):**
| Method | Endpoint | Response |
|--------|----------|----------|
| GET | `/api/PivotSO/SOTopCustomers?year=&top=5` | `[{ customerName, totalAmount, percentage }]` |
| GET | `/api/PivotSO/SOTopProducts?year=&top=5` | `[{ productName, totalAmount, percentage }]` |

**Acceptance Criteria:**
- [ ] แสดง Top 5 Customers (Horizontal bar chart)
- [ ] แสดง Top 5 Products (Horizontal bar chart)
- [ ] แต่ละ bar แสดง % ของยอดรวม
- [ ] Click ที่ customer/product → filter ตาราง (optional)

#### F2.2 - เพิ่ม Filter ขั้นสูง

**เพิ่ม filter ใน header area:**

| Filter | Component | ข้อมูล |
|--------|-----------|--------|
| Date Range | `DatePicker.RangePicker` | เลือกช่วงวันที่แทนแค่ปี |
| สถานะ | `Select` | ปกติ / ยกเลิก / รอดำเนินการ |
| Quick Presets | Buttons | เดือนนี้ / ไตรมาสนี้ / ปีนี้ / ปีก่อน |

**API ที่ต้องปรับ (Backend):**
- เพิ่ม params: `dateFrom`, `dateTo`, `status` ใน SOSummary และ SONotComplete

**Acceptance Criteria:**
- [ ] Date range picker ทำงานได้
- [ ] Quick presets (เดือนนี้, ไตรมาสนี้, ปีนี้)
- [ ] Filter status ในตาราง
- [ ] ปุ่ม "ล้าง filter" (reset ทั้งหมด)
- [ ] Filter มีผลกับทุก section (cards, charts, table)

---

### Phase 3: Export + Comparison (Priority: 🟢 Nice to Have)

#### F3.1 - Export Data

| Feature | Format | วิธี |
|---------|--------|------|
| Export ตาราง | Excel (.xlsx) | ใช้ library `xlsx` |
| Export Dashboard | PDF | ใช้ `html2canvas` + `jsPDF` |
| Export Chart | PNG | ใช้ `@ant-design/charts` built-in `downloadImage()` |

**Acceptance Criteria:**
- [ ] ปุ่ม Export Excel ใน table header
- [ ] ปุ่ม Export PDF สำหรับ dashboard ทั้งหน้า
- [ ] Export มีข้อมูล filter context (ปี, ช่วงวัน)
- [ ] Excel export ส่งข้อมูลทุกหน้า (ไม่ใช่แค่หน้าปัจจุบัน)

#### F3.2 - YoY Comparison Chart

**เพิ่ม option ใน Column Chart:**
- Toggle "เทียบปีก่อน" → แสดง 2 สีบน chart เดียวกัน
- ปีปัจจุบัน: สีน้ำเงินเข้ม
- ปีก่อน: สีน้ำเงินอ่อน (ซ้อนกัน)

**API ที่ต้องเพิ่ม (Backend):**
| Method | Endpoint | Response |
|--------|----------|----------|
| GET | `/api/PivotSO/SOSummaryCompare?year=&compareYear=` | SOSummary ของ 2 ปี |

**Acceptance Criteria:**
- [ ] Toggle เทียบปีก่อนได้
- [ ] Grouped bar chart แสดง 2 ปีเทียบกัน
- [ ] Tooltip แสดง % เปลี่ยนแปลง
- [ ] Stat cards อัพเดท YoY % ตาม data จริง

---

## Design Specifications (สำหรับ Designer)

### Color Palette

| Usage | Color | Hex |
|-------|-------|-----|
| Primary Blue | ยอดขายรวม, main chart | #3b82f6 |
| Success Green | อัตราสำเร็จ, trend ขึ้น | #22c55e |
| Warning Orange | AOV, pending status | #f59e0b |
| Danger Red | trend ลง, cancelled | #ef4444 |
| Neutral | text, borders | #64748b |
| Background | page bg | #f8fafc |
| Card bg | card background | #ffffff |

### Typography

| Element | Size | Weight | Color |
|---------|------|--------|-------|
| Page title | 20px | 600 | #1e293b |
| Card value | 28px | 700 | #1e293b |
| Card label | 14px | 400 | #64748b |
| Trend indicator | 12px | 500 | green/red |
| Table text | 14px | 400 | #334155 |

### Spacing

| Element | Value |
|---------|-------|
| Card padding | 24px |
| Gap between cards | 16px |
| Section gap (rows) | 24px |
| Page padding | 24px |

### Component Library

- Charts: `@ant-design/charts` (Column, Pie/Ring, Bar)
- UI: Ant Design 6 (Card, Statistic, Skeleton, Row, Col, Segmented, Table)
- Icons: `@ant-design/icons`

---

## API Requirements Summary (สำหรับ Backend)

### API ที่มีอยู่แล้ว (ไม่ต้องแก้)
- `GET /api/Company/ComapyGoLive`
- `GET /api/PivotSO/SOSummary?year=`
- `GET /api/PivotSO/SONotComplete?year=&page=&pageSize=&search=`

### API ที่ต้องเพิ่ม

| Phase | Method | Endpoint | Params | Response |
|-------|--------|----------|--------|----------|
| 1 | GET | `/api/PivotSO/SOSummary` | เพิ่ม `compareYear` (optional) | เพิ่ม previousYear data สำหรับ YoY % |
| 2 | GET | `/api/PivotSO/SOTopCustomers` | `year`, `top` | `[{ customerName, totalAmount, percentage }]` |
| 2 | GET | `/api/PivotSO/SOTopProducts` | `year`, `top` | `[{ productName, totalAmount, percentage }]` |
| 2 | - | ปรับ SOSummary, SONotComplete | เพิ่ม `dateFrom`, `dateTo`, `status` | เดิม + filter |
| 3 | GET | `/api/PivotSO/SOSummaryCompare` | `year`, `compareYear` | SOSummary ของ 2 ปี |

---

## Component Breakdown (สำหรับ Developer)

### Components ที่ต้องสร้างใหม่

| Component | หน้าที่ |
|-----------|--------|
| `StatCard` | Reusable KPI card (value, label, trend, icon) |
| `TrendIndicator` | ลูกศรขึ้น/ลง + % เปลี่ยนแปลง |
| `SalesColumnChart` | Column chart (เดือน/ไตรมาส) ใช้ @ant-design/charts |
| `StatusDonutChart` | Donut chart สัดส่วนปกติ/ยกเลิก |
| `TopRankingChart` | Horizontal bar สำหรับ Top Customers/Products (Phase 2) |
| `DashboardFilters` | Filter bar (year, date range, status) (Phase 2) |
| `ExportToolbar` | ปุ่ม Export Excel/PDF (Phase 3) |

### Hooks ที่ต้องปรับ/เพิ่ม

| Hook | เปลี่ยนแปลง |
|------|------------|
| `useDashboard` | เพิ่ม AOV calculation, fetch previous year สำหรับ YoY |
| `useTopRanking` | ใหม่ - fetch Top Customers/Products (Phase 2) |
| `useExport` | ใหม่ - handle Excel/PDF export (Phase 3) |

---

## Phases & Workflow

| Phase | Owner | ส่งต่อ | Dependencies |
|-------|-------|--------|-------------|
| Phase 1: Cards + Charts + Layout | @Designer → @Developer | @QA | ไม่มี (ใช้ API เดิม + คำนวณ frontend) |
| Phase 2: Rankings + Filters | @PM specs → @Developer | @QA | ต้อง Backend เพิ่ม API |
| Phase 3: Export + YoY Compare | @Developer | @QA | ต้อง Backend เพิ่ม API |

---

## Notes

- Phase 1 ส่วนใหญ่ทำได้เลยโดยไม่ต้องรอ Backend (คำนวณ AOV จากข้อมูลเดิม, YoY % ใช้ fetch 2 ปีจาก API เดิม)
- `@ant-design/charts` ต้องเช็ค compatibility กับ React 19 ก่อน
- ถ้า `@ant-design/charts` ไม่รองรับ React 19 ให้ใช้ `@ant-design/plots` หรือ `recharts` แทน
