# Design Specs: Conventional Commits คู่มือฉบับสมบูรณ์

## Overview
บทความ guide สำหรับ Conventional Commits แบบละเอียด ออกแบบให้เป็น reference ที่ครบถ้วน มี code examples, tables, tools setup และ real-world examples

> ใช้ Design System เดียวกับ [design.md](design.md) และ pattern เดียวกับ [design-react-basics.md](design-react-basics.md)

---

## Theme: Git/Commit Style

ใช้สี **Orange/Purple** สื่อถึง Git และ version control

```css
/* Git theme */
--git-orange: #F05032;       /* Git logo orange */
--git-purple: #8B5CF6;       /* Purple-500 for accents */
--commit-dark: #24292E;      /* GitHub dark */

/* Article accents */
--accent-primary: #F97316;   /* orange-500 */
--accent-light: #FFF7ED;     /* orange-50 */
--accent-dark: #C2410C;      /* orange-700 */
```

---

## Page Layout

```
+--------------------------------------------------+
|  Header (existing)                               |
+--------------------------------------------------+
|                                                  |
|  📌 Breadcrumb: Home > Posts > Conventional...   |
|                                                  |
|  +--------------------------------------------+  |
|  |  🏷️ Category Badge: "Development"         |  |
|  |                                            |  |
|  |  # Conventional Commits                   |  |
|  |    คู่มือฉบับสมบูรณ์                       |  |
|  |                                            |  |
|  |  📅 Date  •  👤 Author  •  ⏱️ 20 min       |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  |  📑 Table of Contents (15 sections)       |  |
|  |  1. Intro                                 |  |
|  |  2. รูปแบบ Commit Message                  |  |
|  |  3. Types ทั้งหมด                          |  |
|  |  4. Scope                                 |  |
|  |  5. Body และ Footer                       |  |
|  |  6. Breaking Changes                      |  |
|  |  7. Commitlint                            |  |
|  |  8. Husky                                 |  |
|  |  9. Commitizen                            |  |
|  |  10. Semantic Release                     |  |
|  |  11. Common Mistakes                      |  |
|  |  12. IDE Extensions                       |  |
|  |  13. แก้ไข Commit ที่ผิด                   |  |
|  |  14. Real-world Examples                  |  |
|  |  15. สรุปและ Cheatsheet                   |  |
|  +--------------------------------------------+  |
|                                                  |
|  +--------------------------------------------+  |
|  | CONTENT SECTIONS                           |  |
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
  - Background: orange-100, Text: orange-700
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

### 2. Commit Format Box (Special Component)
```
ใช้แสดงรูปแบบ commit message หลัก

Layout:
- Background: gray-900 (dark terminal look)
- Border: 2px solid orange-500
- Border-radius: 12px
- Padding: 24px
- Margin: 32px 0
- Font-family: monospace

Structure:
+------------------------------------------+
|  📝 รูปแบบ Commit Message                 |
|  ─────────────────────────────────        |
|                                           |
|  <type>[optional scope]: <description>    |
|                                           |
|  [optional body]                          |
|                                           |
|  [optional footer(s)]                     |
|                                           |
+------------------------------------------+

Parts Highlighting:
- <type>: orange-400
- [optional scope]: purple-400
- <description>: white
- body/footer: gray-400

Title:
- Font: text-lg, font-semibold
- Color: orange-400
- Icon: 📝 หรือ Lucide FileText
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
- 📖 สำหรับ Intro
- 📝 สำหรับ รูปแบบ Commit Message
- 🏷️ สำหรับ Types
- 📦 สำหรับ Scope
- 📄 สำหรับ Body และ Footer
- ⚠️ สำหรับ Breaking Changes
- 🔧 สำหรับ Commitlint
- 🐶 สำหรับ Husky
- 💬 สำหรับ Commitizen
- 🚀 สำหรับ Semantic Release
- ❌ สำหรับ Common Mistakes
- 💻 สำหรับ IDE Extensions
- 🔄 สำหรับ แก้ไข Commit ที่ผิด
- 🌍 สำหรับ Real-world Examples
- 📋 สำหรับ สรุปและ Cheatsheet
```

### 4. Type Examples Table (Special Component)
```
ใช้แสดงแต่ละ type พร้อมตัวอย่างละเอียด

Layout:
- Width: 100%
- Border: 1px solid gray-200
- Border-radius: 12px
- Overflow: hidden

