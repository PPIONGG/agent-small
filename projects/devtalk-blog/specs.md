# Project Specs: Next.js Blog

## Overview
เว็บบล็อกสำหรับเขียนและแสดงบทความ สร้างด้วย Next.js App Router ใช้ mock JSON เป็น data source

## Tech Stack
- **Framework**: Next.js 14+ (App Router)
- **Styling**: Tailwind CSS
- **UI Library**: shadcn/ui
- **Icons**: Lucide Icons
- **Data**: Mock JSON (ไฟล์ `.json`)
- **Language**: TypeScript

## Target Users
- ผู้อ่านทั่วไปที่ต้องการอ่านบทความ
- (อนาคต) ผู้เขียนที่ต้องการจัดการ content

---

## Features

### Must Have (MVP)
- [ ] หน้าแรก (Home) - แสดงรายการบทความล่าสุด
- [ ] หน้ารายละเอียดบทความ (Post Detail)
- [ ] หน้า About
- [ ] Responsive Design (Mobile-first)
- [ ] SEO พื้นฐาน (meta tags, title)

### Should Have
- [ ] ค้นหาบทความ (Search)
- [ ] แบ่งหมวดหมู่ (Categories)
- [ ] Pagination
- [ ] Dark Mode
- [ ] Reading Progress Bar
- [ ] Reading Time
- [ ] Back to Top Button
- [ ] Copy Code Button

### Nice to Have
- [ ] Table of Contents (TOC)
- [ ] Tag Cloud
- [ ] Featured Posts (ปักหมุดบทความ)
- [ ] Archive Page (แบ่งตามเดือน/ปี)
- [ ] Keyboard Shortcuts
- [ ] Image Lightbox
- [ ] แชร์บทความไปโซเชียล
- [ ] Related Posts

---

## User Stories

### US-001: ดูรายการบทความ
**As a** ผู้อ่าน
**I want to** เห็นรายการบทความทั้งหมดในหน้าแรก
**So that** ฉันสามารถเลือกอ่านบทความที่สนใจได้

#### Acceptance Criteria
- [ ] แสดงชื่อบทความ, รูป thumbnail, วันที่, และ excerpt
- [ ] เรียงจากใหม่ไปเก่า
- [ ] คลิกแล้วไปหน้ารายละเอียด

#### Priority: 🔴 High

---

### US-002: อ่านบทความ
**As a** ผู้อ่าน
**I want to** อ่านเนื้อหาบทความฉบับเต็ม
**So that** ฉันได้รับความรู้/ความบันเทิงจากบทความ

#### Acceptance Criteria
- [ ] แสดงชื่อบทความ, วันที่, ผู้เขียน
- [ ] แสดงเนื้อหาบทความ (รองรับ Markdown)
- [ ] มีปุ่มกลับหน้าแรก

#### Priority: 🔴 High

---

### US-003: ดูข้อมูล About
**As a** ผู้อ่าน
**I want to** ดูข้อมูลเกี่ยวกับเว็บบล็อกนี้
**So that** ฉันรู้จักเว็บและผู้เขียน

#### Acceptance Criteria
- [ ] แสดงข้อมูลแนะนำเว็บ/ผู้เขียน
- [ ] มีช่องทางติดต่อ

#### Priority: 🟡 Medium

---

## Data Structure

### Post (บทความ)
```json
{
  "id": "string",
  "title": "string",
  "slug": "string",
  "excerpt": "string",
  "content": "string (markdown)",
  "coverImage": "string (URL)",
  "author": "string",
  "category": "string",
  "tags": ["string"],
  "publishedAt": "ISO date string",
  "updatedAt": "ISO date string"
}
```

---

## Pages Structure
```
/                   → หน้าแรก (รายการบทความ)
/posts/[slug]       → หน้าบทความ
/about              → หน้า About
```

---

### US-004: บทความ Ant Design (Antd) เข้าใจง่าย
**As a** ผู้อ่านที่เริ่มต้นเรียนรู้ React/Next.js
**I want to** อ่านบทความ Ant Design แบบเข้าใจง่าย
**So that** ฉันสามารถเริ่มใช้ Antd ในโปรเจคได้อย่างมั่นใจ

#### Acceptance Criteria
- [ ] อธิบาย Ant Design คืออะไร ใช้ทำอะไร
- [ ] แสดงวิธีติดตั้ง Antd ใน Next.js
- [ ] ยกตัวอย่าง components พื้นฐานที่ใช้บ่อย (Button, Input, Card, Table, Form)
- [ ] มีตัวอย่าง code ที่ copy ไปใช้ได้เลย
- [ ] เปรียบเทียบข้อดี/ข้อเสียกับ UI library อื่น (เช่น shadcn/ui, MUI)
- [ ] Tips & Tricks สำหรับมือใหม่
- [ ] Responsive ทดสอบแล้ว
- [ ] SEO meta tags ครบ

#### Priority: 🟡 Medium

#### เนื้อหาที่ต้องมี
1. **Intro**: Antd คืออะไร? ทำไมต้องใช้?
2. **Installation**: วิธีติดตั้งใน Next.js App Router
3. **Basic Components**: Button, Input, Card, Table, Form พร้อมตัวอย่าง
4. **Customization**: วิธีปรับ theme สี/font
5. **เปรียบเทียบ**: Antd vs shadcn/ui vs MUI
6. **สรุป**: ควรใช้เมื่อไหร่?

