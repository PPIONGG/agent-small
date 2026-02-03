# Design Specs: Code Block Styling Enhancement

> **Feature**: US-018 - Code Block & Inline Code Styling
> **Designer**: @Designer
> **Date**: 2026-02-01
> **Status**: Ready for Development

---

## Design Research Summary

### Existing Design System
- **Colors**: OKLCH color space with light/dark mode
- **Fonts**: Geist Sans (body), Geist Mono (code)
- **Border Radius**: 0.625rem base (10px)
- **Dark Mode**: next-themes with `.dark` class
- **CopyButton**: Already implemented with feedback

### Best Practices Applied
- Use `#121212` background for dark (not pure black) - reduces eye strain
- 4.5:1 contrast ratio minimum (WCAG AA)
- DuoTone approach for syntax colors
- Subtle inline code styling

---

## Component 1: Inline Code

### Visual Reference
```
Normal text นี้คือ `inline code` ที่เห็นชัดเจน
```

### Specifications

| Property | Light Mode | Dark Mode |
|----------|------------|-----------|
| Background | `oklch(0.95 0 0)` / #f1f1f1 | `oklch(0.25 0 0)` / #3d3d3d |
| Text Color | inherit (ไม่เปลี่ยน) | inherit |
| Font Family | Geist Mono | Geist Mono |
| Font Size | 0.875em (14px if base 16px) | 0.875em |
| Padding | 0.2em 0.4em | 0.2em 0.4em |
| Border Radius | 4px | 4px |
| Border | none | none |

### CSS Implementation
```css
:not(pre) > code {
  font-family: var(--font-geist-mono);
  font-size: 0.875em;
  padding: 0.2em 0.4em;
  border-radius: 4px;
  background-color: oklch(0.95 0 0);
  color: inherit;
}

.dark :not(pre) > code {
  background-color: oklch(0.25 0 0);
}
```

### States
- **Default**: ตามที่ระบุด้านบน
- **Selection**: ใช้ browser default

---

## Component 2: Code Block

### Visual Reference (ASCII Wireframe)
```
┌──────────────────────────────────────────────────┐
│  typescript                          [Copy btn]  │  ← Header
├──────────────────────────────────────────────────┤
│                                                  │
│  const greeting = "Hello World";                 │
│  function sayHello() {                           │
│    console.log(greeting);                        │
│  }                                               │
│                                                  │
│  ──────────────────────────────────►  scroll     │
└──────────────────────────────────────────────────┘
```

### Layout Specifications

| Element | Value |
|---------|-------|
| Container Width | 100% |
| Container Margin | 1.5rem 0 (24px) |
| Border Radius | 8px |
| Box Shadow | `0 4px 6px -1px rgba(0, 0, 0, 0.1)` |
| Overflow | hidden (container), auto-x (code) |

### Header Bar

| Property | Value |
|----------|-------|
| Height | auto (padding controlled) |
| Padding | 8px 16px |
| Background Light | `oklch(0.92 0 0)` / #e8e8e8 |
| Background Dark | `oklch(0.18 0 0)` / #2a2a2a |
| Border Bottom | 1px solid `oklch(0.85 0 0)` / `oklch(0.25 0 0)` |
| Display | flex, justify-between, align-center |

### Language Label

| Property | Value |
|----------|-------|
| Font Family | Geist Sans (NOT mono) |
| Font Size | 11px |
| Font Weight | 600 |
| Text Transform | uppercase |
| Letter Spacing | 0.5px |
| Color Light | `oklch(0.45 0 0)` / #6b7280 |
| Color Dark | `oklch(0.65 0 0)` / #9ca3af |

### Code Area

| Property | Light Mode | Dark Mode |
|----------|------------|-----------|
| Background | `oklch(0.12 0 0)` / #1e1e1e | `oklch(0.10 0 0)` / #1a1a1a |
| Padding | 16px | 16px |
| Font Family | Geist Mono | Geist Mono |
| Font Size | 14px | 14px |
| Line Height | 1.6 | 1.6 |
| Text Color | `oklch(0.9 0 0)` / #e5e5e5 | `oklch(0.9 0 0)` / #e5e5e5 |

**Note**: Code block background เป็นสีเข้มทั้ง light และ dark mode เพื่อความ contrast ที่ดี

### Scrollbar Styling

| Property | Value |
|----------|-------|
| Height | 8px |
| Track | `rgba(255, 255, 255, 0.05)` |
| Thumb | `rgba(255, 255, 255, 0.2)` |
| Thumb Radius | 4px |
| Thumb Hover | `rgba(255, 255, 255, 0.3)` |

---

## Component 3: Copy Button

### Using Existing CopyButton Component

