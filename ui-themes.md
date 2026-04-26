---
layout: default
title: UI Themes
---

# UI Themes

All Asymmetric Effort web properties must use the following design tokens to ensure consistent branding. These values are derived from the [SpecifyJS showcase site](https://specifyjs.asymmetric-effort.com) and serve as the canonical reference.

## Color Palette

### Light Mode (default: `data-theme="light"` or no attribute)

| Token | Value | Usage |
|---|---|---|
| `--color-primary` | `#3b82f6` | Links, accents, active states, branding |
| `--color-primary-dark` | `#2563eb` | Hover states, emphasized actions |
| `--color-bg` | `#ffffff` | Page background |
| `--color-bg-subtle` | `#f8fafc` | Card backgrounds, table headers, secondary surfaces |
| `--color-bg-muted` | `#f1f5f9` | Hover backgrounds, inactive surfaces |
| `--color-text` | `#0f172a` | Primary body text, headings |
| `--color-text-muted` | `#64748b` | Secondary text, labels, descriptions |
| `--color-border` | `#e2e8f0` | Borders, dividers, table lines |

### Dark Mode (`data-theme="dark"`)

| Token | Value | Usage |
|---|---|---|
| `--color-primary` | `#60a5fa` | Links, accents, active states, branding |
| `--color-primary-dark` | `#3b82f6` | Hover states, emphasized actions |
| `--color-bg` | `#0f172a` | Page background |
| `--color-bg-subtle` | `#1e293b` | Card backgrounds, table headers, secondary surfaces |
| `--color-bg-muted` | `#334155` | Hover backgrounds, inactive surfaces |
| `--color-text` | `#f1f5f9` | Primary body text, headings |
| `--color-text-muted` | `#94a3b8` | Secondary text, labels, descriptions |
| `--color-border` | `#334155` | Borders, dividers, table lines |

### Semantic Colors

| Token | Value | Usage |
|---|---|---|
| Error / Destructive | `#ef4444` | Error messages, destructive actions |
| Toggle off | `#cbd5e1` | Inactive toggle tracks |
| Code block background (dark) | `#1e293b` | Code block surfaces |
| Code block text | `#e2e8f0` | Code block foreground |
| Dialog backdrop | `rgba(0, 0, 0, 0.4)` | Modal overlays |

## Typography

### Font Stacks

| Context | Font Stack |
|---|---|
| Body / UI | `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` |
| Code / Monospace | `"SF Mono", Monaco, Consolas, monospace` |

### Font Sizes

| Element | Size | Weight |
|---|---|---|
| Hero heading (`h1`) | `48px` | `800` |
| Section heading (`h2`) | `28px` | `700` |
| Card heading (`h3`) | `18px` | `700` (default) |
| Article heading | `17px` | `700` |
| Body text | `15px` | `400` |
| Nav links | `14px` | `500` |
| Card body text | `14px` | `400` |
| Table cells | `14px` | `400` |
| Code blocks | `13px` | `400` |
| Small labels / captions | `12px`-`13px` | `400`-`600` |

### Line Height

| Context | Value |
|---|---|
| Body | `1.6` |
| Article body | `1.7` |
| Code blocks | `1.5` |

## Spacing

| Token | Value | Usage |
|---|---|---|
| `--max-width` | `1200px` | Maximum content width |
| Page padding | `32px 24px` | Main content area |
| Nav bar height | `56px` | Sticky navigation |
| Nav bar padding | `0 24px` | Horizontal nav padding |
| Nav link gap | `8px` | Space between nav items |
| Nav link padding | `6px 14px` | Individual nav link |
| Card padding | `24px` | Feature cards |
| Section margin | `48px 0` | Vertical section spacing |
| Grid gap | `24px` | Card grids |
| Stat card gap | `16px` | Stat card grids |
| Hero top padding | `80px` | Hero section top |
| Hero bottom padding | `48px` | Hero section bottom |
| Hero stat gap | `48px` | Space between hero stats |

## Border Radius

| Context | Value |
|---|---|
| `--radius` (default) | `8px` |
| Dialogs | `12px` |
| Toggle tracks | `12px` |
| Toggle thumbs / circle buttons | `50%` |
| Bar chart bars (top) | `4px 4px 0 0` |

## Shadows

| Context | Value |
|---|---|
| Card hover (light) | `0 4px 16px rgba(0, 0, 0, 0.1)` |
| Card hover (dark) | `0 4px 16px rgba(0, 0, 0, 0.4)` |
| Dialog (light) | `0 20px 60px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.05)` |
| Dialog (dark) | `0 20px 60px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255, 255, 255, 0.05)` |
| Toggle thumb | `0 1px 3px rgba(0, 0, 0, 0.2)` |

## Transitions

| Context | Property | Duration | Easing |
|---|---|---|---|
| Hover states | `background`, `border-color`, `color` | `0.15s` | default (ease) |
| Card hover | `box-shadow`, `border-color` | `0.2s` | default (ease) |
| Bar chart | `height` | `0.3s` | default (ease) |
| Toggle thumb | `transform` | `0.2s` | default (ease) |
| Toggle track | `background` | `0.2s` | default (ease) |
| Dialog entrance | opacity, transform | `0.2s` | `ease-out` |

## Component Patterns

### Navigation Bar

- Sticky, top-positioned (`z-index: 100`)
- Background matches `--color-bg` with a `1px` bottom border
- Active nav link uses `--color-primary` background with white text
- Logo: `20px`, weight `700`, colored `--color-primary`

### Cards

- `1px` solid border using `--color-border`
- `8px` border radius
- `24px` padding
- On hover (clickable): elevated shadow, border becomes `--color-primary`

### Code Blocks

- Background: `#1e293b` (always dark, even in light mode)
- Text: `#e2e8f0`
- Monospace font stack at `13px`
- `16px 20px` padding, `8px` border radius
- Horizontal scroll for overflow

### Dialogs

- Backdrop: semi-transparent black (`rgba(0, 0, 0, 0.4)`)
- Panel: `12px` border radius, max-width `1200px`
- Sticky header with close button
- Entrance animation: fade + slide up + slight scale

### Tables

- Full width, collapsed borders
- Header row: `--color-bg-subtle` background, `600` weight
- Row hover: `--color-bg-muted` background
- Cell padding: `10px 14px`

## CSS Custom Properties Reference

All projects should define these custom properties on `:root` (light) and `[data-theme="dark"]`:

```css
:root {
  --color-primary: #3b82f6;
  --color-primary-dark: #2563eb;
  --color-bg: #ffffff;
  --color-bg-subtle: #f8fafc;
  --color-bg-muted: #f1f5f9;
  --color-text: #0f172a;
  --color-text-muted: #64748b;
  --color-border: #e2e8f0;
  --radius: 8px;
  --max-width: 1200px;
}

[data-theme="dark"] {
  --color-primary: #60a5fa;
  --color-primary-dark: #3b82f6;
  --color-bg: #0f172a;
  --color-bg-subtle: #1e293b;
  --color-bg-muted: #334155;
  --color-text: #f1f5f9;
  --color-text-muted: #94a3b8;
  --color-border: #334155;
}
```

## Global Reset

All projects should apply the following global reset:

```css
*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```
