---
name: liquid-glass
description: "Use when building UI with the macOS Liquid Glass aesthetic — translucent embossed panels, backdrop blur, layered inset shadows, blue-tinted dark surfaces. Provides design tokens, glass panel recipes, shadow system, typography, interaction rules, and anti-patterns for consistent dark-mode glass UI across any framework or output format."
version: 1.0.0
author: Arielle Hooper
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [design, glass, macos, ui, css, dark-mode, glassmorphism, tokens, design-system, liquid-glass]
    related_skills: [claude-design, popular-web-designs, design-md, architecture-diagram]
---

# Liquid Glass Design System

A macOS-inspired translucent glass material system. Panels feel like physical sheets of frosted glass floating above content. Depth comes from layered shadows, subtle inset highlights, and backdrop blur — never opaque fills.

Inspired by macOS Liquid Glass (WWDC 2025), Raycast UI, and the MONIT app.

## When to Use

- Building dark-mode UIs with translucent/frosted glass panels
- Designing macOS-native-feeling apps, menu bar utilities, or floating palettes
- Creating dashboards, settings panels, command palettes, or card layouts with depth
- Any project where the user mentions "glass", "translucent", "frosted", "macOS-style", or "Raycast-like"

Do NOT use for:
- Light-mode UIs (this is a dark-mode-first system)
- Flat/minimal material design (this is explicitly layered and dimensional)
- Projects that need fully opaque backgrounds (e.g. print, accessibility-first)

## Core Philosophy

1. **Barely-tinted glass** — fills use `rgba(255,255,255, 0.03–0.07)`, never opaque
2. **Depth through shadow pairs** — every shadow has an outer drop shadow AND an inset highlight/shadow
3. **Blue-tinted void** — the background is near-black with a blue undertone (`#07080a`), never pure `#000`
4. **Backdrop blur is mandatory** — `backdrop-filter: blur(40px) saturate(180%)` on every glass surface
5. **Function over ornament** — glass is a material, not a decoration

## Quick Reference — Design Tokens

Full token set with CSS custom properties: `references/tokens.css`

### Backgrounds
| Token | Value | Use |
|-------|-------|-----|
| `--bg-primary` | `#07080a` | Page/root background (near-black blue-tint) |
| `--bg-surface` | `#101111` | Elevated surface behind glass |

### Glass Fills
| Token | Value | Use |
|-------|-------|-----|
| `--glass-fill` | `rgba(255,255,255, 0.04)` | Default panel fill |
| `--glass-fill-hover` | `rgba(255,255,255, 0.07)` | Hovered panel |
| `--glass-fill-active` | `rgba(255,255,255, 0.03)` | Pressed/active (darker) |
| `--glass-border` | `rgba(255,255,255, 0.06)` | Structural border |
| `--glass-border-hover` | `rgba(255,255,255, 0.12)` | Hovered border |
| `--glass-inset-top` | `rgba(255,255,255, 0.08)` | Top-edge light refraction |
| `--glass-inset-bottom` | `rgba(0,0,0, 0.25)` | Bottom-edge shadow |

### Text
| Token | Value | Use |
|-------|-------|-----|
| `--text-primary` | `#f9f9f9` | Headings, labels |
| `--text-secondary` | `#9c9c9d` | Body, descriptions |
| `--text-tertiary` | `#6a6b6c` | Captions, metadata |

### Accent
| Token | Value | Use |
|-------|-------|-----|
| `--accent` | `#FF6363` | Punctuation accent — use sparingly |
| `--accent-interactive` | `hsl(202, 100%, 67%)` | Links, focus rings, interactive elements |

### Radii
| Token | Value |
|-------|-------|
| `--radius-sm` | `6px` |
| `--radius-md` | `12px` |
| `--radius-lg` | `16px` |
| `--radius-pill` | `86px` |

## Glass Panel Recipe

This is the signature surface treatment. Every glass panel uses this pattern:

```css
.glass-panel {
  background: var(--glass-fill);
  backdrop-filter: blur(40px) saturate(180%);
  -webkit-backdrop-filter: blur(40px) saturate(180%);
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-md);
  box-shadow:
    rgba(0, 0, 0, 0.28) 0px 1px 3px,                    /* outer drop */
    rgba(255, 255, 255, 0.05) 0px 1px 0px 0px inset,     /* top highlight */
    rgba(0, 0, 0, 0.25) 0px -1px 0px 0px inset;          /* bottom shadow */
}

.glass-panel:hover {
  background: var(--glass-fill-hover);
  border-color: var(--glass-border-hover);
  box-shadow:
    rgba(0, 0, 0, 0.35) 0px 2px 6px,
    rgba(255, 255, 255, 0.08) 0px 1px 0px 0px inset,
    rgba(0, 0, 0, 0.25) 0px -1px 0px 0px inset;
}
```

## Shadow System (5 Depth Levels)

| Level | Name | Use |
|-------|------|-----|
| 0 | `shadow-void` | `none` — flat, no elevation |
| 1 | `shadow-subtle` | `rgba(0,0,0, 0.28) 0px 1.189px 2.377px` — subtle lift |
| 2 | `shadow-ring` | Double ring containment (cards, list items) |
| 3 | `shadow-glass` | The signature — outer drop + top inset + bottom inset |
| 4 | `shadow-floating` | Modals, palettes, tooltips — maximum elevation |

