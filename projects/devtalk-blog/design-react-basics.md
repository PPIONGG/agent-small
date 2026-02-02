# Design Specs: บทความ React เบื้องต้น สำหรับมือใหม่ 2026

## Overview
บทความสอน React สำหรับผู้เริ่มต้น ออกแบบให้อ่านง่าย เน้น hands-on learning มี code examples ที่ใช้งานได้จริง

> ใช้ Design System เดียวกับ [design.md](design.md) และ pattern เดียวกับ [design-antd-article.md](design-antd-article.md)

---

## Page Layout

```
+--------------------------------------------------+
|  Header (existing)                               |
+--------------------------------------------------+
|                                                  |
|  📌 Breadcrumb: Home > Posts > React เบื้องต้น    |
|                                                  |
|  +--------------------------------------------+  |
|  |  🏷️ Category Badge: "React"               |  |
|  |                                            |  |
|  |  # React เบื้องต้น                         |  |
|  |    คู่มือสำหรับมือใหม่ 2026                |  |
|  |                                            |  |
|  |  📅 2 Feb 2026  •  👤 Author  •  ⏱️ 15 min |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  📑 Table of Contents (Sticky on Desktop)  |  |
|  |  1. React คืออะไร?                         |  |
|  |  2. Prerequisites                          |  |
|  |  3. เริ่มต้นด้วย Vite                       |  |
|  |  4. JSX                                    |  |
|  |  5. Components                             |  |
|  |  6. Props                                  |  |
|  |  7. State                                  |  |
|  |  8. useEffect                              |  |
|  |  9. Event Handling                         |  |
|  |  10. โปรเจค Todo App                       |  |
|  |  11. Next Steps                            |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | CONTENT SECTIONS                           |  |
|  |                                            |  |
|  | [Prerequisites Box - Special]              |  |
|  | - HTML, CSS, JavaScript ES6+               |  |
|  |                                            |  |
|  | [Section 1-11 Content]                     |  |
|  | - Step-by-step learning                    |  |
|  | - Code blocks with copy                    |  |
|  | - Tip/Warning boxes                        |  |
|  |                                            |  |
|  | [Mini Project: Todo App]                   |  |
|  | - Step-by-step walkthrough                 |  |
|  | - Full code at the end                     |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  🏷️ Tags: react, javascript, tutorial     |  |
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
  - Background: cyan-100, Text: cyan-700 (React brand)
  - Padding: 4px 12px
  - Border-radius: 9999px (pill)
  - Font: text-sm, font-medium

- Title (H1):
  - Font: text-3xl (mobile), text-4xl (desktop)
  - Font-weight: 800
  - Color: gray-900
  - Line-height: 1.2
  - Margin-bottom: 8px

- Subtitle:
  - Font: text-xl
  - Color: gray-600
  - Margin-bottom: 16px

- Meta info:
  - Font: text-sm
  - Color: gray-500
  - Icons: Lucide (Calendar, User, Clock)
  - Gap between items: 16px
```

### 2. Prerequisites Box (Special Component)
```
ใช้เมื่อต้องการแสดง prerequisites ก่อนเริ่มเรียน

Layout:
- Background: gradient from cyan-50 to blue-50
- Border: 2px solid cyan-200
- Border-radius: 12px
- Padding: 24px
- Margin: 32px 0

Structure:
+------------------------------------------+
|  📋 ก่อนเริ่ม คุณต้องรู้...              |
|  ─────────────────────────────────       |
|  ✓ HTML พื้นฐาน                          |
|  ✓ CSS พื้นฐาน                           |
|  ✓ JavaScript ES6+                       |
|    • Arrow functions                     |
|    • Destructuring                       |
|    • Modules (import/export)             |
|    • Async/await                         |
+------------------------------------------+

Title:
- Font: text-lg, font-semibold
- Color: cyan-800
- Icon: 📋 หรือ Lucide ClipboardList

Items:
- Checkmark: cyan-500
- Font: text-base
- Sub-items: indented, text-sm, gray-600
```