CopyButton component มีอยู่แล้วที่ `src/components/CopyButton.tsx`

### Position & Sizing

| Property | Value |
|----------|-------|
| Position | Absolute, top-right of header |
| Size | 32px x 32px (h-8 w-8) |
| Icon Size | 16px (h-4 w-4) |

### States

| State | Background | Icon | Color |
|-------|------------|------|-------|
| Default | transparent | Copy | `oklch(0.55 0 0)` |
| Hover | `rgba(255,255,255,0.1)` | Copy | `oklch(0.75 0 0)` |
| Active | `rgba(255,255,255,0.15)` | Copy | `oklch(0.85 0 0)` |
| Copied | `rgba(34,197,94,0.2)` | Check | `#22c55e` (green-500) |
| Focus | ring-2 ring-ring | - | - |

### Animation

```css
.copy-button {
  transition: all 0.15s ease;
}

.copy-button-icon {
  transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1),
              opacity 0.15s ease;
}
```

### Feedback Duration
- Success state: **2 seconds** (already implemented)

---

## Syntax Highlighting (Shiki)

### Recommended Theme
ใช้ **GitHub Dark** theme จาก Shiki เพราะ:
- ออกแบบมาสำหรับ code
- Contrast ดี
- รองรับหลายภาษา

### Color Tokens

| Token Type | Color (GitHub Dark) |
|------------|---------------------|
| Keyword | `#ff7b72` (red/coral) |
| String | `#a5d6ff` (light blue) |
| Function | `#d2a8ff` (purple) |
| Variable | `#ffa657` (orange) |
| Comment | `#8b949e` (gray) |
| Number | `#79c0ff` (blue) |
| Operator | `#ff7b72` (red/coral) |
| Punctuation | `#c9d1d9` (light gray) |

### Alternative: DuoTone Theme
ถ้าต้องการ minimal look:
- **Hue 1** (Important): Purple/Blue tones
- **Hue 2** (Less important): Gray tones

---

## Language Label Mapping

| Code | Display Label |
|------|---------------|
| `ts` | TypeScript |
| `tsx` | React TSX |
| `js` | JavaScript |
| `jsx` | React JSX |
| `css` | CSS |
| `html` | HTML |
| `json` | JSON |
| `bash` | Bash |
| `sh` | Shell |
| `py` | Python |
| `go` | Go |
| `rust` | Rust |
| `sql` | SQL |
| `yaml` | YAML |
| `md` | Markdown |
| (none) | Code |

---

## Responsive Behavior

### Mobile (< 640px)
- Code block full width
- Font size: 13px
- Padding: 12px
- Horizontal scroll enabled

### Tablet (640px - 1024px)
- Same as desktop

### Desktop (> 1024px)
- Max-width follows prose container
- Font size: 14px
- Padding: 16px

---

## Accessibility Checklist

- [x] Contrast ratio >= 4.5:1 for all text
- [x] Focus states visible (ring)
- [x] Keyboard accessible copy button
- [x] aria-label on copy button
- [x] aria-live for copy feedback
- [x] Scrollable with keyboard
- [x] No reliance on color alone (icons + text)

---

## Component Structure (For Developer)

```
CodeBlock/
├── CodeBlock.tsx          # Main wrapper
│   ├── CodeBlockHeader    # Header with language + copy
│   │   ├── LanguageLabel  # Language display
│   │   └── CopyButton     # Existing component
│   └── CodeBlockContent   # Syntax highlighted code
└── styles in globals.css  # Or Tailwind classes
```

### Props Interface
```typescript
interface CodeBlockProps {
  code: string;
  language?: string;
  showLineNumbers?: boolean;  // optional, default false
  filename?: string;          // optional, for file tabs
}
```

---

## Implementation Notes

### Dependencies to Install
```bash
npm install shiki
# or
npm install @shikijs/core
```

### Integration Points
1. แก้ไข `posts/[slug]/page.tsx` - render code blocks
2. สร้าง `CodeBlock` component ใหม่
3. ใช้ `CopyButton` component ที่มีอยู่
4. เพิ่ม CSS ใน `globals.css`

### Known Limitation
- Shiki ต้อง highlight บน server-side (RSC supported)
- ถ้าใช้ client-side ต้องใช้ `shiki/bundle/web`

---

## Handoff Checklist (Designer -> Developer)

- [x] Layout specifications complete
- [x] Colors defined (light/dark)
- [x] Typography specified
- [x] Component structure documented
- [x] States defined (default, hover, active, copied)
- [x] Responsive behavior documented
- [x] Accessibility requirements listed
- [x] Dependencies identified
- [x] Integration points noted

---

*Design by @Designer | 2026-02-01*
