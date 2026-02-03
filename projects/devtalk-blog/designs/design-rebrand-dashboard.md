# Design Specs: DevTalk Rebrand + Dashboard

**Task**: Design specs สำหรับ Rebrand และ Dashboard
**Owner**: @Designer → @Developer
**Priority**: High
**Created by**: @Designer
**Date**: 2026-02-01

---

## Part 1: DevTalk Branding

### Logo Design

#### Logo SVG Code

```svg
<!-- Full Logo: Icon + Text -->
<svg width="180" height="48" viewBox="0 0 180 48" fill="none" xmlns="http://www.w3.org/2000/svg">
  <!-- Speech Bubble -->
  <path d="M4 8C4 5.79086 5.79086 4 8 4H40C42.2091 4 44 5.79086 44 8V32C44 34.2091 42.2091 36 40 36H28L24 44L20 36H8C5.79086 36 4 34.2091 4 32V8Z" fill="url(#gradient)"/>

  <!-- Code Symbol </> -->
  <text x="24" y="25" text-anchor="middle" font-family="monospace" font-size="14" font-weight="bold" fill="white">&lt;/&gt;</text>

  <!-- DevTalk Text -->
  <text x="56" y="30" font-family="system-ui, sans-serif" font-size="24" font-weight="700" fill="#1E3A8A">Dev</text>
  <text x="96" y="30" font-family="system-ui, sans-serif" font-size="24" font-weight="700" fill="#4F7CFF">Talk</text>

  <defs>
    <linearGradient id="gradient" x1="4" y1="4" x2="44" y2="44" gradientUnits="userSpaceOnUse">
      <stop stop-color="#4F7CFF"/>
      <stop offset="1" stop-color="#93B4FF"/>
    </linearGradient>
  </defs>
</svg>
```

#### Icon Only (for Favicon/Mobile)

```svg
<!-- Icon Only: 48x48 -->
<svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
  <!-- Speech Bubble -->
  <path d="M4 8C4 5.79086 5.79086 4 8 4H40C42.2091 4 44 5.79086 44 8V32C44 34.2091 42.2091 36 40 36H28L24 44L20 36H8C5.79086 36 4 34.2091 4 32V8Z" fill="url(#iconGradient)"/>

  <!-- Code Symbol </> -->
  <text x="24" y="25" text-anchor="middle" font-family="monospace" font-size="14" font-weight="bold" fill="white">&lt;/&gt;</text>

  <defs>
    <linearGradient id="iconGradient" x1="4" y1="4" x2="44" y2="44" gradientUnits="userSpaceOnUse">
      <stop stop-color="#4F7CFF"/>
      <stop offset="1" stop-color="#93B4FF"/>
    </linearGradient>
  </defs>
</svg>
```

### Logo React Component

**File**: `src/components/Logo.tsx`

```tsx
interface LogoProps {
  variant?: 'full' | 'icon';
  size?: 'sm' | 'md' | 'lg';
  className?: string;
}

// Size mappings:
// sm: icon=24px, full=120px
// md: icon=32px, full=160px
// lg: icon=48px, full=200px
```

---

## Color Palette (Official)

### Brand Colors (Hex + OKLCH)

| Name | Hex | OKLCH | Usage |
|------|-----|-------|-------|
| Primary Blue | #4F7CFF | `oklch(0.65 0.18 260)` | Logo, Links, Buttons, Charts |
| Light Blue | #93B4FF | `oklch(0.78 0.12 260)` | Gradient end, Hover states |
| Pale Blue | #E8EEFF | `oklch(0.95 0.03 260)` | Backgrounds, Card hover |
| Dark Blue | #1E3A8A | `oklch(0.35 0.12 260)` | Text emphasis, "Dev" text |
| White | #FFFFFF | `oklch(1 0 0)` | Backgrounds |
| Gray 500 | #6B7280 | `oklch(0.556 0 0)` | Secondary text |
| Gray 900 | #111827 | `oklch(0.205 0 0)` | Primary text |

### CSS Variables to Add

