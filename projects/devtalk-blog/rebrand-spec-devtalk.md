# Rebrand Spec: MyBlog → DevTalk

**Task**: Rebrand เว็บไซต์จาก MyBlog เป็น DevTalk
**Owner**: @Designer → @Developer
**Priority**: 🔴 High
**Created by**: @PM
**Date**: 2026-02-01

---

## Brand Identity

### ชื่อใหม่
- **Name**: DevTalk
- **Tagline**: "พูดคุยเรื่อง Dev แบบเข้าใจง่าย" หรือ "Developer Conversations"

### Logo Concept
จากภาพที่ได้รับ:
- **รูปแบบ**: Speech bubble (กรอบโค้งมนแบบ chat bubble)
- **สัญลักษณ์**: `</>` (code tag) อยู่ตรงกลาง
- **สี**: น้ำเงิน (#4F7CFF หรือใกล้เคียง)
- **พื้นหลัง**: ฟ้าอ่อน/ขาว
- **ความหมาย**: การสนทนา + Programming = DevTalk

### Color Palette (Suggested)
| Color | Hex | Usage |
|-------|-----|-------|
| Primary Blue | #4F7CFF | Logo, Links, Buttons |
| Light Blue | #E8EEFF | Background, Hover states |
| Dark Blue | #1E3A8A | Text emphasis |
| White | #FFFFFF | Background |
| Gray | #6B7280 | Secondary text |

---

## Files to Update

### 1. Site Config
**File**: `src/config/site.ts`
```typescript
export const siteConfig = {
  name: "DevTalk",
  tagline: "พูดคุยเรื่อง Dev แบบเข้าใจง่าย",
  // ... rest unchanged
};
```

### 2. Layout Metadata
**File**: `src/app/layout.tsx`
```typescript
title: "DevTalk - พูดคุยเรื่อง Dev แบบเข้าใจง่าย",
```

### 3. Home Page
**File**: `src/app/page.tsx`
```
Welcome to DevTalk
```

### 4. Footer
**File**: `src/components/Footer.tsx`
```
© {year} DevTalk. All rights reserved.
```

### 5. Post Page
**File**: `src/app/posts/[slug]/page.tsx`
```typescript
title: `${post.title} | DevTalk`,
```

### 6. About Page
**File**: `src/app/about/page.tsx`
```typescript
title: "About | DevTalk",
```

---

## Logo Implementation

### Option A: SVG Component (Recommended)
สร้าง `src/components/Logo.tsx`:
```tsx
// Speech bubble with </> code symbol
// สีน้ำเงิน gradient หรือ solid
// ขนาด responsive
```

### Option B: Image File
- สร้าง `public/logo.svg` หรือ `public/logo.png`
- ใช้ใน Header/Navigation

### Logo Variations Needed
1. **Full Logo**: Icon + Text "DevTalk"
2. **Icon Only**: Speech bubble + `</>` (สำหรับ mobile/favicon)
3. **Favicon**: 32x32, 16x16 versions

---

## Design Tasks for @Designer

- [ ] ออกแบบ Logo SVG ตามภาพต้นแบบ
- [ ] กำหนด Color Palette อย่างเป็นทางการ
- [ ] ออกแบบ Favicon
- [ ] ระบุ Typography (ถ้าต้องการเปลี่ยน)
- [ ] อัพเดท Design System doc (ถ้ามี)

---

## Development Tasks for @Developer

- [ ] อัพเดท `site.ts` config
- [ ] อัพเดท metadata ทุกหน้า
- [ ] สร้าง Logo component
- [ ] อัพเดท Favicon
- [ ] อัพเดท Footer copyright
- [ ] Build และทดสอบ

---

## Acceptance Criteria

- [ ] ชื่อ "DevTalk" แสดงถูกต้องทุกที่
- [ ] Logo ใหม่แสดงใน Header
- [ ] Favicon อัพเดทแล้ว
- [ ] ไม่มี "MyBlog" หลงเหลือในโปรเจค
- [ ] สีสอดคล้องกับ brand identity
- [ ] Build ผ่าน ไม่มี errors

---

*Created by @PM | 2026-02-01*
