---
name: emil-design-polish
description: Use when building or reviewing landing pages, slide decks, interactive HTML boards, or UI animations with precision spring-physics UI and motion polish.
argument-hint: "[<html-path-or-component>] [--mode build|review]"
effort: high
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Precision Spring-Physics UI & Motion Polish (`/emil-design-polish`)

Applies tactile interaction engineering, GPU-composited transitions, and spring-physics motion rules across campaign landing pages (`/launch-page`), interactive decks (`/slide-deck`), and Studio HTML pages (`board.html`, `setup.html`).

## Core Principles

1. **Small interaction details compound.** Origin-aware popovers, `scale(0.97)` button press feedback, and interruptible CSS transitions make pages feel crisp and responsive.
2. **Bind client brand tokens directly.** Read `clients/<slug>/brand/tokens.json` first and bind `--primary`, `--accent`, `--ease-out`, and `typography.headingFont` variables.

## 7-Step UI & Animation Sequence

### 1. Frequency Gate (Should This Animate?)
| Frequency | Rule |
| :--- | :--- |
| **100+ times/day** (keyboard shortcuts, tab switches, toggles) | **No animation (`0ms`).** Instant state change. |
| **Tens of times/day** (hover states, filter chips, list items) | **120 to 160ms subtle transition** or none. |
| **Occasional** (modals, drawers, toasts, accordions) | **180 to 280ms** with custom `ease-out`. |
| **Marketing / First-time** (hero reveals, animated infographics) | **Staggered entrances, `clip-path` reveals, or spring curves.** |

### 2. Name the Job
Every transition needs one concrete purpose: **Feedback** (`scale(0.97)` on `:active`), **Spatial continuity** (enter and exit along the same axis), **State clarity** (status badge update), or **Walkthrough pacing**. Cut any animation without a job.

### 3. Pick the Simplest Runtime
1. **CSS Transition:** Hover, `:active` press, state toggles (interruptible mid-flight).
2. **CSS `@starting-style`:** Mount entrances without extra JS state.
3. **Web Animations API (`element.animate()`):** Programmatic triggers off the main thread.
4. **Deterministic Frame Seek (`window.__hyperframesSeek(frame)`):** Scrubbable HTML video stages captured at `30fps` via `gk render-video`.

### 4. GPU-Safe Properties
- **Animate `transform`, `opacity`, and `clip-path` only.** Avoid animating `width`, `height`, `margin`, `padding`, `top`, or `left`.
- **Start entrances at `transform: scale(0.95); opacity: 0;`** rather than `scale(0)`.
- **Press feedback on interactive buttons:**
  ```css
  .btn { transition: transform 160ms cubic-bezier(0.23, 1, 0.32, 1); }
  .btn:active { transform: scale(0.97); }
  ```

### 5. Custom Easing Curves & Duration Caps
Add custom curves to `:root`:
```css
:root {
  --ease-out: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
}
```
- Never use `ease-in` on UI controls.
- Keep UI durations under `300ms` and list staggers between `30ms` and `80ms` per item.

### 6. Hover & Reduced-Motion Media Queries
Include both media queries on interactive pages:
```css
@media (hover: hover) and (pointer: fine) {
  .interactive-card:hover { transform: translateY(-2px); }
}
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 120ms !important;
  }
}
```

### 7. Review Table Format
When reviewing an existing HTML page or deck (`--mode review`), output a Markdown table with `| Before | After | Why |` columns:

| Before | After | Why |
| :--- | :--- | :--- |
| `transition: all 300ms ease` | `transition: transform 180ms var(--ease-out), opacity 180ms var(--ease-out)` | Restrict to GPU-composited properties and custom `ease-out` |
| `transform: scale(0)` | `transform: scale(0.95); opacity: 0` | Avoid zero-volume pop-in |
| No `:active` button state | `.btn:active { transform: scale(0.97); }` | Immediate press feedback |