### 3. Section Headers (H2)
```
- Font: text-2xl
- Font-weight: 700
- Color: gray-900
- Margin-top: 48px
- Margin-bottom: 24px
- Padding-top: 24px
- Border-top: 1px solid gray-200

Emoji prefix ตาม section:
- ⚛️ สำหรับ React intro
- 📚 สำหรับ Prerequisites
- 🚀 สำหรับ Getting Started (Vite)
- 🧩 สำหรับ JSX
- 📦 สำหรับ Components
- 📨 สำหรับ Props
- 🔄 สำหรับ State
- ⚡ สำหรับ useEffect
- 🎯 สำหรับ Event Handling
- 🏗️ สำหรับ Project
- 🎓 สำหรับ Next Steps
```

### 4. Step-by-Step Box
```
ใช้สำหรับ instructions แบบ step-by-step

Layout:
- Background: gray-50
- Border-radius: 8px
- Padding: 16px 24px

Structure:
+------------------------------------------+
|  Step 1: สร้างโปรเจคใหม่                  |
|                                          |
|  [Code Block]                            |
|  npm create vite@latest my-app           |
|                                          |
|  Step 2: เลือก React template            |
|  ...                                     |
+------------------------------------------+

Step Label:
- Font: text-sm, font-bold
- Color: cyan-600
- Background: cyan-100
- Padding: 2px 8px
- Border-radius: 4px
- Margin-bottom: 8px

Step Content:
- Font: text-base
- Color: gray-700
```

### 5. Code Block (Enhanced)
```
Layout:
- Width: 100%
- Border-radius: 8px
- Overflow: hidden
- Margin: 16px 0

Header:
- Background: gray-800
- Padding: 8px 16px
- Display: flex, justify-between
- Language label: text-xs, gray-400
- Filename (optional): text-xs, cyan-400
- Copy button: icon button, hover: gray-600

Code area:
- Background: gray-900
- Padding: 16px
- Font: Geist Mono / JetBrains Mono / monospace
- Font-size: 14px
- Line-height: 1.6
- Syntax highlighting: Shiki

Special for React:
- JSX syntax highlighting
- Comments: gray-500
- Keywords (const, return): purple-400
- Components: cyan-300
- Props: yellow-300
- Strings: green-400
```

### 6. Concept Explanation Box
```
ใช้อธิบาย concepts สำคัญ

Layout:
- Background: white
- Border: 1px solid gray-200
- Border-left: 4px solid cyan-500
- Border-radius: 0 8px 8px 0
- Padding: 16px 20px
- Margin: 24px 0

Title:
- Font: text-base, font-semibold
- Color: gray-800
- Icon: 💡

Content:
- Font: text-sm
- Color: gray-600
- Line-height: 1.7

Example:
+------------------------------------------+
| 💡 State คืออะไร?                        |
|                                          |
| State คือข้อมูลที่เก็บไว้ใน component    |
| และเมื่อ state เปลี่ยน component จะ      |
| re-render ใหม่โดยอัตโนมัติ               |
+------------------------------------------+
```

### 7. Code Comparison (Before/After)
```
ใช้เปรียบเทียบ code ก่อน/หลัง หรือ wrong/right

Layout:
- Display: grid, 2 columns (desktop)
- Gap: 16px
- Stack on mobile

Structure:
+-------------------+  +-------------------+
| ❌ Don't do this  |  | ✅ Do this        |
|                   |  |                   |
| [Code Block]      |  | [Code Block]      |
+-------------------+  +-------------------+

Label:
- ❌ Background: red-50, Border: red-200
- ✅ Background: green-50, Border: green-200
```

