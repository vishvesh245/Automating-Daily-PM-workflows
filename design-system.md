---
name: design-system
description: "Noon Minutes design system reference. Use when designing features, building UI, reviewing designs, or generating FE code — provides exact tokens, color palette, typography scale, component inventory, and layout rules so output matches the real design system."
argument-hint: "[optional: specific component or token to look up]"
---

# Noon Minutes Design System — Flash_Noon Minutes

Source Figma file: `https://www.figma.com/design/5CW3oDRqn4GzhmyJIms3vy/Flash_Noon-Minutes`
Last synced: 2026-03-23
Created by: Vijay Verma | Maintained by design team (last edit: Amal R)

---

## 1. Typography

### Font Families
| Role | Family | Usage |
|---|---|---|
| Primary UI | **Gilroy** | All body text, headings, labels, buttons |
| Brand/Logo | **Noontree** | Brand header text only (60px/w800) |
| Logo wordmark | **Proxima Nova** | "noon" wordmark (16px/w700) |
| Serif accent | **Libre Caslon Text** | Limited decorative use |
| System | **SF Pro Text** | iOS system UI elements (status bar) |

### Font Size Scale (Gilroy)
| Token | Size | Rem |
|---|---|---|
| display-xl | 80px | 5rem |
| display-lg | 64px | 4rem |
| display-md | 40px | 2.5rem |
| heading-xl | 32px | 2rem |
| heading-lg | 28px | 1.75rem |
| heading-md | 26px | 1.625rem |
| heading-sm | 24px | 1.5rem |
| body-lg | 20px | 1.25rem |
| body-md | 17px | 1.0625rem |
| body-sm | 15px | 0.9375rem |
| caption-lg | 13px | 0.8125rem |
| caption-md | 12px | 0.75rem |
| caption-sm | 11px | 0.6875rem |
| micro-lg | 10px | 0.625rem |
| micro-sm | 9px | 0.5625rem |

### Font Weights
| Token | Value | Usage |
|---|---|---|
| regular | 400 | Body text, descriptions |
| medium | 500 | Secondary headings, labels |
| semibold | 600 | Primary headings, buttons |
| bold | 700 | Emphasis, CTAs |
| extrabold | 800 | Display/hero text |

### Line Heights
| Size Range | Line Height |
|---|---|
| 80px (display-xl) | 82px |
| 64px (display-lg) | 70px |
| 32px (heading-xl) | 42px |
| 28px (heading-lg) | 34px |
| 26px (heading-md) | 32px |
| 24px (heading-sm) | 30px |
| 20px (body-lg) | 28px |
| 17px (body-md) | 24px |
| 15px (body-sm) | 20px |
| 13px (caption-lg) | 18px |
| 12px (caption-md) | 16px |
| 11px (caption-sm) | 14px |
| 10px (micro-lg) | 12px |
| 9px (micro-sm) | 10px |

### Letter Spacing
| Size Range | Letter Spacing |
|---|---|
| 80px | -2.4px (-0.15rem) |
| 64px | -1.92px (-0.12rem) |
| 40px | -0.8px (-0.05rem) |
| 32px | -0.64px (-0.04rem) |
| 28px | -0.56px (-0.035rem) |
| 26px | -0.26px (-0.016rem) |
| 24px | -0.24px (-0.015rem) |
| 20px | -0.2px (-0.0125rem) |
| 17px | -0.18px (-0.011rem) |
| 15px | -0.16px (-0.01rem) |
| 13px | -0.14px (-0.009rem) |
| 12px | -0.12px (-0.0075rem) |
| 11px | 0px |
| 10px | 1px (0.0625rem) |
| 9px | 0px |

### Font Styles
- `normal` (default)
- `italic` (emphasis only)

---

## 2. Color Palette — Primitives

Each scale has 10 shades, numbered 50 (lightest) to 900 (darkest).

### Crimson (Primary Brand Red)
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fff0f2 | #ffc0cb | #ffa3b4 | #fe859b | #ff4869 | #f91a47 | #e0013a | #bf0333 | #930227 | #33010e |

### Orange
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fff6eb | #ffe7d6 | #fdd1af | #fbb782 | #ff9647 | #ff720d | #ef5700 | #cc4a00 | #992b00 | #561700 |

### Yellow
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fff8ea | #fff2d6 | #ffe6ad | #fcd373 | #f9c64d | #ffba19 | #eaa400 | #945c00 | #702c00 | #3d1200 |