```css
/* DevTalk Brand Colors */
--devtalk-primary: oklch(0.65 0.18 260);
--devtalk-primary-light: oklch(0.78 0.12 260);
--devtalk-primary-pale: oklch(0.95 0.03 260);
--devtalk-primary-dark: oklch(0.35 0.12 260);

/* Chart Colors (using brand) */
--chart-1: oklch(0.65 0.18 260);  /* Primary Blue */
--chart-2: oklch(0.70 0.15 200);  /* Teal */
--chart-3: oklch(0.75 0.12 160);  /* Green */
--chart-4: oklch(0.68 0.16 320);  /* Purple */
--chart-5: oklch(0.72 0.14 30);   /* Orange */
```

### Dark Mode Adjustments

```css
.dark {
  --devtalk-primary: oklch(0.70 0.15 260);
  --devtalk-primary-light: oklch(0.55 0.12 260);
  --devtalk-primary-pale: oklch(0.25 0.05 260);
  --devtalk-primary-dark: oklch(0.85 0.08 260);
}
```

---

## Part 2: Dashboard Design

### Page Layout

```
┌──────────────────────────────────────────────────────────────────┐
│  Header (existing - add Dashboard nav)                           │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  📊 DevTalk Dashboard                          (h1)        │  │
│  │  ดูสถิติการเขียน blog ของคุณ                   (subtitle)  │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐            │
│  │  📝 5    │ │  🏷️ 12   │ │  📂 3    │ │ 📅 Feb 1 │  (gap-4)  │
│  │  Posts   │ │  Tags    │ │ Category │ │  Latest  │            │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘            │
│                                                                  │
│  ┌─────────────────────────────┐ ┌──────────────────────────┐   │
│  │  📈 Tech Stack Popularity   │ │  📂 Posts by Category    │   │
│  │  ───────────────────────    │ │  ────────────────────    │   │
│  │  React     ████████████  4  │ │                          │   │
│  │  Next.js   █████████     3  │ │    Development  60%      │   │
│  │  TypeScript██████        2  │ │    Frontend     40%      │   │
│  │  Git       ████          2  │ │                          │   │
│  │  JavaScript███           1  │ │  [Horizontal bars]       │   │
│  │  Tailwind  ███           1  │ │                          │   │
│  └─────────────────────────────┘ └──────────────────────────┘   │
│                                           (grid 2 cols)          │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  🏷️ All Tags                                               │  │
│  │  ──────────────────────────────────────────────            │  │
│  │  React(4)  Next.js(3)  TypeScript(2)  Git(2)               │  │
│  │  JavaScript(1)  Tailwind(1)  CSS(1)  Antd(1)               │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  📝 Recent Posts                                           │  │
│  │  ──────────────────────────────────────────────            │  │
│  │  • Ant Design คู่มือ...                        Feb 1       │  │
│  │  • Conventional Commits: คู่มือ...             Feb 1       │  │
│  │  • TypeScript สำหรับ React...                  Jan 25      │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  Footer (existing)                                               │
└──────────────────────────────────────────────────────────────────┘
```

---

## Component Specs

### 1. StatCard Component

**File**: `src/components/dashboard/StatCard.tsx`

#### Layout
```
┌─────────────────────────┐
│  [Icon]      Value      │  <- flex items-center justify-between
│  Label                  │  <- text-muted-foreground
└─────────────────────────┘
```

#### Specs
| Property | Value |
|----------|-------|
| Width | `flex-1` (expands equally in grid) |
| Min Width | `150px` |
| Padding | `p-4` (16px) |
| Border Radius | `rounded-xl` (--radius-xl) |
| Background | `bg-card` (white / dark:gray-800) |
| Border | `border border-border` |
| Shadow | `shadow-sm` |

#### Typography
| Element | Style |
|---------|-------|
| Value | `text-3xl font-bold text-foreground` |
| Label | `text-sm text-muted-foreground` |
| Icon | `size-5 text-devtalk-primary` |

#### States
- **Default**: `bg-card`
- **Hover**: `hover:bg-devtalk-primary/5 hover:border-devtalk-primary/20 transition-colors`

#### Dark Mode
- Background: `dark:bg-card`
- Border: `dark:border-border`
- Icon: maintains brand color

