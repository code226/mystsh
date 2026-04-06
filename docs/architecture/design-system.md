# Design System: mystsh `ui-kit`

This document outlines the visual and interactive foundations of the mystsh platform, shared across all mobile and web applications via the `packages/ui-kit` monorepo package.

## 1. Color Palette & Design Tokens

We use a token-based system to ensure consistency and facilitate future theme updates.

### Core Brand Colors
| Token | Value | Usage |
| :--- | :--- | :--- |
| `token.color.brand.primary` | #39FF14 | Neon Green: Primary actions, success, balances. |
| `token.color.brand.secondary` | #4B0082 | Deep Purple: Branding, secondary surfaces. |
| `token.color.brand.accent` | #7DF9FF | Electric Blue: Interactive highlights, progress. |

### UI Surfaces & Text
| Token | Value | Usage |
| :--- | :--- | :--- |
| `token.color.bg.base` | #121212 | Main app background (Dark Mode). |
| `token.color.bg.surface` | #1E1E1E | Cards, modals, and elevated surfaces. |
| `token.color.text.primary` | #FFFFFF | Primary readability. |
| `token.color.text.secondary` | #B3B3B3 | Supporting text, captions. |

### Semantic States
- **Error:** #FF3B30 (`token.color.state.error`)
- **Warning:** #FFCC00 (`token.color.state.warning`)

## 2. Layout & Spacing

### Spacing Scale (4px Base Grid)
All margins, padding, and gaps must align with the base-4 scale:
`4, 8, 12, 16, 24, 32, 48, 64, 80, 96`.

### Border Radii
- **Small (4px):** Tooltips, small tags.
- **Medium (12px):** Input fields, standard cards.
- **Large (24px):** Large dashboard sections.
- **Pill (999px):** Primary buttons.

## 3. Typography

| Style | Font Family | Weight | Line Height | Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Heading 1** | Inter | Bold | 1.2 | Screen titles. |
| **Body** | Roboto | Regular/Medium | 1.5 | General text. |
| **Monospace** | SF Pro Mono | Medium | 1.0 | Transaction amounts, ID numbers. |

## 4. Accessibility (A11y) Standards

- **Contrast:** Minimum 4.5:1 ratio for all text.
- **Touch Targets:** Interactive elements must be at least 44x44 points.
- **Screen Readers:** All icons must include `accessibilityLabel`.
- **Motion:** Use `useReducedMotion` hooks to disable animations for sensitive users.