---

## Phase 2: Reading Experience & UX Features

### US-005: Reading Progress Bar
**As a** ผู้อ่าน
**I want to** เห็นแถบแสดงความคืบหน้าการอ่าน
**So that** ฉันรู้ว่าอ่านไปถึงไหนแล้ว

#### Acceptance Criteria
- [ ] แถบอยู่ด้านบนสุดของหน้า (fixed)
- [ ] แสดง % ที่อ่านไปแล้ว (0-100%)
- [ ] อัพเดทแบบ real-time ตาม scroll
- [ ] สีสอดคล้องกับ theme ของเว็บ

#### Priority: 🟡 Medium

---

### US-006: Reading Time
**As a** ผู้อ่าน
**I want to** เห็นเวลาอ่านโดยประมาณ
**So that** ฉันวางแผนเวลาอ่านได้

#### Acceptance Criteria
- [ ] แสดง "X min read" ใต้หัวข้อบทความ
- [ ] คำนวณจากจำนวนคำ (ประมาณ 200 คำ/นาที)
- [ ] แสดงทั้งหน้า Home (card) และหน้า Post Detail

#### Priority: 🟡 Medium

---

### US-007: Dark Mode
**As a** ผู้อ่าน
**I want to** สลับระหว่างธีมสว่าง/มืด
**So that** ฉันอ่านสบายตาในทุกสภาพแสง

#### Acceptance Criteria
- [ ] มีปุ่ม toggle ที่ header
- [ ] จำค่าที่เลือกไว้ใน localStorage
- [ ] ตรวจสอบ prefers-color-scheme ของระบบ
- [ ] transition ที่ smooth เวลาเปลี่ยน theme
- [ ] ทุก component รองรับทั้ง 2 themes

#### Priority: 🟡 Medium

---

### US-008: Back to Top Button
**As a** ผู้อ่าน
**I want to** กดปุ่มเพื่อกลับไปด้านบนของหน้า
**So that** ฉันไม่ต้อง scroll ขึ้นไปเอง

#### Acceptance Criteria
- [ ] ปุ่มลอยมุมขวาล่าง
- [ ] แสดงเมื่อ scroll ลงไปเกิน 300px
- [ ] Smooth scroll กลับด้านบน
- [ ] Animation fade in/out

#### Priority: 🟢 Low

---

### US-009: Copy Code Button
**As a** ผู้อ่านบทความ tech
**I want to** copy code จาก code block ได้ง่าย
**So that** ฉันนำ code ไปใช้ได้สะดวก

#### Acceptance Criteria
- [ ] ปุ่ม copy มุมขวาบนของทุก code block
- [ ] แสดง feedback เมื่อ copy สำเร็จ (เช่น "Copied!")
- [ ] รองรับทุก code block ในบทความ

#### Priority: 🟡 Medium

---

### US-010: Search บทความ
**As a** ผู้อ่าน
**I want to** ค้นหาบทความด้วย keyword
**So that** ฉันหาบทความที่ต้องการได้เร็ว

#### Acceptance Criteria
- [ ] มีช่อง search ที่ header หรือ หน้า Home
- [ ] ค้นหาจาก title และ excerpt
- [ ] แสดงผลลัพธ์แบบ real-time (debounce)
- [ ] แสดง "ไม่พบผลลัพธ์" เมื่อไม่เจอ

#### Priority: 🟡 Medium

---

### US-011: Tag Cloud
**As a** ผู้อ่าน
**I want to** เห็น tags ยอดนิยมและคลิกดูบทความตาม tag
**So that** ฉันค้นพบบทความที่เกี่ยวข้องได้

#### Acceptance Criteria
- [ ] แสดง tag cloud ที่ sidebar หรือ footer
- [ ] ขนาด tag สัมพันธ์กับจำนวนบทความ
- [ ] คลิก tag แล้วแสดงบทความที่มี tag นั้น

#### Priority: 🟢 Low

---

### US-012: Table of Contents (TOC)
**As a** ผู้อ่านบทความยาว
**I want to** เห็นสารบัญของบทความ
**So that** ฉันข้ามไปหัวข้อที่สนใจได้

#### Acceptance Criteria
- [ ] แสดง TOC ที่ sidebar (desktop) หรือ dropdown (mobile)
- [ ] ดึง headings (h2, h3) จากเนื้อหาอัตโนมัติ
- [ ] Highlight หัวข้อปัจจุบันที่กำลังอ่าน
- [ ] คลิกแล้ว smooth scroll ไปที่หัวข้อนั้น

#### Priority: 🟢 Low

---

### US-013: Featured Posts
**As a** เจ้าของบล็อก
**I want to** ปักหมุดบทความเด่นไว้ด้านบน
**So that** ผู้อ่านเห็นบทความสำคัญก่อน

#### Acceptance Criteria
- [ ] เพิ่ม field `featured: boolean` ใน post data
- [ ] บทความที่ featured แสดงด้านบนสุดของ Home
- [ ] มี badge หรือ style ที่แตกต่าง

#### Priority: 🟢 Low

---

