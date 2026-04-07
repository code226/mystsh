# Design System: mystsh `ui-kit` (Tracker Model)

This document outlines the visual and interactive foundations for the mystsh Stash Tracker platform.

## 1. Color Palette & Design Tokens

We use a high-energy "Dark Mode" aesthetic to appeal to digital-native teens while maintaining a professional feel for parents.

### Core Brand Colors
| Token | Value | Usage |
| :--- | :--- | :--- |
| `token.color.brand.primary` | #39FF14 | Neon Green: Balances, points earned, "On Budget" states. |
| `token.color.brand.secondary` | #4B0082 | Deep Purple: Branding, secondary surfaces. |
| `token.color.brand.accent` | #7DF9FF | Electric Blue: Interactive highlights, budget progress. |

### UI Surfaces & Text
- **Main Background:** #121212 (`token.color.bg.base`)
- **Surface (Cards):** #1E1E1E (`token.color.bg.surface`)
- **Text Primary:** #FFFFFF (`token.color.text.primary`)
- **Text Secondary:** #B3B3B3 (`token.color.text.secondary`)

### Gamification States
- **Streak Bonus:** Gold (#FFD700)
- **Over Budget:** Coral (#FF7F50)
- **Quest Completion:** Neon Green (#39FF14)

## 2. Layout & Gamified Components

### The "Budget Meter"
- A semi-circular or horizontal progress bar using **Electric Blue**.
- **Animation:** Fills from left to right as spending occurs.
- **Visual Feedback:** Turns **Neon Green** if the user is under budget, and **Coral** if they exceed it.

### The "Stash Point" Badge
- A glowing pill-shaped badge displaying the current point balance.
- **Animation:** "Pops" or scales up when points are added in real-time.

## 3. Typography
- **Headings:** Inter (Bold) - Line height 1.2.
- **Body:** Roboto (Regular/Medium) - Line height 1.5.
- **Monospace (Balances):** SF Pro Mono - For clear, tabular figure alignment in transaction lists.

## 4. Accessibility & Feedback
- **Haptics:** Strong haptic feedback for "Point Earned" events.
- **Contrast:** Minimum 4.5:1 ratio for all text/background combinations.
- **Reduced Motion:** Respect system settings to simplify animations for budget meters and point counters.
