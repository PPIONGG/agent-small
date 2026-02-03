# Design Specs: Mobile Navigation Enhancement

> US-017: Mobile Navigation ที่สมบูรณ์

---

## Overview

ปรับปรุง Mobile Navigation ให้สวยงาม มีข้อมูลครบถ้วน และน่าใช้งานมากขึ้น

**Before**: มีแค่ 2 links (Home, About)
**After**: มี Branding, Nav Links, Actions, Social Links, Footer Info

---

## Visual Design

### Layout Structure

```
┌─────────────────────────────────────┐
│                              ✕      │  ← Close button (มุมขวาบน)
├─────────────────────────────────────┤
│                                     │
│   🏠 MyBlog                        │  ← Logo (text-xl, font-bold)
│   Personal Tech Blog               │  ← Tagline (text-sm, text-muted)
│                                     │
├─────────────────────────────────────┤
│   MENU                              │  ← Section label (text-xs, uppercase)
│   ─────────────────────────────     │
│   🏠  Home                          │  ← Nav item with icon
│   👤  About                         │
│   📚  Archive                       │  ← (ถ้ามีในอนาคต)
│                                     │
├─────────────────────────────────────┤
│   ACTIONS                           │
│   ─────────────────────────────     │
│   🔍  Search                        │  ← Opens SearchDialog
│   🌙  Dark Mode              [ON]   │  ← Toggle switch
│                                     │
├─────────────────────────────────────┤
│   CONNECT                           │
│   ─────────────────────────────     │
│                                     │
│   [GitHub]  [Twitter]  [LinkedIn]   │  ← Icon buttons in a row
│                                     │
├─────────────────────────────────────┤
│                                     │
│   v1.0.0  •  © 2026 MyBlog         │  ← Footer (text-xs, text-muted)
│                                     │
└─────────────────────────────────────┘
```

---

## Component Specs

### 1. Sheet Container (SheetContent)

```css
/* Layout */
width: 100%;
max-width: 320px;
height: 100vh;
padding: 24px;

/* Background */
background: var(--background);
border-left: 1px solid var(--border);

/* Sections */
display: flex;
flex-direction: column;
gap: 24px;
```

### 2. Branding Section

```
┌─────────────────────────────────────┐
│   🏠 MyBlog                        │
│   Personal Tech Blog               │
└─────────────────────────────────────┘
```

| Element | Spec |
|---------|------|
| Logo text | `text-xl`, `font-bold`, `text-primary` |
| Tagline | `text-sm`, `text-muted-foreground` |
| Container | `flex flex-col gap-1` |
| Margin bottom | `mb-6` |

### 3. Section Label

```css
/* "MENU", "ACTIONS", "CONNECT" */
font-size: 12px (text-xs);
font-weight: 600;
text-transform: uppercase;
letter-spacing: 0.05em;
color: var(--text-muted);
margin-bottom: 12px;
```

### 4. Navigation Items

```
┌─────────────────────────────────────┐
│   🏠  Home                          │
└─────────────────────────────────────┘
```

| State | Style |
|-------|-------|
| Default | `text-foreground`, `bg-transparent` |
| Hover | `bg-muted`, `text-primary` |
| Active | `bg-primary/10`, `text-primary`, `font-medium` |

```css
/* Nav Item */
display: flex;
align-items: center;
gap: 12px;
padding: 12px 16px;
border-radius: 8px;
font-size: 16px;
transition: all 0.2s ease;

/* Icon */
width: 20px;
height: 20px;
color: currentColor;
```

### 5. Action Items

#### Search Button
```tsx
<button className="flex items-center gap-3 w-full p-3 rounded-lg hover:bg-muted">
  <Search className="h-5 w-5" />
  <span>Search</span>
  <kbd className="ml-auto text-xs bg-muted px-2 py-1 rounded">⌘K</kbd>
</button>
```

#### Theme Toggle
```tsx
<div className="flex items-center justify-between p-3 rounded-lg hover:bg-muted">
  <div className="flex items-center gap-3">
    <Moon className="h-5 w-5" />
    <span>Dark Mode</span>
  </div>
  <Switch checked={isDark} onCheckedChange={toggleTheme} />
</div>
```

### 6. Social Links

```
┌─────────────────────────────────────┐
│   [GitHub]  [Twitter]  [LinkedIn]   │
└─────────────────────────────────────┘
```

| Element | Spec |
|---------|------|
| Container | `flex gap-2` |
| Button | `h-10 w-10`, `rounded-full`, `variant="ghost"` |
| Icon | `h-5 w-5` |
| Hover | `bg-muted`, `text-primary` |

### 7. Footer Info

```css
/* Version + Copyright */
font-size: 12px (text-xs);
color: var(--text-muted);
text-align: center;
margin-top: auto;  /* Push to bottom */
padding-top: 24px;
border-top: 1px solid var(--border);
```

---

## Colors (ใช้ตาม Design System เดิม)

| Element | Light Mode | Dark Mode |
|---------|------------|-----------|
| Background | `#FFFFFF` | `#0A0A0A` |
| Text primary | `#111827` | `#FAFAFA` |
| Text muted | `#9CA3AF` | `#6B7280` |
| Border | `#E5E7EB` | `#27272A` |
| Primary | `#6366F1` | `#818CF8` |
| Hover bg | `#F3F4F6` | `#27272A` |