### 8. Interactive Demo Placeholder
```
สำหรับ embedded demo (ถ้ามีในอนาคต)

Layout:
- Background: gray-100
- Border: 2px dashed gray-300
- Border-radius: 12px
- Padding: 32px
- Text-align: center

Content:
- Icon: Play (Lucide)
- Text: "ลองรันดู" / "Try it yourself"
- Link: CodeSandbox / StackBlitz

หมายเหตุ: Phase แรกใช้ static code blocks ก่อน
```

### 9. Mini Project Section
```
สำหรับ Todo App project

Layout:
- Background: gradient from gray-50 to cyan-50
- Border: 2px solid cyan-200
- Border-radius: 16px
- Padding: 32px
- Margin: 48px 0

Structure:
+------------------------------------------+
|  🏗️ โปรเจค: Todo App                     |
|                                          |
|  สิ่งที่จะได้เรียนรู้:                     |
|  • useState สำหรับจัดการ list             |
|  • Event handling (onClick, onChange)    |
|  • Conditional rendering                 |
|  • List rendering with map()             |
|                                          |
|  [Preview Image - mockup]                |
|                                          |
|  [Step-by-step instructions]             |
|                                          |
|  [Full Code Accordion]                   |
+------------------------------------------+

Title:
- Font: text-2xl, font-bold
- Color: gray-900

Learning points:
- Checkmark bullets
- Font: text-base
```

### 10. Callout Boxes (Tips, Warnings)
```
Variants:
1. Tip (cyan - React theme):
   - Background: cyan-50
   - Border-left: 4px solid cyan-500
   - Icon: 💡 Lightbulb (cyan-600)

2. Warning (amber):
   - Background: amber-50
   - Border-left: 4px solid amber-500
   - Icon: ⚠️ AlertTriangle (amber-600)

3. Important (red):
   - Background: red-50
   - Border-left: 4px solid red-500
   - Icon: ❗ AlertCircle (red-600)

4. Note (blue):
   - Background: blue-50
   - Border-left: 4px solid blue-500
   - Icon: ℹ️ Info (blue-600)

Layout:
- Padding: 16px 20px
- Border-radius: 0 8px 8px 0
- Margin: 24px 0

Placement Rules:
- ไม่เกิน 2 callouts ติดกัน
- ใช้ Warning เมื่อมี common mistake
- ใช้ Tip สำหรับ best practices
```

### 11. Next Steps Section
```
Layout:
- Background: gradient cyan-500 to blue-600
- Border-radius: 16px
- Padding: 32px
- Color: white
- Margin-top: 48px

Structure:
+------------------------------------------+
|  🎓 ก้าวต่อไป                             |
|                                          |
|  ยินดีด้วย! คุณได้เรียนรู้พื้นฐาน React     |
|  แล้ว ขั้นตอนต่อไปคือ:                     |
|                                          |
|  → React Router - การจัดการ routing      |
|  → Context API - state management        |
|  → Next.js - fullstack framework         |
|                                          |
|  [Resources Links]                       |
+------------------------------------------+

Links:
- Background: white/20
- Hover: white/30
- Border-radius: 8px
- Padding: 12px 16px
```

---

## Typography Scale (Article-specific)

| Element | Size | Weight | Line-height | Color |
|---------|------|--------|-------------|-------|
| H1 (Title) | 36px / 40px | 800 | 1.2 | gray-900 |
| Subtitle | 20px | 400 | 1.4 | gray-600 |
| H2 (Section) | 24px | 700 | 1.3 | gray-900 |
| H3 (Subsection) | 20px | 600 | 1.4 | gray-800 |
| Body | 16px | 400 | 1.75 | gray-700 |
| Code | 14px | 400 | 1.6 | - |
| Small/Meta | 14px | 400 | 1.5 | gray-500 |

---

## Color Palette (React Theme)