### Rose
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fdf2f8 | #fee1ed | #fecde1 | #fd9bc2 | #fc69a4 | #f73b86 | #dc1867 | #bc064f | #9e0542 | #60062a |

### Magenta
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #feeff9 | #fedff3 | #ffcef2 | #fface5 | #f877d2 | #e142bc | #ca26a5 | #a91a90 | #891869 | #66124e |

### Blue
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #ebf1ff | #d6e2ff | #c2d4ff | #8fb0ff | #5c8dff | #2969ff | #034efc | #0043e0 | #0037b8 | #00257a |

### Purple (Cornflower)
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #f1eefc | #efe3ff | #e8d6ff | #c599ff | #b47aff | #9f5ff1 | #8a47e1 | #6831af | #582593 | #391f5c |

### Emerald
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #f0fdf7 | #d2f9e7 | #b6f7d8 | #77e8b3 | #36d38e | #03b876 | #11a770 | #007a53 | #006644 | #005136 |

### Green (Grape)
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #f2fdf5 | #defce9 | #c6f7bb | #9eef8a | #68de4a | #08c04b | #06a23f | #087f34 | #0b7132 | #084721 |

### Cherry
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fff0ee | #ffe1de | #ffd2cd | #ffb2ab | #fc7f79 | #f83446 | #de1135 | #bb032a | #950f22 | #520810 |

### Grey (Neutral)
| 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 |
|---|---|---|---|---|---|---|---|---|---|
| #fafafc | #f0f0f5 | #e2e2e7 | #d2d2d6 | #babbc0 | #aaabb1 | #909197 | #66686e | #36393e | #02060c |

### Semantic Color Usage
| Purpose | Token | Example |
|---|---|---|
| Primary brand | Crimson-500 | #f91a47 — CTAs, primary buttons, brand accents |
| Secondary brand | Purple-600 | #8a47e1 — Secondary actions, highlights |
| Success | Emerald-500 | #03b876 — Confirmations, delivery status |
| Warning | Yellow-500 | #ffba19 — Caution states, low stock |
| Error/Danger | Cherry-500 | #f83446 — Errors, destructive actions, out of stock |
| Info | Blue-500 | #2969ff — Informational states, links |
| Text primary | Grey-900 | #02060c |
| Text secondary | Grey-600 | #909197 |
| Text tertiary | Grey-500 | #aaabb1 |
| Background primary | #ffffff | White |
| Background secondary | Grey-50 | #fafafc |
| Border default | Grey-200 | #e2e2e7 |
| Border subtle | Grey-100 | #f0f0f5 |

### Registered Figma Styles
- **Gray Shades/Grey 1** — Secondary text, icons default color
- **Primary Colors/White** — White backgrounds
- **Elevations/100** — Drop shadow for depth (blur: 8, rgba(2,6,12,0.10))

---

## 3. Effects & Elevation

| Token | Type | Properties |
|---|---|---|
| elevation-100 | drop-shadow | blur: 8px, color: rgba(2,6,12,0.10), x: 0, y: 0 |
| elevation-200 | drop-shadow | blur: 8px, color: rgba(2,6,12,0.10), x: 0, y: 4 |
| elevation-300 | drop-shadow | blur: 28px, color: rgba(2,6,12,0.10), x: 0, y: -12 |

---

## 4. Component Inventory

### Stable Components (Production Ready)
Components marked "do not make edits" in Figma are the source of truth.

| Component | Figma Node | Key Variants | Notes |
|---|---|---|---|
| **Button** | 477:32681 | — | Primary shopping CTA |
| **Icon Buttons** | 7900:37764 | — | Standalone icon actions |
| **Add Button** | 7899:29745 | Add Button (component set) | Quantity increment/decrement |
| **Alerts** | 797:5886 | .progress, .Action Type | Toast/banner notifications |
| **Badges** | 576:48671 | — | Status indicators, counts |
| **Bottom Navigation** | 715:27783 | — | App tab bar |
| **Bottom Sheet** | 776:46752 | `Type`: Default/Full, `Action Bar`: True/False | Modal overlay from bottom |
| ↳ .Header | — | `Navigation`: T/F, `Alignment`: Center/Left, `Scroll`: T/F | Sheet header sub-component |
| **Chips** | 5958:63754 | default chip, active chips, Input Chip, Image selection chip, States | Filter/selection pills |
| **Feature Tag** | 7319:32462 | — | Promotional labels |
| **Page Header** | 576:49812 | — | Screen title bar |
| **Info Strips** | 2075:13197 | — | Informational banners |
| **Search Bar** | 690:3602 | — | Global search input |
| **Hero Widget** | 10645:769 | — | Homepage hero/promo carousel |
| **Action Bar** | 2030:11940 | — | Fixed bottom action bar |