Shadow level 2 (ring):
```css
box-shadow:
  rgb(27, 28, 30) 0px 0px 0px 1px,
  rgb(7, 8, 10) 0px 0px 0px 1px inset;
```

Shadow level 4 (floating):
```css
box-shadow:
  rgba(0, 0, 0, 0.5) 0px 0px 0px 2px,
  rgba(255, 255, 255, 0.19) 0px 0px 14px,
  rgba(255, 255, 255, 0.05) 0px 1px 0px 0px inset,
  rgba(0, 0, 0, 0.25) 0px -1px 0px 0px inset;
```

## Typography

```css
font-family: 'Inter', system-ui, -apple-system, sans-serif;
mono-family: 'Geist Mono', ui-monospace, SFMono-Regular, monospace;
```

| Role | Size | Weight | Line-height |
|------|------|--------|-------------|
| Display | 64px | 600 | 1.10 |
| Heading | 24px | 500 | normal |
| Subhead | 20px | 500 | 1.60 |
| Body | 16px | 500 | 1.60 |
| Caption | 14px | 500 | 1.14 |
| Small | 12px | 600 | 1.33 |

- Body weight is **500** (medium) — never 400 on dark backgrounds
- Letter-spacing: `0.2px` positive — creates airy feel on dark
- OpenType features: `"calt" "kern" "liga" "ss03"`

## Interaction Rules

| State | Treatment |
|-------|-----------|
| Hover | Opacity transition `0.6` — NOT color swap |
| Focus | Border brightens + glow ring `hsla(202, 100%, 67%, 0.15)` |
| Active | Glass fill drops to `0.03`, slight `scale(0.98)` |
| Transition | `200ms ease-out` for all |

```css
.glass-interactive {
  transition: background 200ms ease-out, border-color 200ms ease-out, box-shadow 200ms ease-out;
}
.glass-interactive:focus-visible {
  border-color: var(--accent-interactive);
  box-shadow:
    0 0 0 2px hsla(202, 100%, 67%, 0.15),
    /* plus the standard inset shadows */;
}
.glass-interactive:active {
  background: var(--glass-fill-active);
  transform: scale(0.98);
}
```

## Animation

- **Easing:** `cubic-bezier(0.22, 1, 0.36, 1)` for entrances (spring-like)
- **Duration:** 200–400ms for micro-interactions, 600ms for page-level transitions
- **Respect `prefers-reduced-motion`** — provide a `prefers-reduced-motion` media query that disables non-essential animation
- **NO looping decorative animations** — animation serves function only

## Anti-Patterns (DO NOT)

1. **Pure black backgrounds** — always use `#07080a` (blue-tinted)
2. **Single-layer flat shadows** — shadows MUST have outer + inset pairs
3. **Opaque gray fills called "glass"** — background MUST show through (keep fills at 0.03–0.07 opacity)
4. **Heavy drop shadows without inset companions** — every shadow needs a partner
5. **Regular (400) body weight on dark** — use 500
6. **Negative letter-spacing on body text** — use positive `0.2px`
7. **Aggressive gradient backgrounds or rainbow palettes** — this is a restrained system
8. **Decorative glassmorphism** — glass is a material, not a visual effect to sprinkle everywhere
9. **Color-swapping on hover** — use opacity transitions instead
10. **Looping animations** — no spinning icons, pulsing glows, or breathing effects

## Framework-Agnostic Guidance

This design system works with any output:

- **HTML/CSS:** Use the CSS custom properties and class recipes directly
- **React/Vue/Svelte:** Map tokens to CSS-in-JS variables or Tailwind theme config
- **SwiftUI:** Map to `.ultraThinMaterial` with custom shadow overlays and the same color values
- **Tailwind:** Extend `theme.colors` and `theme.boxShadow` with the token values
- **Figma/Design tools:** Use the token table as the source of truth for color/typography styles

When generating code, always:
1. Start with `--bg-primary: #07080a` as the root background
2. Apply `backdrop-filter: blur(40px) saturate(180%)` to every glass surface
3. Use the shadow system (never a single `box-shadow` value — always the multi-layer recipe)
4. Set body text weight to 500
5. Include `prefers-reduced-motion` handling

## Verification Checklist

- [ ] Root background is `#07080a`, not `#000000` or pure black
- [ ] All glass panels have `backdrop-filter: blur(40px) saturate(180%)`
- [ ] Every shadow has outer + inset layers (no single-value box-shadows)
- [ ] Glass fills stay between 0.03–0.07 opacity
- [ ] Body text weight is 500, not 400
- [ ] Letter-spacing is positive (0.2px), not negative
- [ ] Hover uses opacity transitions, not color swaps
- [ ] Focus states include a colored glow ring
- [ ] Active states darken the fill and apply `scale(0.98)`
- [ ] `prefers-reduced-motion` is respected for animations
- [ ] No looping decorative animations
- [ ] No aggressive gradients or rainbow palettes
