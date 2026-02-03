# Design Specs: Phase 2 - Reading Experience & UX Features

> Designer: @Designer | Date: 2026-02-01

---

## Overview

ออกแบบ 6 features สำหรับปรับปรุง Reading Experience และ UX
โปรเจคใช้ **Tailwind CSS + shadcn/ui** มี dark theme variables พร้อมอยู่แล้ว

---

## 1. Dark Mode Toggle (US-007)

### Component: ThemeToggle

```
+------------------+
|  [Sun/Moon Icon] |  <- ปุ่มกลม หรือ icon button
+------------------+
```

### Layout & Position
- **ตำแหน่ง**: Header ด้านขวา (ก่อน Mobile menu)
- **Desktop**: แสดงเป็น icon button
- **Mobile**: แสดงเป็น icon button (เหมือน desktop)

### Specs

| Property | Value |
|----------|-------|
| Size | 40x40px (icon 20x20px) |
| Border Radius | 9999px (rounded-full) |
| Background | transparent (ghost button) |
| Hover | bg-accent |

### States & Icons
| State | Icon | Color |
|-------|------|-------|
| Light Mode | `Sun` (lucide) | text-foreground |
| Dark Mode | `Moon` (lucide) | text-foreground |
| Hover | - | bg-accent |

### Animation
- Icon rotation: 180deg เมื่อเปลี่ยน theme
- Duration: 200ms
- Easing: ease-in-out

### Behavior
1. คลิกเพื่อ toggle ระหว่าง light/dark
2. ตรวจสอบ `prefers-color-scheme` ตอน first load
3. เก็บค่าใน `localStorage` key: `theme`
4. เพิ่ม class `dark` ที่ `<html>` element

### Wireframe (Header)
```
+----------------------------------------------------------+
|  MyBlog              Home    About    [Theme] [Mobile]   |
+----------------------------------------------------------+
                                           ^
                                    ThemeToggle Button
```

---

## 2. Reading Progress Bar (US-005)

### Component: ReadingProgress

```
+============================================--------------+
|████████████████████████████                              |
+----------------------------------------------------------+
^ 0%                                                   100% ^
```

### Layout & Position
- **ตำแหน่ง**: Fixed top (ใต้ header หรือ บนสุดของหน้า)
- **Width**: 100vw
- **Height**: 3px
- **Z-index**: 50 (เท่ากับ header)

### Specs

| Property | Light Mode | Dark Mode |
|----------|------------|-----------|
| Background (track) | transparent | transparent |
| Progress Color | primary (oklch 0.205) | primary (oklch 0.922) |
| Height | 3px | 3px |

### Animation
- Smooth width transition
- Duration: 50ms (real-time feel)

### Behavior
1. แสดงเฉพาะหน้า Post Detail
2. คำนวณ % จาก scroll position / (document height - viewport height)
3. Progress bar width = scroll percentage

### Responsive
- ทุก breakpoint: เหมือนกัน (full width)

---

## 3. Reading Time (US-006)

### Component: ReadingTime

```
+------------------+
|  Clock  5 min read |
+------------------+
```

### Layout & Position

**หน้า Home (PostCard)**:
```
+----------------------------------+
|  [Image]                         |
|  Title                           |
|  Feb 1, 2026  •  5 min read      |  <- ต่อจาก date
|  Excerpt...                      |
+----------------------------------+
```

**หน้า Post Detail**:
```
+------------------------------------------+
|  Title                                   |
|  Author  •  Feb 1, 2026  •  5 min read   |
+------------------------------------------+
```

### Specs

| Property | Value |
|----------|-------|
| Font Size | text-sm (14px) |
| Color | text-muted-foreground |
| Icon | `Clock` (lucide) 14x14px |
| Icon Gap | 4px (gap-1) |

### Calculation
- Average reading speed: 200 words/minute
- Formula: `Math.ceil(wordCount / 200)`
- แสดงเป็น "X min read"

---

## 4. Back to Top Button (US-008)

### Component: BackToTop

```
      +-------+
      |   ^   |
      | Arrow |
      +-------+
```

### Layout & Position
- **ตำแหน่ง**: Fixed bottom-right
- **Offset**: right: 24px, bottom: 24px
- **Mobile**: right: 16px, bottom: 16px

### Specs

| Property | Value |
|----------|-------|
| Size | 44x44px (touch target) |
| Border Radius | rounded-full |
| Background | bg-primary |
| Icon Color | text-primary-foreground |
| Icon | `ChevronUp` or `ArrowUp` (lucide) 24x24px |
| Shadow | shadow-lg |

### States

| State | Style |
|-------|-------|
| Default | bg-primary, shadow-lg |
| Hover | bg-primary/90, scale(1.05) |
| Active | scale(0.95) |
| Hidden | opacity-0, pointer-events-none |

### Animation
- **Show/Hide**: Fade + scale
- **Duration**: 200ms
- **Trigger**: แสดงเมื่อ scroll > 300px

### Behavior
1. ซ่อนตอน scroll อยู่ด้านบน (< 300px)
2. แสดงเมื่อ scroll ลงมา > 300px
3. คลิกแล้ว smooth scroll to top
4. `scrollBehavior: 'smooth'`

---

## 5. Copy Code Button (US-009)

### Component: CopyButton (ใน CodeBlock)

```
+----------------------------------------+
| javascript                    [Copy]   |
+----------------------------------------+
| const hello = "world";                 |
| console.log(hello);                    |
+----------------------------------------+
```

