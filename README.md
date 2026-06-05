# Liquid Glass

A macOS-inspired translucent glass design system for AI agents.

## Install

```bash
hermes skills install aehooper72-svg/liquid-glass
```

## What It Is

Design tokens, glass panel recipes, shadow system, typography, and interaction rules for building dark-mode UIs with the macOS "Liquid Glass" aesthetic — translucent embossed panels, backdrop blur, layered inset shadows over blue-tinted dark surfaces.

Inspired by macOS Liquid Glass (WWDC 2025), Raycast UI, and MONIT.

## What's Included

- **SKILL.md** — full design system spec with tokens, recipes, anti-patterns, and framework-agnostic guidance
- **references/tokens.css** — ready-to-import CSS custom properties and component classes

## Quick Start

The skill auto-loads when you ask your agent to build UI with glass, translucent, or macOS-style aesthetics. Or load it explicitly:

```bash
hermes -s liquid-glass
```

## Tokens

| Category | Key Token | Value |
|----------|-----------|-------|
| Background | `--bg-primary` | `#07080a` |
| Glass | `--glass-fill` | `rgba(255,255,255, 0.04)` |
| Text | `--text-primary` | `#f9f9f9` |
| Accent | `--accent-interactive` | `hsl(202, 100%, 67%)` |

## License

MIT
