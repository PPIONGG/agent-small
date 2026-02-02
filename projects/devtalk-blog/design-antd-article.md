# Design Specs: บทความ Ant Design (Antd)

## Overview
บทความแนะนำ Ant Design สำหรับมือใหม่ ออกแบบให้อ่านง่าย มี code examples ที่ copy ได้

---

## Page Layout

```
+--------------------------------------------------+
|  Header (existing)                               |
+--------------------------------------------------+
|                                                  |
|  📌 Breadcrumb: Home > Posts > Ant Design Guide  |
|                                                  |
|  +--------------------------------------------+  |
|  |  🏷️ Category Badge: "Frontend"            |  |
|  |                                            |  |
|  |  # Ant Design (Antd) คู่มือเริ่มต้น        |  |
|  |     สำหรับมือใหม่                          |  |
|  |                                            |  |
|  |  📅 1 Feb 2026  •  👤 Author  •  ⏱️ 10 min |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  📑 Table of Contents (Sticky on Desktop)  |  |
|  |  1. Antd คืออะไร?                          |  |
|  |  2. Installation                           |  |
|  |  3. Basic Components                       |  |
|  |  4. Customization                          |  |
|  |  5. เปรียบเทียบ                            |  |
|  |  6. สรุป                                   |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | CONTENT SECTIONS                           |  |
|  |                                            |  |
|  | [Section 1: Intro]                         |  |
|  | - ข้อความอธิบาย                            |  |
|  | - Info box: ข้อดีหลัก 3 ข้อ                |  |
|  |                                            |  |
|  | [Section 2: Installation]                  |  |
|  | - Step-by-step                             |  |
|  | - Code block with copy button              |  |
|  |                                            |  |
|  | [Section 3: Basic Components]              |  |
|  | - Component cards with examples            |  |
|  | - Live code snippets                       |  |
|  |                                            |  |
|  | [Section 4: Customization]                 |  |
|  | - Theme config example                     |  |
|  |                                            |  |
|  | [Section 5: Comparison Table]              |  |
|  | - Antd vs shadcn/ui vs MUI                 |  |
|  |                                            |  |
|  | [Section 6: Summary]                       |  |
|  | - Key takeaways                            |  |
|  | - When to use Antd                         |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  💡 Tips Box (highlighted)                 |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  🏷️ Tags: antd, react, ui-library          |  |
|  +--------------------------------------------+  |
|                                                  |
+--------------------------------------------------+
|  Footer (existing)                               |
+--------------------------------------------------+
```

---

## Component Specs

### 1. Article Header
```
Layout:
- Max-width: 768px (prose)
- Padding: 24px (mobile), 48px (desktop)
- Center aligned

Elements:
- Category Badge:
  - Background: blue-100, Text: blue-700
  - Padding: 4px 12px
  - Border-radius: 9999px (pill)
  - Font: text-sm, font-medium

- Title (H1):
  - Font: text-3xl (mobile), text-4xl (desktop)
  - Font-weight: 800
  - Color: gray-900
  - Line-height: 1.2
  - Margin-bottom: 16px

- Meta info:
  - Font: text-sm
  - Color: gray-500
  - Icons: Lucide (Calendar, User, Clock)
  - Gap between items: 16px
```

### 2. Table of Contents
```
Layout:
- Desktop: Sticky sidebar (right side)
- Mobile: Collapsible accordion at top

Styling:
- Background: gray-50
- Border: 1px solid gray-200
- Border-radius: 8px
- Padding: 16px

Items:
- Font: text-sm
- Color: gray-600
- Active state: text-blue-600, font-medium
- Hover: text-gray-900
- Left border on active: 2px solid blue-600
```

### 3. Section Headers (H2)
```
- Font: text-2xl
- Font-weight: 700
- Color: gray-900
- Margin-top: 48px
- Margin-bottom: 24px
- Padding-top: 24px
- Border-top: 1px solid gray-200 (optional divider)

Emoji prefix (optional):
- 🚀 สำหรับ Intro
- 📦 สำหรับ Installation
- 🧩 สำหรับ Components
- 🎨 สำหรับ Customization
- ⚖️ สำหรับ Comparison
- ✅ สำหรับ Summary
```

### 4. Code Block
```
Layout:
- Width: 100%
- Border-radius: 8px
- Overflow: hidden

Header:
- Background: gray-800
- Padding: 8px 16px
- Display: flex, justify-between
- Language label: text-xs, gray-400
- Copy button: icon button, hover: gray-600

Code area:
- Background: gray-900
- Padding: 16px
- Font: JetBrains Mono / Fira Code / monospace
- Font-size: 14px
- Line-height: 1.6
- Syntax highlighting: Prism.js style

Copy button states:
- Default: Copy icon
- Copied: Check icon + "Copied!" (green)
- Reset after 2s
```