---

### 2. TagChart Component (Bar Chart)

**File**: `src/components/dashboard/TagChart.tsx`

#### Layout
```
┌───────────────────────────────────────┐
│  📈 Tech Stack Popularity      (h3)   │
├───────────────────────────────────────┤
│                                       │
│  React        ██████████████████  4   │
│  Next.js      █████████████       3   │
│  TypeScript   ████████            2   │
│  Git          ████████            2   │
│  JavaScript   ████                1   │
│                                       │
└───────────────────────────────────────┘
```

#### Container Specs
| Property | Value |
|----------|-------|
| Padding | `p-6` |
| Border Radius | `rounded-xl` |
| Background | `bg-card` |
| Border | `border border-border` |

#### Bar Row Specs
| Property | Value |
|----------|-------|
| Row Height | `h-8` (32px) |
| Row Gap | `gap-3` (12px) |
| Label Width | `w-28` (112px) - fixed |
| Bar Container | `flex-1` |
| Count Width | `w-8` (32px) - fixed |

#### Bar Styling
```css
.tag-bar {
  height: 24px;
  border-radius: 6px;
  background: linear-gradient(90deg, var(--devtalk-primary), var(--devtalk-primary-light));
  transition: width 0.3s ease;
}
```

#### Animation (Nice to have)
- On mount: bars animate from 0 to actual width
- Duration: 300ms
- Easing: ease-out

---

### 3. CategoryChart Component

**File**: `src/components/dashboard/CategoryChart.tsx`

#### Layout (Horizontal Bars - simpler than pie)
```
┌───────────────────────────────────────┐
│  📂 Posts by Category          (h3)   │
├───────────────────────────────────────┤
│                                       │
│  Development  ██████████████████ 60%  │
│  Frontend     ████████████       40%  │
│                                       │
└───────────────────────────────────────┘
```

#### Specs (same as TagChart)
- Use different color for each category
- Show percentage instead of count

#### Color Mapping
| Category | Color |
|----------|-------|
| Development | `--chart-1` (Primary Blue) |
| Frontend | `--chart-2` (Teal) |
| CSS | `--chart-3` (Green) |
| Tools | `--chart-4` (Purple) |
| Other | `--chart-5` (Orange) |

---

### 4. TagCloud Component

**File**: `src/components/dashboard/TagCloud.tsx`

#### Layout
```
┌──────────────────────────────────────────────────┐
│  🏷️ All Tags                               (h3)  │
├──────────────────────────────────────────────────┤
│                                                  │
│  React(4)  Next.js(3)  TypeScript(2)  Git(2)    │
│  JavaScript(1)  Tailwind(1)  CSS(1)  Antd(1)    │
│                                                  │
└──────────────────────────────────────────────────┘
```

#### Tag Badge Specs
| Property | Value |
|----------|-------|
| Padding | `px-3 py-1.5` |
| Border Radius | `rounded-full` |
| Font Size | Dynamic based on count |
| Background | `bg-devtalk-primary/10` |
| Text Color | `text-devtalk-primary-dark` |
| Border | `border border-devtalk-primary/20` |

#### Font Size Scaling
| Count | Font Size | Tailwind Class |
|-------|-----------|----------------|
| 1 | 12px | `text-xs` |
| 2-3 | 14px | `text-sm` |
| 4-5 | 16px | `text-base` |
| 6+ | 18px | `text-lg font-medium` |

#### States
- **Default**: as above
- **Hover**: `hover:bg-devtalk-primary/20 hover:scale-105 transition-all cursor-pointer`

#### Dark Mode
- Background: `dark:bg-devtalk-primary/20`
- Text: `dark:text-devtalk-primary-light`

---

### 5. RecentPosts Component

**File**: `src/components/dashboard/RecentPosts.tsx`

#### Layout
```
┌────────────────────────────────────────────────────┐
│  📝 Recent Posts                            (h3)   │
├────────────────────────────────────────────────────┤
│                                                    │
│  • Ant Design คู่มือเริ่มต้น...         Feb 1     │
│    ─────────────────────────────────────────────   │
│  • Conventional Commits: คู่มือ...       Feb 1    │
│    ─────────────────────────────────────────────   │
│  • TypeScript สำหรับ React...           Jan 25    │
│                                                    │
└────────────────────────────────────────────────────┘
```