Structure:
+------+----------+----------------------------------------+
| Type | ใช้เมื่อ  | ตัวอย่าง                                |
+------+----------+----------------------------------------+
| feat | เพิ่ม..  | feat(auth): add OAuth login            |
|      |          | feat(cart): implement checkout flow    |
|      |          | feat: add dark mode support            |
+------+----------+----------------------------------------+
| fix  | แก้ bug  | fix(api): handle null response         |
|      |          | fix(ui): correct button alignment      |
+------+----------+----------------------------------------+

Header:
- Background: orange-50
- Font: text-sm, font-semibold
- Padding: 12px 16px

Row:
- Background: white
- Border-bottom: 1px solid gray-100
- Padding: 12px 16px

Type Column:
- Background: gray-100
- Font: monospace, font-semibold
- Color: orange-600
- Width: 80px

Examples:
- Font: monospace, text-sm
- Color: gray-700
- Each example on new line
- Hover: highlight row
```

### 5. Before/After Comparison (Mistakes Table)
```
ใช้แสดง common mistakes

Layout:
- Display: grid, 3 columns (ผิด | ถูก | เหตุผล)
- Border-radius: 12px
- Border: 1px solid gray-200
- Overflow: hidden

Structure:
+-------------------+-------------------+------------------+
| ❌ ผิด            | ✅ ถูก            | เหตุผล           |
+-------------------+-------------------+------------------+
| update code       | feat(auth): add   | ไม่มี type        |
|                   | login             |                  |
+-------------------+-------------------+------------------+
| feat: Add Feature | feat: add feature | ตัวใหญ่           |
+-------------------+-------------------+------------------+

Wrong Column:
- Background: red-50
- Border-left: 3px solid red-500
- Font: monospace
- Color: red-700

Right Column:
- Background: green-50
- Border-left: 3px solid green-500
- Font: monospace
- Color: green-700

Reason Column:
- Background: white
- Font: text-sm
- Color: gray-600
```

### 6. Tool Setup Box (Step-by-step)
```
ใช้สำหรับ Commitlint, Husky, Commitizen, Semantic Release

Layout:
- Background: gray-50
- Border: 1px solid gray-200
- Border-radius: 12px
- Padding: 24px
- Margin: 24px 0

Structure:
+------------------------------------------+
|  🔧 Setup: Commitlint                     |
|                                          |
|  Step 1: ติดตั้ง packages                 |
|  [Code Block]                            |
|                                          |
|  Step 2: สร้าง config file               |
|  [Code Block]                            |
|                                          |
|  Step 3: ทดสอบ                           |
|  [Code Block]                            |
+------------------------------------------+

Title:
- Font: text-lg, font-bold
- Color: gray-900
- Icon: Tool icon (🔧 or Lucide)
- Border-bottom: 1px solid gray-200
- Padding-bottom: 12px
- Margin-bottom: 16px

Step Label:
- Font: text-sm, font-bold
- Color: orange-600
- Background: orange-100
- Padding: 2px 8px
- Border-radius: 4px
```

### 7. Code Block (Terminal Style)
```
ใช้สำหรับ commands และ config files

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
- Filename: text-xs, orange-400
- Copy button: icon button

Code area:
- Background: gray-900
- Padding: 16px
- Font: Geist Mono / monospace
- Font-size: 14px
- Line-height: 1.6

Syntax colors:
- Commands (npm, git): orange-400
- Flags (--): purple-400
- Strings: green-400
- Comments: gray-500
```

### 8. Config File Display
```
ใช้แสดง configuration files (commitlint.config.js, etc.)

Layout:
- Border-radius: 8px
- Border: 1px solid gray-300
- Overflow: hidden

Header:
- Background: gray-200
- Padding: 8px 12px
- Font: text-xs
- Display: flex, items-center, gap-8px
- File icon: orange-500
- Filename: gray-700, font-medium

Body:
- Same as Code Block
- Syntax highlighting: JS/JSON
```

### 9. Real-world Example Box
```
ใช้แสดงตัวอย่างจาก projects จริง

Layout:
- Background: white
- Border: 2px solid purple-200
- Border-radius: 12px
- Padding: 20px
- Margin: 24px 0

Structure:
+------------------------------------------+
|  🌍 ตัวอย่างจาก: Angular                  |
|                                          |
|  [Code Block - commit example]           |
|                                          |
|  📎 Source: github.com/angular/angular   |
+------------------------------------------+

Project Name:
- Font: text-base, font-semibold
- Color: purple-700
- Icon: 🌍

