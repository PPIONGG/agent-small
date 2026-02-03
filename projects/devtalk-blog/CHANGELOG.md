# Changelog

รูปแบบตาม [Keep a Changelog](https://keepachangelog.com/)

---

## [1.1.0] - 2026-02-02

### Added
- **บทความใหม่: Microfrontend Module Federation** (~3000 คำ, 16 sections)
  - อธิบาย Microfrontend Architecture
  - Module Federation concepts (Host, Remote, Shared)
  - Module Federation 2.0 features
  - Setup กับ Webpack 5 และ Vite
  - Best Practices และ Anti-patterns
- **บทความใหม่: React เบื้องต้น สำหรับมือใหม่ 2026** (~2000 คำ)
  - JSX, Components, Props, State
  - React Hooks (useState, useEffect)
  - โปรเจค Todo App
- **อัพเดทบทความ: Conventional Commits ฉบับสมบูรณ์** (~3000 คำ)
  - เพิ่ม Commitlint, Husky, Commitizen setup
  - เพิ่ม Semantic Release overview
  - เพิ่ม Common Mistakes และ Real-world examples
- **Components ใหม่**:
  - `Table.tsx` - แสดงตารางจาก markdown
  - `Callout.tsx` - แสดง TIP/WARNING/DANGER boxes
- **parseContent.tsx** - รองรับ Table และ Callout parsing

### Changed
- ลดจำนวนบทความเหลือ 4 บทความ (จาก 10+)
- ปรับปรุงโครงสร้างเนื้อหาให้ละเอียดขึ้น

### Deployment
- **Platform**: Vercel
- **URL**: https://devtalk-blog.vercel.app
- **Deployed by**: @DevOps

---

## [1.0.0] - 2026-02-01

### Added
- **Rebrand: DevTalk** - ชื่อใหม่พร้อม Logo SVG (speech bubble + `</>` gradient)
- **Dashboard Page** - สถิติบทความ, Tag Chart, Category Chart, Tag Cloud, Recent Posts
- **Code Block Styling** - Shiki syntax highlighting, copy button, line numbers
- **Mobile Navigation** - Hamburger menu, theme toggle, responsive design
- **Reading Experience Features**:
  - Dark Mode Toggle
  - Reading Progress Bar
  - Reading Time Estimate
  - Back to Top Button
  - Search Dialog (Cmd+K)
- **บทความ**:
  - Ant Design (Antd) เข้าใจง่าย
  - Conventional Commits Guide (ฉบับสมบูรณ์)

### Tech Stack
- Next.js 16 (App Router)
- React 19
- Tailwind CSS v4
- shadcn/ui components
- Shiki (syntax highlighting)
- TypeScript

### Deployment
- **Platform**: Vercel
- **URL**: https://devtalk-blog.vercel.app
- **Auto Deploy**: Push to `master` branch

---

## [0.0.1] - 2026-02-01

### Added
- Initial project setup
- PM สร้าง specs.md, TODO.md, CHANGELOG.md