### US-014: Archive Page
**As a** ผู้อ่าน
**I want to** ดูบทความทั้งหมดแบ่งตามเดือน/ปี
**So that** ฉันย้อนดูบทความเก่าได้ง่าย

#### Acceptance Criteria
- [ ] หน้า /archive แสดงบทความจัดกลุ่มตามปี/เดือน
- [ ] แสดงจำนวนบทความในแต่ละเดือน
- [ ] Collapsible sections

#### Priority: 🟢 Low

---

### US-015: Image Lightbox
**As a** ผู้อ่าน
**I want to** คลิกรูปในบทความเพื่อขยายดู
**So that** ฉันเห็นรายละเอียดของรูปได้ชัด

#### Acceptance Criteria
- [ ] คลิกรูปแล้วแสดง modal เต็มจอ
- [ ] กด ESC หรือคลิกนอก modal เพื่อปิด
- [ ] รองรับ zoom และ pan (optional)

#### Priority: 🟢 Low

---

### US-016: Keyboard Shortcuts
**As a** power user
**I want to** ใช้ keyboard shortcuts นำทางในเว็บ
**So that** ฉันใช้งานได้เร็วขึ้นโดยไม่ต้องใช้เมาส์

#### Acceptance Criteria
- [ ] `/` เปิด search
- [ ] `j/k` เลื่อนระหว่างบทความ (หน้า Home)
- [ ] `t` กลับด้านบน
- [ ] `d` toggle dark mode
- [ ] แสดง help modal เมื่อกด `?`

#### Priority: 🟢 Low

---

---

## Phase 3: Mobile Navigation Enhancement

### US-017: Mobile Navigation ที่สมบูรณ์
**As a** ผู้ใช้มือถือ
**I want to** เห็น Mobile Navigation ที่สวยงามและมีข้อมูลครบถ้วน
**So that** ฉันรู้สึกว่าเว็บมีความเป็นมืออาชีพและใช้งานง่าย

#### ปัญหาปัจจุบัน
- Mobile menu ดูโล่งเกินไป (มีแค่ Home, About)
- ขาด visual elements และ branding
- ไม่มีข้อมูลเสริมที่ช่วยให้ผู้ใช้รู้สึกเชื่อมต่อกับเว็บ

#### Acceptance Criteria
- [ ] แสดง Logo/Branding ด้านบนของ menu
- [ ] แสดง nav links ทั้งหมด (Home, About, Archive ถ้ามี)
- [ ] มี Social Links section (GitHub, Twitter, LinkedIn)
- [ ] แสดง Version info (เช่น v1.0.0)
- [ ] แสดง Copyright text
- [ ] มี Theme Toggle button ใน menu
- [ ] มี Search shortcut ใน menu
- [ ] Layout สวยงาม มี spacing ที่เหมาะสม
- [ ] Transition/Animation ที่ smooth

#### UI Structure (แนะนำ)
```
┌─────────────────────────┐
│  ✕ Close               │
├─────────────────────────┤
│  🏠 MyBlog             │  ← Logo/Branding
│  Personal Tech Blog    │  ← Tagline
├─────────────────────────┤
│  Navigation            │
│  ─────────────         │
│  • Home                │
│  • About               │
│  • Archive (ถ้ามี)      │
├─────────────────────────┤
│  🔍 Search             │  ← Quick search
│  🌙 Dark Mode          │  ← Theme toggle
├─────────────────────────┤
│  Connect               │
│  ─────────────         │
│  GitHub | Twitter | LinkedIn
├─────────────────────────┤
│  v1.0.0                │  ← Version
│  © 2026 MyBlog         │  ← Copyright
└─────────────────────────┘
```

#### Priority: 🟡 Medium

#### Technical Notes
- ใช้ Sheet component จาก shadcn/ui (มีอยู่แล้ว)
- เพิ่ม config สำหรับ social links และ version ใน site config
- ทำให้ reusable สำหรับอนาคต

---

## Phase 4: Code Block Styling Enhancement

### US-018: Code Block & Inline Code Styling
**As a** ผู้อ่านบทความ tech
**I want to** เห็น code blocks และ inline code ที่แตกต่างจาก text ปกติอย่างชัดเจน
**So that** ฉันแยกแยะได้ง่ายว่าส่วนไหนคือ code ที่ต้อง copy ไปใช้

#### ปัญหาปัจจุบัน
- Code blocks ถูก strip ออกจาก DOM (หายไปเลย)
- Inline code ไม่มี styling ใดๆ
- ไม่มี syntax highlighting
- ไม่มีปุ่ม copy code

#### Acceptance Criteria

**Inline Code:**
- [ ] มี background color ที่แตกต่างจาก text ปกติ
- [ ] ใช้ font monospace (Geist Mono)
- [ ] มี padding เล็กน้อย และ border-radius
- [ ] รองรับทั้ง light และ dark mode

**Code Blocks:**
- [ ] แสดง code blocks ที่ถูก render อย่างถูกต้อง (ไม่หายไป)
- [ ] มี Syntax Highlighting ตามภาษา (bash, tsx, css, json, etc.)
- [ ] แสดง label ชื่อภาษา (เช่น "bash", "typescript")
- [ ] มี background color ที่ชัดเจน
- [ ] มี border หรือ shadow เพื่อแยกจาก content
- [ ] มี padding ที่เหมาะสม
- [ ] รองรับ horizontal scroll สำหรับ code ยาว
- [ ] รองรับทั้ง light และ dark mode