Source Link:
- Font: text-xs
- Color: purple-500
- Icon: 📎 or Lucide Link
- Hover: underline
```

### 10. Callout Boxes
```
Variants:
1. Tip (orange - Git theme):
   - Background: orange-50
   - Border-left: 4px solid orange-500
   - Icon: 💡 (orange-600)

2. Warning (amber):
   - Background: amber-50
   - Border-left: 4px solid amber-500
   - Icon: ⚠️ (amber-600)

3. Important (red):
   - Background: red-50
   - Border-left: 4px solid red-500
   - Icon: ❗ (red-600)

4. Note (blue):
   - Background: blue-50
   - Border-left: 4px solid blue-500
   - Icon: ℹ️ (blue-600)

Layout:
- Padding: 16px 20px
- Border-radius: 0 8px 8px 0
- Margin: 24px 0
```

### 11. IDE Extension Cards
```
ใช้แสดง extensions สำหรับ IDE

Layout:
- Display: grid, 2 columns (desktop), 1 column (mobile)
- Gap: 16px

Card:
- Background: white
- Border: 1px solid gray-200
- Border-radius: 8px
- Padding: 16px
- Hover: shadow-md

Structure:
+------------------------------------------+
|  [Icon]  Conventional Commits            |
|          for VS Code                     |
|                                          |
|  Interactive commit message builder      |
|                                          |
|  [Install Button]                        |
+------------------------------------------+

Icon:
- Size: 48x48
- Border-radius: 8px

Title:
- Font: text-base, font-semibold

Description:
- Font: text-sm
- Color: gray-600

Install Button:
- Background: orange-500
- Color: white
- Padding: 8px 16px
- Border-radius: 6px
- Hover: orange-600
```

### 12. Cheatsheet Section
```
ใช้สำหรับ quick reference ท้ายบทความ

Layout:
- Background: gradient from gray-50 to orange-50
- Border: 2px solid orange-200
- Border-radius: 16px
- Padding: 32px
- Margin: 48px 0

Structure:
+------------------------------------------+
|  📋 Quick Reference Cheatsheet           |
|                                          |
|  Types Summary:                          |
|  [Compact Table]                         |
|                                          |
|  Commands:                               |
|  [Code snippets grid]                    |
|                                          |
|  [Download PDF Button]                   |
+------------------------------------------+

Title:
- Font: text-2xl, font-bold
- Color: gray-900

Sub-sections:
- Font: text-lg, font-semibold
- Color: orange-700
- Margin-top: 24px
```

---

## Typography Scale

| Element | Size | Weight | Line-height | Color |
|---------|------|--------|-------------|-------|
| H1 (Title) | 36px / 40px | 800 | 1.2 | gray-900 |
| Subtitle | 20px | 400 | 1.4 | gray-600 |
| H2 (Section) | 24px | 700 | 1.3 | gray-900 |
| H3 (Subsection) | 20px | 600 | 1.4 | gray-800 |
| Body | 16px | 400 | 1.75 | gray-700 |
| Code/Mono | 14px | 400 | 1.6 | - |
| Small/Meta | 14px | 400 | 1.5 | gray-500 |
| Table | 14px | 400 | 1.5 | gray-700 |

---

## Color Palette

```css
/* Git theme accents */
--git-orange: #F05032;        /* Git logo */
--accent-primary: #F97316;    /* orange-500 */
--accent-light: #FFF7ED;      /* orange-50 */
--accent-dark: #C2410C;       /* orange-700 */

/* Secondary (purple for variety) */
--secondary: #8B5CF6;         /* purple-500 */
--secondary-light: #F5F3FF;   /* purple-50 */

/* Article */
--article-bg: #FFFFFF;
--article-text: #1F2937;      /* gray-800 */
--article-muted: #6B7280;     /* gray-500 */

/* Code block */
--code-bg: #1E1E1E;           /* VS Code dark */
--code-header: #2D2D2D;
--code-text: #D4D4D4;

/* Semantic (mistakes table) */
--success-bg: #ECFDF5;        /* green-50 */
--success-border: #10B981;    /* green-500 */
--error-bg: #FEF2F2;          /* red-50 */
--error-border: #EF4444;      /* red-500 */