### 5. Info/Tip Box
```
Variants:
1. Info (blue):
   - Background: blue-50
   - Border-left: 4px solid blue-500
   - Icon: Info circle (blue-500)

2. Tip (green):
   - Background: green-50
   - Border-left: 4px solid green-500
   - Icon: Lightbulb (green-500)

3. Warning (yellow):
   - Background: yellow-50
   - Border-left: 4px solid yellow-500
   - Icon: Alert triangle (yellow-500)

Layout:
- Padding: 16px
- Border-radius: 8px (right corners only)
- Margin: 24px 0

Content:
- Title: font-medium, color matching variant
- Text: text-sm, gray-700
```

### 6. Comparison Table
```
Layout:
- Width: 100%
- Border: 1px solid gray-200
- Border-radius: 8px
- Overflow: hidden

Header row:
- Background: gray-50
- Font-weight: 600
- Padding: 12px 16px

Body rows:
- Padding: 12px 16px
- Border-bottom: 1px solid gray-100
- Hover: background gray-50

Cells:
- Feature column: font-medium
- Check/cross icons: green-500 / red-500
```

### 7. Component Example Card
```
Layout:
- Background: white
- Border: 1px solid gray-200
- Border-radius: 12px
- Overflow: hidden
- Margin: 16px 0

Structure:
+---------------------------+
| Component Name      [i]   |  <- Header
+---------------------------+
|                           |
|   [Live Preview Area]     |  <- Preview
|                           |
+---------------------------+
| <code example>            |  <- Code
+---------------------------+

Header:
- Background: gray-50
- Padding: 12px 16px
- Font-weight: 600

Preview:
- Padding: 24px
- Background: white
- Min-height: 100px
- Display: flex, center

Code:
- Collapsible
- Toggle: "Show code" / "Hide code"
```

---

## Typography Scale

| Element | Size | Weight | Line-height |
|---------|------|--------|-------------|
| H1 (Title) | 36px / 40px | 800 | 1.2 |
| H2 (Section) | 24px | 700 | 1.3 |
| H3 (Subsection) | 20px | 600 | 1.4 |
| Body | 16px | 400 | 1.7 |
| Code | 14px | 400 | 1.6 |
| Small/Meta | 14px | 400 | 1.5 |

---

## Color Palette

```css
/* Article specific */
--article-bg: #FFFFFF;
--article-text: #1F2937;      /* gray-800 */
--article-muted: #6B7280;     /* gray-500 */

/* Code block */
--code-bg: #111827;           /* gray-900 */
--code-header: #1F2937;       /* gray-800 */
--code-text: #E5E7EB;         /* gray-200 */

/* Accent (Antd blue) */
--antd-primary: #1677FF;
--antd-primary-light: #E6F4FF;

/* Info boxes */
--info-bg: #EFF6FF;           /* blue-50 */
--info-border: #3B82F6;       /* blue-500 */
--tip-bg: #F0FDF4;            /* green-50 */
--tip-border: #22C55E;        /* green-500 */
```

---

## Responsive Behavior

### Desktop (>1024px)
- Content max-width: 768px
- TOC: Sticky sidebar on right
- Code blocks: Full width with horizontal scroll

### Tablet (640-1024px)
- Content max-width: 100%
- TOC: Top of article, collapsible
- Code blocks: Full width

### Mobile (<640px)
- Content: Full width, padding 16px
- TOC: Collapsible accordion
- Code blocks: Horizontal scroll
- Comparison table: Horizontal scroll

---

## Content Structure for Developer

```markdown
# Ant Design (Antd) คู่มือเริ่มต้นสำหรับมือใหม่

[Meta: category, date, author, reading time]

[TOC]

## 🚀 Antd คืออะไร?
- อธิบายสั้นๆ
- [Info Box] ข้อดี 3 ข้อ
- เหมาะกับโปรเจคแบบไหน

## 📦 Installation
- Step 1: Install package
- Step 2: Setup with Next.js App Router
- [Code Block] package install
- [Code Block] app/layout.tsx setup
- [Tip Box] สำหรับ App Router ต้องใส่ 'use client'

## 🧩 Basic Components
### Button
- [Component Card] ตัวอย่าง Button variants
- [Code Block]

### Input
- [Component Card] ตัวอย่าง Input
- [Code Block]

### Card
- [Component Card]
- [Code Block]

### Table
- [Component Card]
- [Code Block]

### Form
- [Component Card]
- [Code Block]

## 🎨 Customization
- ConfigProvider
- [Code Block] Theme config example

## ⚖️ เปรียบเทียบ
- [Comparison Table] Antd vs shadcn/ui vs MUI

## ✅ สรุป
- Key takeaways (bullet points)
- เมื่อไหร่ควรใช้ Antd
- [Tip Box] คำแนะนำสุดท้าย

[Tags]
```

---

## Assets Needed
- None (ใช้ Lucide icons ที่มีอยู่แล้ว)

---

## Handoff Checklist
- [x] Layout structure defined
- [x] Component specs complete
- [x] Typography scale defined
- [x] Color palette defined
- [x] Responsive breakpoints defined
- [x] Content structure outlined
- [x] Ready for Developer

---

*Design by @Designer - 2026-02-01*
