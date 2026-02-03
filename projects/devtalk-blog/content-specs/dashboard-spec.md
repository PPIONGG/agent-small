# Dashboard Spec: Blog Statistics

**Task**: สร้างหน้า Dashboard แสดงสถิติ Blog
**Owner**: @Designer → @Developer
**Priority**: 🟡 Medium
**Created by**: @PM
**Date**: 2026-02-01

---

## Overview

สร้างหน้า `/dashboard` ที่แสดงสถิติของ blog posts โดยเฉพาะการวิเคราะห์ tags เพื่อดูว่าเขียนเรื่อง tech stack อะไรบ่อยที่สุด

---

## Navigation Update

เพิ่ม Dashboard ใน main navigation:

```
🏠 Home  |  👤 About  |  📊 Dashboard
```

**File to update**: `src/config/site.ts`
```typescript
navItems: [
  { href: "/", label: "Home", icon: "Home" as const },
  { href: "/about", label: "About", icon: "User" as const },
  { href: "/dashboard", label: "Dashboard", icon: "BarChart2" as const },
],
```

---

## Page Structure

### URL
`/dashboard`

### Layout

```
┌──────────────────────────────────────────────────────┐
│  📊 DevTalk Dashboard                                │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │  📝 5   │ │  🏷️ 12  │ │  📂 3   │ │ 📅 Feb 1│    │
│  │ Posts   │ │ Tags    │ │Category │ │ Latest  │    │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘    │
│                                                      │
│  📈 Tech Stack Popularity          📂 By Category   │
│  ┌─────────────────────────┐  ┌─────────────────┐   │
│  │ React     ████████  4   │  │   [Pie Chart]   │   │
│  │ Next.js   ██████    3   │  │                 │   │
│  │ TypeScript████      2   │  │ Dev: 60%        │   │
│  │ Tailwind  ██        1   │  │ Frontend: 20%  │   │
│  │ Git       ██        1   │  │ CSS: 20%       │   │
│  └─────────────────────────┘  └─────────────────┘   │
│                                                      │
│  🏷️ All Tags                                        │
│  ┌──────────────────────────────────────────────┐   │
│  │ React(4) Next.js(3) TypeScript(2) Git(2)     │   │
│  │ Tailwind(1) CSS(1) JavaScript(1) ...         │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
│  📝 Recent Posts                                    │
│  ┌──────────────────────────────────────────────┐   │
│  │ • Ant Design คู่มือ...           Feb 1       │   │
│  │ • Conventional Commits...        Feb 1       │   │
│  │ • TypeScript สำหรับ React...     Jan 25      │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## Components

### 1. StatCard
แสดงตัวเลขสถิติแบบ card

```tsx
interface StatCardProps {
  icon: React.ReactNode;
  label: string;
  value: string | number;
}
```

**Stats to show:**
- Total Posts
- Total Tags (unique)
- Total Categories (unique)
- Latest Post Date

### 2. TagChart (Bar Chart)
แสดง tag popularity เรียงจากมากไปน้อย

```tsx
interface TagChartProps {
  data: Array<{ tag: string; count: number }>;
  limit?: number; // default 10
}
```

**Implementation options:**
- Option A: Pure CSS bars (no library) - แนะนำ
- Option B: recharts library
- Option C: chart.js

### 3. CategoryPieChart
แสดงสัดส่วน posts ต่อ category

```tsx
interface CategoryPieChartProps {
  data: Array<{ category: string; count: number }>;
}
```

**Implementation:**
- CSS-based pie chart หรือ
- Simple percentage bars (fallback)

### 4. TagCloud
แสดง tags ทั้งหมดแบบ cloud

```tsx
interface TagCloudProps {
  tags: Array<{ tag: string; count: number }>;
}
```

**Features:**
- ขนาด font ตาม count
- Click ได้ (filter posts by tag - future)

### 5. RecentPostsList
แสดง posts ล่าสุด

```tsx
interface RecentPostsListProps {
  posts: Post[];
  limit?: number; // default 5
}
```

---

## Data Calculation

### Helper Functions (src/lib/stats.ts)

```typescript
// นับ tags ทั้งหมด
function getTagStats(posts: Post[]): TagStat[] {
  // Return: [{ tag: "React", count: 4 }, ...]
}

// นับ categories
function getCategoryStats(posts: Post[]): CategoryStat[] {
  // Return: [{ category: "Development", count: 3 }, ...]
}

// Overview stats
function getOverviewStats(posts: Post[]): OverviewStats {
  // Return: { totalPosts, uniqueTags, uniqueCategories, latestPostDate }
}
```

---

## Design Specs

### Colors (ใช้ DevTalk brand colors)
- Primary: #4F7CFF (blue)
- Chart bars: gradient from #4F7CFF to #93B4FF
- Background cards: white / dark:gray-800
- Text: gray-900 / dark:gray-100

### Responsive
- **Desktop**: 2 columns for charts
- **Mobile**: 1 column, stacked

### Dark Mode
- รองรับ dark mode ตาม theme ปัจจุบัน

---

## Files to Create

| File | Type | Description |
|------|------|-------------|
| `src/app/dashboard/page.tsx` | Page | Dashboard page |
| `src/lib/stats.ts` | Library | Stats calculation |
| `src/components/dashboard/StatCard.tsx` | Component | Stat card |
| `src/components/dashboard/TagChart.tsx` | Component | Bar chart |
| `src/components/dashboard/CategoryChart.tsx` | Component | Pie/bar chart |
| `src/components/dashboard/TagCloud.tsx` | Component | Tag cloud |
| `src/components/dashboard/RecentPosts.tsx` | Component | Recent posts |

---

## Acceptance Criteria

- [ ] หน้า `/dashboard` เข้าถึงได้
- [ ] Navigation มี Dashboard link
- [ ] แสดง Overview Stats (4 cards)
- [ ] แสดง Tag Popularity Chart
- [ ] แสดง Category Distribution
- [ ] แสดง Tag Cloud
- [ ] แสดง Recent Posts
- [ ] Responsive (mobile/desktop)
- [ ] Dark mode support
- [ ] Build ผ่าน ไม่มี errors

---

## Priority Order

1. **Must Have (MVP)**
   - Overview Stats
   - Tag Popularity (list/bar)
   - Navigation link

2. **Should Have**
   - Category Chart
   - Recent Posts
   - Tag Cloud

3. **Nice to Have**
   - Animated charts
   - Click to filter

---

*Created by @PM | 2026-02-01*