/* Callout */
--tip-bg: #FFF7ED;            /* orange-50 */
--tip-border: #F97316;        /* orange-500 */
--warning-bg: #FFFBEB;        /* amber-50 */
--warning-border: #F59E0B;    /* amber-500 */
```

---

## Responsive Behavior

### Desktop (>1024px)
- Content max-width: 768px
- TOC: Sticky sidebar on right
- Tables: Full width
- IDE cards: 2 columns
- Mistakes table: 3 columns

### Tablet (640-1024px)
- Content max-width: 100%
- TOC: Top of article, collapsible
- Tables: Horizontal scroll if needed
- IDE cards: 2 columns
- Mistakes table: 3 columns (narrower)

### Mobile (<640px)
- Content: Full width, padding 16px
- TOC: Collapsible accordion
- Tables: Horizontal scroll
- IDE cards: 1 column
- Mistakes table: Stack vertically
- Code blocks: Horizontal scroll

---

## Content Structure for Developer

```markdown
# Conventional Commits: คู่มือฉบับสมบูรณ์

[Meta: category=Development, date, author, reading time=20 min]

[TOC - 15 sections]

## 📖 1. Intro
- Conventional Commits คืออะไร (expanded)
- ทำไมถึงสำคัญ (with examples)
- ใครใช้บ้าง (Angular, Vue, Vite logos)

## 📝 2. รูปแบบ Commit Message
- [Commit Format Box]
- อธิบายแต่ละส่วน
- [Tip] 50/72 rule

## 🏷️ 3. Types ทั้งหมด
- [Type Examples Table - expandable]
- 10 types พร้อม 3+ examples each

## 📦 4. Scope
- [Concept Box] Scope คืออะไร
- [Before/After] ดี vs ไม่ดี
- Common scopes list

## 📄 5. Body และ Footer
- เมื่อไหร่ใช้ body
- Footer types (table)
- [Code Block] Full commit example

## ⚠️ 6. Breaking Changes
- [Warning Box] เมื่อไหร่ถือว่า breaking
- วิธีเขียน (! และ footer)
- [Real-world Example]

## 🔧 7. Commitlint Setup
- [Tool Setup Box]
- [Config File] commitlint.config.js
- Custom rules examples

## 🐶 8. Husky Setup
- [Tool Setup Box]
- commit-msg hook
- pre-commit hook
- [Tip] Troubleshooting

## 💬 9. Commitizen
- [Tool Setup Box]
- Interactive demo screenshot
- [Tip] ทำไมควรใช้

## 🚀 10. Semantic Release
- [Concept Box] Overview
- Basic setup
- [Code Block] CHANGELOG example

## ❌ 11. Common Mistakes
- [Before/After Table - 10+ mistakes]
- Each with explanation

## 💻 12. IDE Extensions
- [IDE Extension Cards]
- VS Code
- JetBrains

## 🔄 13. แก้ไข Commit ที่ผิด
- git commit --amend
- Interactive rebase
- [Warning] Force push

## 🌍 14. Real-world Examples
- [Real-world Example Box] Angular
- [Real-world Example Box] Vue.js
- [Real-world Example Box] Vite

## 📋 15. สรุปและ Cheatsheet
- [Cheatsheet Section]
- Quick reference table
- Resources links

[Tags: git, conventional-commits, best-practices, tools]
```

---

## Special Notes for Developer

1. **Tables are Key**
   - Type examples table ต้องอ่านง่าย ใช้ horizontal scroll บน mobile
   - Mistakes table ใช้สี red/green ชัดเจน

2. **Code Blocks**
   - ทุก tool setup ต้องมี copy button
   - แสดง filename ที่ header เสมอ
   - Syntax highlight: bash, js, json

3. **TOC is Important**
   - 15 sections = ต้องมี TOC ที่ใช้งานง่าย
   - Highlight current section
   - Mobile: collapsible

4. **Progressive Enhancement**
   - เริ่มด้วย basic sections
   - Tools sections เป็น bonus content

---

## Assets Needed
- Git logo (optional, ใช้ emoji ก็ได้)
- VS Code icon
- JetBrains icon
- Lucide icons: FileText, Terminal, Check, X, Link, Download

---

## Handoff Checklist

- [x] Layout structure defined
- [x] All component specs complete
- [x] Typography scale defined
- [x] Color palette defined (Git/Orange theme)
- [x] Responsive breakpoints defined
- [x] Content structure outlined
- [x] Special components defined:
  - [x] Commit Format Box
  - [x] Type Examples Table
  - [x] Before/After Mistakes Table
  - [x] Tool Setup Box
  - [x] Real-world Example Box
  - [x] IDE Extension Cards
  - [x] Cheatsheet Section
- [x] Ready for Developer

---

*Design by @Designer - 2026-02-02*
*Status: Ready for Development*