#### Row Specs
| Property | Value |
|----------|-------|
| Padding | `py-3` |
| Border Bottom | `border-b border-border last:border-0` |
| Layout | `flex items-center justify-between` |

#### Typography
| Element | Style |
|---------|-------|
| Title | `text-sm font-medium text-foreground hover:text-devtalk-primary truncate` |
| Date | `text-xs text-muted-foreground whitespace-nowrap` |

#### States
- **Hover**: Row background `hover:bg-muted/50`
- Entire row is clickable link

---

## Responsive Design

### Breakpoints

| Breakpoint | Layout |
|------------|--------|
| Mobile (<640px) | 1 column, stacked |
| Tablet (640-1024px) | 2 columns for stats, 1 for charts |
| Desktop (>1024px) | 4 columns for stats, 2 for charts |

### Stats Cards Grid
```css
/* Mobile */
grid-template-columns: repeat(2, 1fr);
gap: 12px;

/* Desktop */
@screen md {
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}
```

### Charts Grid
```css
/* Mobile */
grid-template-columns: 1fr;
gap: 16px;

/* Desktop */
@screen lg {
  grid-template-columns: repeat(2, 1fr);
  gap: 24px;
}
```

---

## Accessibility

### Requirements
- [ ] Color contrast >= 4.5:1 for text
- [ ] Focus states visible on all interactive elements
- [ ] Screen reader labels for charts
- [ ] Keyboard navigable (Tab through interactive elements)

### ARIA Labels
```tsx
// StatCard
<div role="figure" aria-label="Total Posts: 5">

// TagChart
<div role="figure" aria-label="Tag popularity chart">
  <div role="listitem" aria-label="React: 4 posts">

// TagCloud
<button aria-label="Filter by React tag (4 posts)">
```

---

## Files to Create

| File | Type | Description |
|------|------|-------------|
| `src/components/Logo.tsx` | Component | DevTalk logo (icon + full) |
| `src/app/dashboard/page.tsx` | Page | Dashboard page |
| `src/lib/stats.ts` | Library | Stats calculation |
| `src/components/dashboard/StatCard.tsx` | Component | Stats card |
| `src/components/dashboard/TagChart.tsx` | Component | Bar chart |
| `src/components/dashboard/CategoryChart.tsx` | Component | Category bars |
| `src/components/dashboard/TagCloud.tsx` | Component | Tag cloud |
| `src/components/dashboard/RecentPosts.tsx` | Component | Recent posts list |

---

## CSS to Add (globals.css)

```css
/* DevTalk Brand Colors */
:root {
  --devtalk-primary: oklch(0.65 0.18 260);
  --devtalk-primary-light: oklch(0.78 0.12 260);
  --devtalk-primary-pale: oklch(0.95 0.03 260);
  --devtalk-primary-dark: oklch(0.35 0.12 260);
}

.dark {
  --devtalk-primary: oklch(0.70 0.15 260);
  --devtalk-primary-light: oklch(0.55 0.12 260);
  --devtalk-primary-pale: oklch(0.25 0.05 260);
  --devtalk-primary-dark: oklch(0.85 0.08 260);
}

/* Dashboard Chart Bar Animation */
@keyframes barGrow {
  from { width: 0; }
  to { width: var(--bar-width); }
}

.chart-bar {
  animation: barGrow 0.3s ease-out forwards;
}
```

---

## Handoff Checklist (Designer → Developer)

- [x] **Layout**: Page structure, spacing defined
- [x] **Colors**: All color codes (Hex + OKLCH)
- [x] **Typography**: Font sizes, weights for each element
- [x] **Components**: 6 components with full specs
- [x] **States**: Hover, focus, dark mode
- [x] **Responsive**: Breakpoints and layouts
- [x] **Accessibility**: ARIA labels, contrast requirements
- [x] **Assets**: Logo SVG code included
- [x] **CSS**: New variables and animations

---

*Created by @Designer | 2026-02-01*