---

## Typography

| Element | Size | Weight | Line Height |
|---------|------|--------|-------------|
| Logo | 20px (`text-xl`) | 700 | 1.2 |
| Tagline | 14px (`text-sm`) | 400 | 1.5 |
| Section label | 12px (`text-xs`) | 600 | 1.5 |
| Nav item | 16px (`text-base`) | 500 | 1.5 |
| Footer | 12px (`text-xs`) | 400 | 1.5 |

---

## Spacing

```
Sheet padding: 24px (p-6)

Section gap: 24px (gap-6)

Section label mb: 12px (mb-3)

Nav item padding: 12px 16px (py-3 px-4)
Nav item gap (icon-text): 12px (gap-3)

Social buttons gap: 8px (gap-2)

Footer pt: 24px (pt-6)
Footer border-top: 1px
```

---

## Icons (Lucide)

| Usage | Icon | Size |
|-------|------|------|
| Close | `X` | 24px |
| Home | `Home` | 20px |
| About | `User` | 20px |
| Archive | `Archive` | 20px |
| Search | `Search` | 20px |
| Dark mode | `Moon` / `Sun` | 20px |
| GitHub | `Github` | 20px |
| Twitter | `Twitter` | 20px |
| LinkedIn | `Linkedin` | 20px |

---

## Interactions & Animations

### Sheet Open/Close
```css
/* shadcn/ui Sheet มี animation มาให้แล้ว */
animation: slide-in-from-right 0.3s ease-out;
```

### Nav Item Hover
```css
transition: all 0.2s ease;
/* Hover: scale(1.02), bg-muted */
```

### Theme Toggle
```css
/* Switch component มี animation มาให้แล้ว */
transition: background-color 0.2s, transform 0.2s;
```

### Social Icons Hover
```css
transition: all 0.2s ease;
/* Hover: scale(1.1), color: primary */
```

---

## Accessibility

- [ ] Focus ring visible (`ring-2 ring-primary ring-offset-2`)
- [ ] Touch targets >= 44px (nav items, buttons)
- [ ] Aria labels สำหรับ icon buttons
- [ ] Close button มี `aria-label="Close menu"`
- [ ] Keyboard navigation (Tab, Enter, Escape)
- [ ] Screen reader: SheetTitle visible หรือ sr-only

---

## Site Config (แนะนำ)

สร้างไฟล์ `src/config/site.ts` สำหรับจัดการข้อมูล:

```typescript
export const siteConfig = {
  name: "MyBlog",
  tagline: "Personal Tech Blog",
  version: "1.0.0",
  author: "Your Name",
  social: {
    github: "https://github.com/yourusername",
    twitter: "https://twitter.com/yourusername",
    linkedin: "https://linkedin.com/in/yourusername",
  },
  navItems: [
    { href: "/", label: "Home", icon: "Home" },
    { href: "/about", label: "About", icon: "User" },
    // { href: "/archive", label: "Archive", icon: "Archive" },
  ],
};
```

---

## Component Structure

```tsx
// Header.tsx - Mobile Navigation section

<Sheet>
  <SheetTrigger asChild>
    <Button variant="ghost" size="icon">
      <Menu className="h-5 w-5" />
    </Button>
  </SheetTrigger>

  <SheetContent side="right" className="w-[320px] flex flex-col">
    {/* Branding */}
    <div className="mb-6">
      <h2 className="text-xl font-bold text-primary">{siteConfig.name}</h2>
      <p className="text-sm text-muted-foreground">{siteConfig.tagline}</p>
    </div>

    {/* Navigation */}
    <div className="space-y-1">
      <p className="text-xs font-semibold uppercase text-muted-foreground mb-3">Menu</p>
      {navItems.map(item => (
        <NavItem key={item.href} {...item} />
      ))}
    </div>

    {/* Actions */}
    <div className="space-y-1 mt-6">
      <p className="text-xs font-semibold uppercase text-muted-foreground mb-3">Actions</p>
      <SearchButton />
      <ThemeToggleRow />
    </div>

    {/* Social */}
    <div className="mt-6">
      <p className="text-xs font-semibold uppercase text-muted-foreground mb-3">Connect</p>
      <SocialLinks />
    </div>

    {/* Footer */}
    <div className="mt-auto pt-6 border-t text-center text-xs text-muted-foreground">
      <p>v{siteConfig.version} • © 2026 {siteConfig.name}</p>
    </div>
  </SheetContent>
</Sheet>
```

---

## Handoff Checklist (Designer → Developer)

- [x] Layout structure defined
- [x] Colors specified (hex codes)
- [x] Typography specs (sizes, weights)
- [x] Spacing system (Tailwind classes)
- [x] Component structure
- [x] States (default, hover, active)
- [x] Icons list (Lucide)
- [x] Animations/transitions
- [x] Accessibility requirements
- [x] Site config structure

---

*Created by: @Designer*
*Date: 2026-02-01*
*Status: Ready for Development*
