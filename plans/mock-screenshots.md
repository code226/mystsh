# mystsh Mock Screenshots & Wireframes

This document provides visual representations of the core app screens as defined in the [Comprehensive Plan](./plan.md).

---

## 1. Teen Dashboard (Home Screen)

**Theme:** Dark Mode (#121212) | **Primary:** Neon Green (#39FF14)

```mermaid
graph TD
    A[Header: Hello, Alex 👋 + Avatar]
    B[Balance: $125.50 - Neon Green, Large]
    C[Virtual Card: 'mystsh' Logo - Chip - Tap to Pay]
    D[Button: Add to Apple Wallet - Pill Shape]
    E[Section: Recent Transactions]
    F[Transaction: Starbucks - $5.45]
    G[Transaction: Steam - $12.99]
    H[Bottom Nav: Home | Quests | Goals | Profile]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    E --> G
    G --> H
```

### UI Details:
- **Balance:** `SF Pro Display`, Bold, 32pt.
- **Virtual Card:** 16px border radius, subtle gradient (Deep Purple to Black).
- **Transactions:** Merchant logos on the left, amount in `SF Pro Mono` on the right.

---

## 2. Parent Dashboard (Control Center)

**Theme:** Dark Mode (#121212) | **Secondary:** Deep Purple (#4B0082)

```mermaid
graph TD
    A[Header: Family Overview]
    B[Total Balance: $2,450.00]
    C[Teen Card: Alex - Active - $125.50]
    D[Teen Card: Sam - Frozen - $0.00]
    E[Quick Actions: Send Money | Set Limits]
    F[Critical Action: FREEZE CARD - Red Button]
    G[Section: Real-time Activity Feed]
    H[Feed: Alex spent $5.45 at Starbucks - 2m ago]

    A --> B
    B --> C
    B --> D
    C --> E
    C --> F
    F --> G
    G --> H
```

### UI Details:
- **Teen Profile Card:** Displays avatar, current balance, and a "View Analytics" link.
- **Freeze Button:** Prominent #FF3B30 button with a lock icon.
- **Activity Feed:** Push-style notifications in a scrollable list.

---

## 3. Literacy Quest Screen (Teen App)

**Theme:** Dark Mode (#121212) | **Accent:** Electric Blue (#7DF9FF)

```mermaid
graph TD
    A[Header: Stash Points: 1,250 🌟]
    B[Quest: Magic of Compounding - [======--] 75%]
    C[Quest: Spotting Phishing - [---] 0%]
    D[Quest: Credit Score 101 - Completed ✅]
    E[Section: Point Rewards]
    F[Reward: $10 Amazon Gift Card - 5,000 pts]
    G[Reward: Stash Boost +5% - 2,500 pts]

    A --> B
    A --> C
    A --> D
    D --> E
    E --> F
    E --> G
```

### UI Details:
- **Progress Bars:** Thin Electric Blue bars against a Dark Gray background.
- **Quest Cards:** Large cards with icons representing the topic (e.g., a shield for Phishing).
- **Points:** Animated counter when a quest is completed.