### Product Cards (Key Commerce Component)
| Component | Variants | Properties |
|---|---|---|
| **Card** (31 variants) | `Size`: S/M/L, `State`: Default/Out of Stock/Dropping Soon/One Exclusive, `Style`: Floating/Solid/Loading/Banner | Vertical product display |
| **Horizontal Card** (7 variants) | `Size`: M/L/Freebie, `Use Case`: Variant/Cart/Product/Loading | Cart items, horizontal lists |
| **Combo Card** (2 variants) | `View`: Scroll/Default | Bundle/combo products |

### Other Components
| Component | Figma Node | Notes |
|---|---|---|
| Tabs | 815:13914 | Tab navigation (Tab Navigation set) |
| Dropdowns | 690:1649 | Select/dropdown menus |
| Toggle | 576:45025 | On/off switches |
| Tooltips | 576:45101 | Contextual hints |
| Lists | 776:53704 | List item rows |
| Section Header | 879:3167 | Section title + action |
| Accordion | 884:5974 | Expandable content |
| Aerobar | 758:25723 | Top app bar with address, MOV, carousel indicators |
| Offers/Coupons | 1478:24189 | Coupon Card, Promocode, ticket separator |
| Product Card Tags | (in Product Cards) | Price, discount, status badges |
| Qty + Variant selector | (in Product Cards) | Quantity stepper with variant selection |

### WIP Components (In Progress — Use with Caution)
| Component | Figma Node |
|---|---|
| Input | 477:32682 |
| Pill Button | 8349:17373 |
| Dividers | 690:1624 |
| Overlay | 7946:21718 |
| Checkbox Field | 477:38912 |
| Radio Field | 7640:34988 |
| Special Button | 7900:37763 |

---

## 5. Layout & Spacing Conventions

### Page Structure
- **Device target**: iPhone 16 Pro (393pt width)
- **Page padding**: 16px horizontal
- **Section gap**: 24px vertical
- **Content padding**: 16px left/right, 16px top, 64px bottom (for bottom nav clearance)

### Common Spacing Tokens (from layout patterns)
| Gap | Usage |
|---|---|
| 0px | Tightly coupled elements |
| 4px | Inline icon + text |
| 8px | Related items in a group |
| 16px | Between content sections |
| 24px | Between major sections |
| 48px | Hero/display spacing |

### Border/Stroke Patterns
- Default border: 1px inside, Grey-200 (#e2e2e7)
- Subtle border: 1px inside, Grey-100 (#f0f0f5)
- Active/focus: 1px inside, brand color
- Divider: 1px, Grey-100

---

## 6. Component Section Convention in Figma

Each component page follows this section pattern:
| Section | Icon | Purpose |
|---|---|---|
| Source components | ⚠️ do not make edits | Master component definitions — never edit directly |
| Documentation | ℹ️ | Usage guidelines, do's and don'ts |
| Usage examples | ➤ | Real-world usage patterns and context |
| Deprecated | ❌ | Old versions kept for reference, do not use |

---

## 7. How to Use This Skill

### When designing a new feature:
1. Reference this file for all token values (colors, typography, spacing)
2. Check the component inventory before creating anything new
3. Use exact hex values and font sizes from this file
4. If a component doesn't exist here, flag it — don't invent one

### When writing frontend code:
1. Use the typography scale for all text sizing
2. Use the color primitives for all color values
3. Reference component variant properties for prop definitions
4. Follow the spacing tokens for consistent layout

### When reviewing designs:
1. Verify all colors match this palette
2. Check typography against the scale
3. Confirm all components exist in the inventory
4. Flag any custom/non-system elements

### Fetching live component details from Figma:
If you need deeper component information (exact padding, border-radius, inner structure), fetch from Figma using:
- File key: `5CW3oDRqn4GzhmyJIms3vy`
- Use `FIGMA_GET_FILE_JSON` with the component's node ID from the inventory above
- Use `FIGMA_RENDER_IMAGES_OF_FILE_NODES` to get visual reference

---

*This file is auto-generated from the Flash_Noon Minutes Figma file. If the design system is updated, re-run extraction to refresh tokens.*