```css
/* React brand accent */
--react-primary: #61DAFB;      /* React cyan */
--react-dark: #20232A;         /* React dark */

/* Article specific */
--article-bg: #FFFFFF;
--article-text: #1F2937;       /* gray-800 */
--article-muted: #6B7280;      /* gray-500 */

/* Code block */
--code-bg: #1E1E1E;            /* VS Code dark */
--code-header: #2D2D2D;
--code-text: #D4D4D4;

/* Accent for React content */
--accent-primary: #06B6D4;     /* cyan-500 */
--accent-light: #ECFEFF;       /* cyan-50 */
--accent-dark: #0E7490;        /* cyan-700 */

/* Callout colors (same as design-antd-article.md) */
--tip-bg: #ECFEFF;             /* cyan-50 */
--tip-border: #06B6D4;         /* cyan-500 */
--warning-bg: #FFFBEB;         /* amber-50 */
--warning-border: #F59E0B;     /* amber-500 */
```

---

## Responsive Behavior

### Desktop (>1024px)
- Content max-width: 768px
- TOC: Sticky sidebar on right
- Code comparison: 2 columns
- Mini project: Full width with image

### Tablet (640-1024px)
- Content max-width: 100%
- TOC: Top of article, collapsible
- Code comparison: 2 columns (narrower)
- Mini project: Stack vertically

### Mobile (<640px)
- Content: Full width, padding 16px
- TOC: Collapsible accordion
- Code comparison: Stack vertically
- Mini project: Simplified layout
- Code blocks: Horizontal scroll

---

## Content Structure for Developer

```markdown
# React เบื้องต้น คู่มือสำหรับมือใหม่ 2026

[Meta: category=React, date, author, reading time=15 min]

[TOC]

[Prerequisites Box]
- HTML พื้นฐาน
- CSS พื้นฐาน
- JavaScript ES6+

## ⚛️ React คืออะไร?
- อธิบายสั้นๆ
- [Concept Box] ทำไม React ถึงนิยม
- React 19 overview

## 🚀 เริ่มต้นด้วย Vite
- [Step-by-step Box]
- [Code Block] npm create vite
- [Warning] ไม่แนะนำ Create React App
- อธิบาย project structure

## 🧩 JSX คืออะไร?
- [Concept Box] JSX = JavaScript + HTML
- [Code Block] ตัวอย่าง JSX
- [Code Comparison] HTML vs JSX
- [Tip] Rules ของ JSX

## 📦 Components
- [Concept Box] Component คืออะไร
- [Code Block] สร้าง Functional Component
- [Code Block] export/import

## 📨 Props
- [Concept Box] Props คืออะไร
- [Code Block] ส่ง props
- [Code Block] destructuring props
- [Tip] Props เป็น read-only

## 🔄 State
- [Concept Box] State vs Props
- [Code Block] useState
- [Code Comparison] ❌ mutate vs ✅ setState
- [Mini Demo] Counter example

## ⚡ useEffect
- [Concept Box] Side Effects
- [Code Block] useEffect patterns
- [Warning] Dependency array
- [Code Block] Cleanup function

## 🎯 Event Handling
- [Code Block] onClick, onChange
- [Code Block] Form handling
- [Tip] Naming convention

## 🏗️ โปรเจค: Todo App
- [Mini Project Section]
- Step-by-step walkthrough
- [Full Code Accordion]

## 🎓 ก้าวต่อไป
- [Next Steps Section]
- Resources links

[Tags: react, javascript, tutorial, beginner]
```

---

## Assets Needed
- React logo icon (optional, ใช้ emoji ⚛️ ก็ได้)
- Todo App preview mockup (optional)
- Lucide icons: ClipboardList, Lightbulb, AlertTriangle, Info, ChevronRight

---

## Handoff Checklist

- [x] Layout structure defined
- [x] All component specs complete
- [x] Typography scale defined
- [x] Color palette defined (React theme)
- [x] Responsive breakpoints defined
- [x] Content structure outlined
- [x] Callout types defined
- [x] Special components (Prerequisites, Step-by-step, Mini Project)
- [x] Ready for Developer

---

*Design by @Designer - 2026-02-02*
*Status: Ready for Development*