**Copy Button:**
- [ ] มีปุ่ม Copy มุมขวาบนของ code block
- [ ] แสดง feedback "Copied!" เมื่อ copy สำเร็จ
- [ ] ใช้ CopyButton component ที่มีอยู่แล้ว

**Typography Plugin:**
- [ ] ติดตั้ง @tailwindcss/typography
- [ ] prose classes ทำงานถูกต้อง

#### Priority: 🔴 High

#### Technical Approach
1. ติดตั้ง `@tailwindcss/typography` plugin
2. ติดตั้ง `shiki` สำหรับ syntax highlighting
3. แก้ไข post rendering logic ใน `posts/[slug]/page.tsx`
4. สร้าง CodeBlock component พร้อม copy button
5. เพิ่ม CSS สำหรับ inline code และ code blocks

#### Design Requirements
- **Inline code**:
  - Light: bg-gray-100, text-gray-800
  - Dark: bg-gray-800, text-gray-200
  - Font: Geist Mono
  - Border-radius: 4px
  - Padding: 2px 6px

- **Code block**:
  - Light: bg-gray-900 (dark background for contrast)
  - Dark: bg-gray-950
  - Border-radius: 8px
  - Padding: 16px
  - Language label: top-left corner
  - Copy button: top-right corner

- **Syntax colors** (ใช้ theme ของ Shiki):
  - Keywords: purple/pink
  - Strings: green
  - Functions: blue
  - Comments: gray
  - Numbers: orange

---

## Phase 5: Content - React สำหรับมือใหม่

### US-019: บทความ React เบื้องต้น สำหรับมือใหม่ 2026
**As a** ผู้เริ่มต้นเรียนรู้ Web Development
**I want to** อ่านบทความ React เบื้องต้นที่ทันสมัยและเข้าใจง่าย
**So that** ฉันสามารถเริ่มต้นเขียน React ได้อย่างมั่นใจ

#### Target Audience
- ผู้ที่มีพื้นฐาน HTML, CSS, JavaScript แล้ว
- ต้องการเริ่มเรียน React เป็นครั้งแรก
- ชอบเรียนรู้แบบ hands-on (ลงมือทำเลย)

#### Acceptance Criteria
- [ ] อธิบาย React คืออะไร ทำไมต้องใช้ในปี 2026
- [ ] แนะนำ prerequisites ที่ต้องรู้ก่อนเรียน React
- [ ] แนะนำให้ใช้ **Vite** (ไม่ใช่ Create React App)
- [ ] อธิบาย JSX พร้อมตัวอย่าง
- [ ] อธิบาย Components (Functional Components เท่านั้น)
- [ ] อธิบาย Props และ State
- [ ] อธิบาย React Hooks พื้นฐาน (useState, useEffect)
- [ ] มี code ตัวอย่างที่ copy ไปใช้ได้เลย
- [ ] มีโปรเจคตัวอย่างให้ทำตาม (Counter App หรือ Todo App)
- [ ] Responsive ทดสอบแล้ว
- [ ] SEO meta tags ครบ

#### Priority: 🔴 High

#### เนื้อหาที่ต้องมี (Outline)

**1. React คืออะไร? (Intro)**
- React คือ JavaScript Library สำหรับสร้าง UI
- สร้างโดย Facebook (Meta)
- ทำไม React ยังคงเป็นที่นิยมในปี 2026
- React 19 มีอะไรใหม่ (overview สั้นๆ)

**2. ก่อนเริ่มต้อง รู้อะไรก่อน? (Prerequisites)**
- HTML พื้นฐาน
- CSS พื้นฐาน
- JavaScript ES6+ (arrow functions, destructuring, modules, async/await)

**3. เริ่มต้นด้วย Vite**
```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```
- อธิบาย project structure
- ⚠️ หมายเหตุ: ไม่แนะนำ Create React App (Legacy)

**4. JSX คืออะไร?**
- Syntax ที่รวม JavaScript + HTML
- ตัวอย่าง JSX พื้นฐาน
- Rules ของ JSX (ต้อง return element เดียว, ใช้ className แทน class)

**5. Components**
- Component คืออะไร (building blocks)
- วิธีสร้าง Functional Component
- การ export/import components
- ตัวอย่าง: สร้าง Greeting component

**6. Props - ส่งข้อมูลให้ Component**
- Props คืออะไร (read-only data)
- วิธีส่ง props
- การใช้ destructuring กับ props
- ตัวอย่าง: UserCard component รับ name, avatar

**7. State - จัดการข้อมูลที่เปลี่ยนแปลง**
- State คืออะไร (mutable data)
- useState Hook
- ตัวอย่าง: Counter App
```jsx
const [count, setCount] = useState(0)
```

**8. useEffect - จัดการ Side Effects**
- Side Effects คืออะไร
- useEffect Hook
- Dependency Array
- Cleanup function
- ตัวอย่าง: Fetch data จาก API

**9. Event Handling**
- onClick, onChange, onSubmit
- ตัวอย่าง: Form handling

**10. โปรเจคตัวอย่าง: Todo App**
- Step-by-step tutorial
- รวม concepts ทั้งหมดที่เรียนมา
- Code เต็มให้ copy