### Layout & Position
- **ตำแหน่ง**: มุมขวาบนของ code block
- **Offset**: top: 8px, right: 8px
- **Position**: absolute (parent = relative)

### Specs

| Property | Value |
|----------|-------|
| Size | 32x32px |
| Border Radius | rounded-md |
| Background | bg-secondary |
| Icon | `Copy` / `Check` (lucide) 16x16px |
| Icon Color | text-muted-foreground |

### States

| State | Icon | Background | Duration |
|-------|------|------------|----------|
| Default | `Copy` | bg-secondary | - |
| Hover | `Copy` | bg-secondary/80 | - |
| Copied | `Check` | bg-green-500/20 | 2000ms |

### Animation
- Icon swap: fade transition
- Duration: 150ms

### Behavior
1. คลิก → copy code to clipboard
2. เปลี่ยน icon เป็น Check + สีเขียว
3. 2 วินาทีแล้วกลับเป็น Copy icon
4. ใช้ `navigator.clipboard.writeText()`

### Code Block Container
```css
/* Wrapper */
.code-block {
  position: relative;
  border-radius: var(--radius);
  overflow: hidden;
}
```

---

## 6. Search (US-010)

### Component: SearchDialog

**Trigger Button (Header)**:
```
+------------------+
|  Search...  ⌘K  |
+------------------+
```

**Search Dialog**:
```
+------------------------------------------+
|  [Search Icon] Search posts...           |
+------------------------------------------+
|                                          |
|  Results:                                |
|  +------------------------------------+  |
|  | Title 1                            |  |
|  | Excerpt preview...                 |  |
|  +------------------------------------+  |
|  | Title 2                            |  |
|  | Excerpt preview...                 |  |
|  +------------------------------------+  |
|                                          |
|  No results found.                       |
+------------------------------------------+
```

### Layout & Position

**Trigger Button**:
- **Desktop**: Header, ก่อน ThemeToggle
- **Mobile**: Icon only ใน header

**Dialog**:
- **Position**: Fixed center
- **Width**: max-w-lg (512px)
- **Max Height**: 60vh

### Trigger Button Specs

| Property | Desktop | Mobile |
|----------|---------|--------|
| Width | 200px | 40px (icon only) |
| Height | 40px | 40px |
| Background | bg-secondary | transparent |
| Border Radius | rounded-md | rounded-full |
| Text | "Search..." + "⌘K" | Search icon only |

### Dialog Specs

| Property | Value |
|----------|-------|
| Background | bg-background |
| Border | border |
| Border Radius | rounded-lg |
| Shadow | shadow-xl |
| Backdrop | bg-black/50 |

### Input Specs

| Property | Value |
|----------|-------|
| Height | 48px |
| Font Size | text-lg |
| Icon | `Search` (lucide) 20x20px |
| Placeholder | "Search posts..." |

### Result Item Specs

| Property | Value |
|----------|-------|
| Padding | p-3 |
| Border Bottom | border-b |
| Hover | bg-accent |
| Title | text-base, font-medium |
| Excerpt | text-sm, text-muted-foreground, line-clamp-1 |

### Animation
- **Open**: Fade in + scale from 95%
- **Close**: Fade out + scale to 95%
- **Duration**: 150ms

### Behavior
1. กด trigger หรือ `⌘K` / `Ctrl+K` เพื่อเปิด
2. พิมพ์แล้ว filter แบบ debounce (300ms)
3. ค้นหาจาก title และ excerpt
4. คลิกผลลัพธ์ → navigate ไปหน้า post
5. กด `Esc` หรือคลิก backdrop เพื่อปิด

### Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `⌘K` / `Ctrl+K` | Open search |
| `Esc` | Close search |
| `↑` / `↓` | Navigate results |
| `Enter` | Go to selected result |

---

## Component Summary

| Component | File | Priority |
|-----------|------|----------|
| ThemeToggle | `components/ThemeToggle.tsx` | 1 |
| ReadingProgress | `components/ReadingProgress.tsx` | 2 |
| ReadingTime | `components/ReadingTime.tsx` | 3 |
| BackToTop | `components/BackToTop.tsx` | 4 |
| CopyButton | `components/CopyButton.tsx` | 5 |
| SearchDialog | `components/SearchDialog.tsx` | 6 |

---

## Dependencies ที่ต้องติดตั้ง

```bash
npm install next-themes  # สำหรับ Dark Mode
```

---

## Responsive Breakpoints

| Breakpoint | Width | Changes |
|------------|-------|---------|
| Mobile | < 640px | Search = icon only, smaller offsets |
| Tablet | 640-1024px | Same as desktop |
| Desktop | > 1024px | Full search trigger |

---

## Accessibility Checklist

- [x] Color contrast >= 4.5:1 (ใช้ shadcn defaults)
- [ ] Focus states visible (ทุก interactive element)
- [ ] Keyboard navigable (Search, Theme toggle)
- [ ] Touch targets >= 44px (Back to Top, Theme toggle)
- [ ] Screen reader labels (aria-label)

---

## Handoff Checklist (Designer → Developer)

- [x] Layout specs ครบทุก component
- [x] Colors ใช้ CSS variables ที่มีอยู่
- [x] Typography specs
- [x] States ครบ (default, hover, active)
- [x] Responsive behavior
- [x] Animation specs
- [x] Keyboard shortcuts (Search)
- [x] Dependencies listed

---

*Ready for Development*