**11. ก้าวต่อไป (Next Steps)**
- เรียนรู้ React Router
- เรียนรู้ State Management (Context, Redux)
- ลองใช้ Next.js
- Resources แนะนำ

#### Technical Notes
- ใช้ React 19 syntax (ไม่ต้อง forwardRef)
- เน้น Functional Components เท่านั้น
- Code ตัวอย่างทุกอันต้อง test ว่าทำงานได้จริง

#### References
- [React Official Docs](https://react.dev)
- [Vite Guide](https://vitejs.dev/guide/)
- React 19.2 Features

---

## Phase 6: Content - Conventional Commits ฉบับสมบูรณ์

### US-020: อัพเดทบทความ Conventional Commits ให้ครบถ้วน
**As a** นักพัฒนาที่ต้องการเรียนรู้ Conventional Commits
**I want to** อ่านคู่มือ Conventional Commits ที่ละเอียดและครบถ้วน
**So that** ฉันสามารถใช้งานได้จริงในทีมและโปรเจคต่างๆ

#### ปัญหาปัจจุบัน
- เนื้อหาสั้นเกินไป (8 sections พื้นฐาน)
- ตัวอย่างน้อย (4 ตัวอย่างสั้นๆ)
- ขาดรายละเอียดการ setup tools
- ไม่มี real-world examples
- ขาดเรื่อง Common Mistakes

#### Acceptance Criteria
- [ ] อธิบายแต่ละ Type พร้อมตัวอย่างละเอียด (feat, fix, docs, style, refactor, perf, test, build, ci, chore)
- [ ] อธิบายการใช้ Scope อย่างถูกต้อง + ตัวอย่าง
- [ ] อธิบาย Body และ Footer พร้อม use cases
- [ ] อธิบาย Breaking Changes ละเอียด (เมื่อไหร่, วิธีเขียน)
- [ ] Commitlint Configuration ละเอียด (rules, extends, custom rules)
- [ ] Husky Setup step-by-step
- [ ] Commitizen (Interactive Commit) setup และใช้งาน
- [ ] Semantic Release overview + basic setup
- [ ] Common Mistakes และวิธีแก้ไข
- [ ] IDE Extensions (VS Code, JetBrains)
- [ ] วิธีแก้ไข Commit ที่ผิด (amend, rebase)
- [ ] Real-world examples จาก popular projects

#### Priority: 🔴 High

#### เนื้อหาที่ต้องมี (Outline)

**1. Intro (ปรับปรุง)**
- Conventional Commits คืออะไร (ขยายเพิ่ม)
- ทำไมถึงสำคัญ (เพิ่มตัวอย่าง)
- ใครใช้บ้าง (Angular, Vue, React, Vite)

**2. รูปแบบ Commit Message (ละเอียด)**
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```
- อธิบายแต่ละส่วนละเอียด
- ความยาวที่แนะนำ (50/72 rule)

**3. Types ทั้งหมดพร้อมตัวอย่างละเอียด (ใหม่)**
| Type | ใช้เมื่อ | ตัวอย่าง |
|------|---------|---------|
| feat | เพิ่ม feature | 3+ ตัวอย่าง |
| fix | แก้ bug | 3+ ตัวอย่าง |
| docs | แก้เอกสาร | 2+ ตัวอย่าง |
| style | formatting | 2+ ตัวอย่าง |
| refactor | ปรับโครงสร้าง | 3+ ตัวอย่าง |
| perf | performance | 2+ ตัวอย่าง |
| test | tests | 2+ ตัวอย่าง |
| build | build system | 2+ ตัวอย่าง |
| ci | CI/CD | 2+ ตัวอย่าง |
| chore | maintenance | 2+ ตัวอย่าง |

**4. Scope - ใช้ยังไงให้ถูก (ใหม่)**
- Scope คืออะไร
- ตัวอย่าง scope ที่ดี vs ไม่ดี
- Common scopes: auth, api, ui, db, config, deps
- เมื่อไหร่ไม่ต้องใช้ scope

**5. Body และ Footer (ใหม่)**
- เมื่อไหร่ต้องใช้ body
- รูปแบบ body ที่ดี
- Footer types: BREAKING CHANGE, Closes, Refs, Co-authored-by
- ตัวอย่าง commit แบบเต็ม

**6. Breaking Changes (ขยาย)**
- เมื่อไหร่ถือว่า breaking
- วิธีเขียน breaking change (! และ BREAKING CHANGE footer)
- ตัวอย่าง real breaking changes

**7. Commitlint Setup (ขยายมาก)**
```bash
npm install -D @commitlint/cli @commitlint/config-conventional
```
- Configuration file ละเอียด
- Custom rules
- Common config options

**8. Husky Setup (ใหม่)**
- ติดตั้ง Husky
- Setup commit-msg hook
- Setup pre-commit hook
- Troubleshooting common issues

**9. Commitizen - Interactive Commit (ใหม่)**
```bash
npm install -D commitizen cz-conventional-changelog
```
- Setup และใช้งาน
- Custom adapter
- ทำไมควรใช้ (enforce format)

**10. Semantic Release Overview (ใหม่)**
- Semantic Release คืออะไร
- ทำงานยังไงกับ Conventional Commits
- Basic setup example
- ตัวอย่าง CHANGELOG ที่ generate อัตโนมัติ

**11. Common Mistakes (ใหม่)**
| ผิด | ถูก | เหตุผล |
|-----|-----|--------|
| `update code` | `feat(auth): add login` | ไม่มี type |
| `feat: Add new Feature` | `feat: add new feature` | ตัวใหญ่ |
| `fix: fixed bug` | `fix: resolve null error` | กริยาไม่ถูก |
| และอื่นๆ... | | |

**12. IDE Extensions (ใหม่)**
- VS Code: Conventional Commits extension
- JetBrains: Git Commit Template
- วิธีใช้งานและ config

**13. แก้ไข Commit ที่ผิด (ใหม่)**
- git commit --amend
- Interactive rebase
- Force push (ข้อควรระวัง)

**14. Real-world Examples (ใหม่)**
- ตัวอย่างจาก Angular
- ตัวอย่างจาก Vue.js
- ตัวอย่างจาก popular GitHub repos

**15. สรุปและ Cheatsheet (ปรับปรุง)**
- Quick reference table
- Links ที่เป็นประโยชน์

#### Technical Notes
- บทความควรยาว ~2500-3000 คำ (จากเดิม ~500 คำ)
- แบ่ง sections ชัดเจน
- มี code blocks copy ได้
- มีตารางสรุป

#### References
- [conventionalcommits.org](https://www.conventionalcommits.org/)
- [Commitlint](https://commitlint.js.org/)
- [Semantic Release](https://semantic-release.gitbook.io/)
- [Commitizen](https://commitizen-tools.github.io/commitizen/)

---

## Phase 7: Content - Microfrontend with Module Federation

### US-021: บทความ Microfrontend แบบ Module Federation
**As a** Frontend Developer ที่ต้องการพัฒนา Large-scale Application
**I want to** อ่านคู่มือ Microfrontend with Module Federation ที่ครบถ้วน
**So that** ฉันสามารถออกแบบและพัฒนา Microfrontend architecture ได้จริง

#### Target Audience
- Frontend Developer ที่มีประสบการณ์ 1+ ปี
- ทีมที่กำลังจะ scale application ให้ใหญ่ขึ้น
- Developer ที่ต้องการแยก codebase ออกเป็น independent modules

#### Acceptance Criteria
- [ ] อธิบาย Microfrontend คืออะไร + ทำไมต้องใช้
- [ ] เปรียบเทียบ Microfrontend approaches (iframes, Web Components, Module Federation)
- [ ] อธิบาย Module Federation concepts (Host, Remote, Shared)
- [ ] อธิบาย Module Federation 2.0 features ใหม่
- [ ] Step-by-step setup Module Federation กับ Webpack 5
- [ ] Step-by-step setup Module Federation กับ Vite (ใช้ @module-federation/vite)
- [ ] อธิบายการ Share dependencies อย่างถูกต้อง (singleton, version strategy)
- [ ] อธิบาย Communication ระหว่าง Microfrontends (Event Bus, Shared State)
- [ ] อธิบาย Routing strategies ใน Microfrontend
- [ ] Common Problems และ Solutions (version mismatch, CSS conflicts, state sync)
- [ ] Best Practices และ Anti-patterns
- [ ] Real-world architecture example
- [ ] Code ตัวอย่างที่ทำงานได้จริง
- [ ] Responsive และ SEO ครบ

#### Priority: 🔴 High

#### เนื้อหาที่ต้องมี (Outline)

**1. Microfrontend คืออะไร? (Intro)**
- Definition: แบ่ง frontend ออกเป็น independent deployable units
- ทำไมต้องใช้ Microfrontend
  - ทีมใหญ่ต้องการ autonomy
  - แยก deploy ได้อิสระ
  - Tech stack flexibility
  - Scale development team ง่ายขึ้น
- เมื่อไหร่ **ไม่ควร** ใช้ (complexity vs benefit)

**2. เปรียบเทียบ Microfrontend Approaches**
| Approach | Pros | Cons | เมื่อไหร่ใช้ |
|----------|------|------|------------|
| iframes | Isolation สูง | Performance, UX | Legacy integration |
| Web Components | Framework-agnostic | Limited styling | Simple widgets |
| Module Federation | Runtime sharing, Performance | Learning curve | Modern apps |
| Import Maps | No bundler lock-in | Limited features | Simple cases |

**3. Module Federation คืออะไร?**
- Webpack 5 feature
- Core concepts:
  - **Host (Container)**: App หลักที่ load remote modules
  - **Remote**: App ที่ expose modules ให้ Host ใช้
  - **Shared**: Dependencies ที่ share ระหว่าง apps
- ข้อดี: Runtime loading, No rebuild required, Share code
- Diagram architecture

**4. Module Federation 2.0 - มีอะไรใหม่? (NEW)**
- Runtime Plugin System
- Standalone Runtime SDK (ไม่ต้อง build tool)
- Dynamic Type Hints (TypeScript support)
- Build tool support: Webpack, Rspack, Vite
- Manifest-based loading
- Official resources: module-federation.io

**5. Setup Module Federation กับ Webpack 5**
```javascript
// Host webpack.config.js
new ModuleFederationPlugin({
  name: 'host',
  remotes: {
    remoteApp: 'remoteApp@http://localhost:3001/remoteEntry.js',
  },
  shared: {
    react: { singleton: true },
    'react-dom': { singleton: true },
  },
});

// Remote webpack.config.js
new ModuleFederationPlugin({
  name: 'remoteApp',
  filename: 'remoteEntry.js',
  exposes: {
    './Button': './src/components/Button',
  },
  shared: {
    react: { singleton: true },
    'react-dom': { singleton: true },
  },
});
```
- Project structure
- Step-by-step configuration
- Loading remote components
- Error boundaries

**6. Setup Module Federation กับ Vite (2026)**
```javascript
// vite.config.js
import { federation } from '@module-federation/vite';

export default {
  plugins: [
    federation({
      name: 'host',
      remotes: {
        remoteApp: 'http://localhost:3001/assets/remoteEntry.js',
      },
      shared: ['react', 'react-dom'],
    }),
  ],
};
```
- @module-federation/vite plugin
- Configuration differences from Webpack
- Rspack alternative

**7. Shared Dependencies Strategy**
- **singleton: true** - มีแค่ 1 instance (React, React DOM)
- **strictVersion** - บังคับ version ตรงกัน
- **requiredVersion** - กำหนด minimum version
- Version mismatch handling
```javascript
shared: {
  react: {
    singleton: true,
    strictVersion: true,
    requiredVersion: '^18.2.0',
  },
}
```
- เมื่อไหร่ใช้แต่ละ option
- Semantic versioning ใน shared deps

**8. Communication ระหว่าง Microfrontends**

| วิธี | Pros | Cons | Use Case |
|-----|------|------|----------|
| Props | Simple, Type-safe | Tight coupling | Parent-child |
| Custom Events | Decoupled | No type safety | Cross-app notifications |
| Event Bus | Organized | Boilerplate | Complex communication |
| Shared State (Redux) | Powerful | Complexity | State sync critical |
| URL/Query params | Universal | Limited data | Navigation state |

```javascript
// Custom Events example
// Remote: dispatch event
window.dispatchEvent(new CustomEvent('cart:add', {
  detail: { productId: 123 }
}));

// Host: listen event
window.addEventListener('cart:add', (e) => {
  console.log(e.detail.productId);
});
```

**9. Routing Strategies**
- Host-based routing (Host controls all routes)
- Nested routing (Each microfrontend has own router)
- Shell routing pattern
- URL synchronization between apps
- Example with React Router

**10. Common Problems และ Solutions**

| Problem | Cause | Solution |
|---------|-------|----------|
| Duplicate React | Singleton not set | `singleton: true` |
| CSS Conflicts | Global styles | CSS Modules, CSS-in-JS |
| Version mismatch | Different versions | `strictVersion` หรือ version sync |
| Slow initial load | Too many remotes | Prefetch, lazy loading |
| Type safety lost | No shared types | shared npm package for types |
| Routing conflicts | Overlapping routes | Route prefix convention |

**11. Best Practices**
✅ Do:
- กำหนด clear contracts ระหว่าง Host และ Remote
- ใช้ Error Boundaries ครอบ remote components
- Preload remote modules ที่ใช้บ่อย
- Share types ผ่าน npm package
- ใช้ singleton สำหรับ framework dependencies
- ตั้ง route prefix ให้แต่ละ microfrontend

❌ Don't:
- อย่า share state เยอะเกินไป (tight coupling)
- อย่าใช้ global CSS โดยไม่มี namespace
- อย่า hard-code remote URLs
- อย่าละเลย error handling
- อย่า expose internal components

**12. Anti-patterns ที่ต้องเลี่ยง**
- Shared everything - ทำให้ coupling สูง
- No error boundaries - crash 1 ที่ ล่มทั้งหมด
- Tight version coupling - deploy ไม่อิสระ
- CSS global pollution - style conflicts
- Circular dependencies - ระหว่าง microfrontends

**13. Real-world Architecture Example**
```
┌─────────────────────────────────────────┐
│           Shell/Host App                │
│   (Routing, Auth, Layout, Header)       │
├─────────┬─────────┬─────────┬──────────┤
│ Product │  Cart   │ Checkout│  Admin   │
│   MFE   │   MFE   │   MFE   │   MFE    │
│(Team A) │(Team B) │(Team C) │ (Team D) │
└─────────┴─────────┴─────────┴──────────┘
         ↓           ↓
    ┌─────────────────────┐
    │   Shared Libraries  │
    │ (Design System, Utils)│
    └─────────────────────┘
```
- E-commerce example
- Team ownership
- Shared design system

**14. Deployment Strategies**
- Independent deployment per MFE
- Versioned remote URLs
- Dynamic remote loading
- CDN considerations
- Rollback strategy

**15. Testing Microfrontends**
- Unit tests (per MFE)
- Integration tests (Host + Remotes)
- E2E tests (full application)
- Contract testing

**16. สรุป Cheatsheet**
- Quick reference configuration
- Decision flowchart: เมื่อไหร่ใช้ Module Federation
- Essential links และ resources

#### Technical Notes
- บทความควรยาว ~3000-3500 คำ
- ใช้ Module Federation 2.0 syntax
- Code examples ต้อง test ว่าทำงานได้จริง

#### 📊 Diagrams Required (สำคัญมาก - ช่วยให้เข้าใจง่าย)

**Diagram 1: Microfrontend vs Monolith Comparison**
```
┌─ Monolith ─────────────────┐    ┌─ Microfrontend ────────────┐
│                            │    │   ┌───┐ ┌───┐ ┌───┐ ┌───┐ │
│    Single Large App        │ vs │   │MFE│ │MFE│ │MFE│ │MFE│ │
│    (One Team Deploy)       │    │   │ A │ │ B │ │ C │ │ D │ │
│                            │    │   └───┘ └───┘ └───┘ └───┘ │
└────────────────────────────┘    │   (Independent Deploy)     │
                                  └────────────────────────────┘
```

**Diagram 2: Module Federation Architecture**
```
┌──────────────────────────────────────────────────────┐
│                    HOST APP                          │
│              (Shell/Container)                       │
│  ┌─────────────────────────────────────────────────┐│
│  │ import RemoteButton from 'remoteApp/Button'     ││
│  └─────────────────────────────────────────────────┘│
│                        │                             │
│              Runtime Load at ▼                       │
├──────────────────────────────────────────────────────┤
│                                                      │
│   ┌──────────────┐  ┌──────────────┐  ┌──────────┐  │
│   │  REMOTE A    │  │  REMOTE B    │  │ REMOTE C │  │
│   │ (Port 3001)  │  │ (Port 3002)  │  │(Port 3003)│  │
│   │              │  │              │  │          │  │
│   │ exposes:     │  │ exposes:     │  │ exposes: │  │
│   │ - Button     │  │ - Header     │  │ - Cart   │  │
│   │ - Card       │  │ - Footer     │  │ - Checkout│ │
│   └──────────────┘  └──────────────┘  └──────────┘  │
│                                                      │
│   ┌─────────────────────────────────────────────────┐│
│   │              SHARED DEPENDENCIES                ││
│   │         React, React-DOM (singleton)            ││
│   └─────────────────────────────────────────────────┘│
└──────────────────────────────────────────────────────┘
```

**Diagram 3: Data Flow / Communication**
```
┌─────────────┐    Custom Event    ┌─────────────┐
│   MFE A     │ ───────────────▶   │   MFE B     │
│  (Product)  │  'cart:add-item'   │   (Cart)    │
└─────────────┘                    └─────────────┘
       │                                  │
       │         Props                    │
       └──────────▶ Host ◀────────────────┘
                     │
              Shared State
              (if needed)
```

**Diagram 4: Deployment Architecture**
```
┌─────────────────────────────────────────────────────────┐
│                        CDN                              │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  host.example.com    mfe-a.example.com  mfe-b.example   │
│        │                    │                 │         │
│        ▼                    ▼                 ▼         │
│   ┌─────────┐         ┌─────────┐       ┌─────────┐    │
│   │  Host   │         │ Remote  │       │ Remote  │    │
│   │  App    │────────▶│   A     │       │   B     │    │
│   │         │ runtime │         │       │         │    │
│   │         │  load   │         │       │         │    │
│   └─────────┘         └─────────┘       └─────────┘    │
│                                                         │
│   Deploy: Team Core   Deploy: Team A   Deploy: Team B  │
│   (independent)        (independent)    (independent)   │
└─────────────────────────────────────────────────────────┘
```

**Diagram 5: Decision Flowchart - ควรใช้ Module Federation ไหม?**
```
                    ┌───────────────────┐
                    │ App ของคุณเป็น    │
                    │ Large-scale ไหม?  │
                    └─────────┬─────────┘
                              │
              ┌───────────────┴───────────────┐
              ▼                               ▼
         ┌────────┐                     ┌────────┐
         │  Yes   │                     │   No   │
         └────┬───┘                     └────┬───┘
              │                              │
              ▼                              ▼
    ┌─────────────────┐            ┌─────────────────┐
    │ มีหลายทีม       │            │ ใช้ Monolith    │
    │ ต้องการ deploy  │            │ ก็เพียงพอ        │
    │ อิสระจากกันไหม? │            └─────────────────┘
    └────────┬────────┘
             │
    ┌────────┴────────┐
    ▼                 ▼
┌────────┐      ┌────────┐
│  Yes   │      │   No   │
└────┬───┘      └────┬───┘
     │               │
     ▼               ▼
┌──────────────┐ ┌──────────────┐
│ ✅ ใช้       │ │ ❓ พิจารณา   │
│ Module       │ │ ข้อดี/ข้อเสีย│
│ Federation   │ │ ก่อนตัดสินใจ │
└──────────────┘ └──────────────┘
```

> **Note to Designer**: Diagrams เหล่านี้เป็น ASCII art สำหรับ reference
> Designer สามารถทำเป็น SVG หรือ Image ที่สวยงามกว่านี้ได้

#### Research Findings

**Sources:**
- [Webpack Module Federation](https://webpack.js.org/concepts/module-federation/)
- [Module Federation 2.0](https://module-federation.io/guide/start/)
- [LogRocket Tutorial](https://blog.logrocket.com/building-micro-frontends-webpacks-module-federation/)
- [State Management in MFE](https://www.burhanuday.com/blog/2023/05/state-management-in-micro-frontends)
- [Rspack Module Federation](https://rspack.rs/guide/features/module-federation)

---

*Last updated: 2026-02-02*
