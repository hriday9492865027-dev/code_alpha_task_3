# Lumina Workstation — All 44 Features Implementation Plan

## Overview

The existing `calculator.html` (1,951 lines, single-file) will be expanded to a **fully-featured workstation** (~6,000–7,000 lines). All 44 features will be integrated into the same single-file architecture for zero-dependency deployment.

---

## Open Questions

> [!IMPORTANT]
> **Currency Exchange (#37)**: Live FX rates require a free API key (e.g., [open.er-api.com](https://open.er-api.com)). Should I use a free key-less CDN, or skip live rates and use fixed reference rates?

> [!IMPORTANT]
> **Snake Game (#40)**: This requires its own full canvas game loop. Should it launch in a modal overlay, or replace the graphing canvas temporarily?

> [!IMPORTANT]
> **Matrix Mode (#20)**: This is a full UI panel (input grids, operation buttons). Should it appear as a new toggle button in the header (like Scientific/Graphing), or as a separate tab inside the scientific panel?

---

## Proposed Changes

### `[MODIFY]` [calculator.html](file:///c:/Users/Hriday/OneDrive/Desktop/pjct%201%20calci/calculator.html)

The file will be restructured into clearly labeled sections:

---

### 🎨 Section 1 — UI / UX Enhancements (8 features)

| # | Feature | Approach |
|---|---|---|
| 1 | **Resizable Font** | CSS variable `--display-font-size` + range slider in settings |
| 2 | **Haptic Feedback (Mobile)** | `navigator.vibrate(12)` on every button press |
| 3 | **Auto Dark/Light Mode** | `window.matchMedia('prefers-color-scheme')` listener applies Sakura (light) or Midnight (dark) on load |
| 4 | **Custom Accent Color Picker** | `<input type="color">` in header, updates `--accent-color` CSS var in real-time |
| 5 | **5th Theme — Ocean Depth** | New `[data-theme="ocean"]` CSS block + animated underwater bubble particles |
| 6 | **Animated Digit Roll** | CSS `@keyframes` count-up animation on display number change (odometer style) |
| 7 | **Responsive Mobile Layout** | `@media (max-width: 600px)` — stacked vertical panels, larger touch buttons (70px height) |
| 8 | **Swipe Gestures** | `touchstart/touchend` delta detection — swipe up=history, left=scientific, right=graphing |

---

### 🔬 Section 2 — Scientific & Math (12 features)

| # | Feature | Approach |
|---|---|---|
| 9 | **Inverse Trig** | `2nd` toggle button in scientific panel switches sin→asin, cos→acos, tan→atan |
| 10 | **Hyperbolic Functions** | `sinh`, `cosh`, `tanh` row added to scientific panel (shown when 2nd is active) |
| 11 | **Factorial (n!)** | `n!` button using iterative loop, error for non-integers/negatives |
| 12 | **Modulo (mod)** | `mod` operator added to `opIds`, treated same as `+`, `−`, etc. |
| 13 | **Log Base-N** | `logₙ` button opens a mini input prompt for base, computes `log(x)/log(n)` |
| 14 | **Cube Root (∛)** | `∛x` unary function using `Math.cbrt(v)` |
| 15 | **nCr / nPr** | Two buttons in scientific panel, use `n` as prev and `r` as cur |
| 16 | **Prime Checker** | After `=`, show a `[PRIME]` or `[COMPOSITE]` badge below display for integer results |
| 17 | **GCD / LCM** | Two buttons in scientific panel using Euclidean algorithm |
| 18 | **Base Converter** | Segmented control below display: DEC / BIN / OCT / HEX. Converts display value in real-time |
| 19 | **Expression Parser** | Text input field in display area — parse full expressions like `3*(4+2)^2` using `Function()` |
| 20 | **Matrix Calculator** | New modal panel: 2×2 / 3×3 input grids, operations: det, inverse, multiply, transpose |

---

### 📈 Section 3 — Graphing Enhancements (8 features)

| # | Feature | Approach |
|---|---|---|
| 21 | **Multi-Function Plot** | 3 formula input rows (f1, f2, f3) each with a unique color (accent, cyan, lime) |
| 22 | **Root Finder** | After each draw, Newton's method finds zeros and marks them with labeled dots |
| 23 | **Derivative Overlay** | Toggle button computes f′(x) numerically `(f(x+h)-f(x))/h` and draws dashed line |
| 24 | **Crosshair Tooltip** | `mousemove` on graph canvas shows floating `(x, y)` label at cursor |
| 25 | **Polar Mode** | Toggle switch converts formula bar to `r(θ)` polar mode, draws parametric xy from θ=0 to 2π |
| 26 | **Export Graph as PNG** | `canvas.toDataURL()` + programmatic `<a>` download click |
| 27 | **Parametric Equations** | Two inputs `x(t)` and `y(t)`, draws parametric curve over t range |
| 28 | **Integral Shading** | Two range inputs for `a` and `b`, shades area under curve with translucent fill + shows value |

---

### 🛠️ Section 4 — Utility / Productivity (9 features)

| # | Feature | Approach |
|---|---|---|
| 29 | **Unit Converter** | New panel (toggle button): dropdowns for category + from/to units, conversion tables in JS |
| 30 | **Percentage Solver** | Quick mode: 3 pre-set query types shown as tiles in a mini modal |
| 31 | **Equation Solver** | Quadratic formula panel — inputs for a, b, c coefficients, shows roots |
| 32 | **Statistics Mode** | Comma-separated data entry field, shows mean, median, mode, variance, std dev |
| 33 | **History Export** | "Export CSV" button in history drawer header — generates `.csv` blob download |
| 34 | **Pinned Calculations** | Star icon per history item, pinned panel shown at top of history drawer |
| 35 | **Multi-line Notepad** | Expandable `<textarea>` panel toggled from header, content persisted in localStorage |
| 36 | **Calculation Timer** | Stopwatch in header area with Start/Stop/Reset — uses `performance.now()` |
| 37 | **Currency Exchange** | Fixed reference rates table (USD base) + optional live fetch from `open.er-api.com` |

---

### 🎮 Section 5 — Fun / Easter Eggs (7 features)

| # | Feature | Approach |
|---|---|---|
| 38 | **Easter Egg: 1337** | Detects typed `1337` → display flashes green + "H4CK3R M0D3" glitch text for 2s |
| 39 | **Confetti on Big Numbers** | `Math.abs(result) >= 1,000,000` triggers `canvas-confetti` CDN animation |
| 40 | **Snake Game** | Hidden modal canvas game triggered by pressing `↑↑↓↓←→←→` (Konami code) |
| 41 | **Voice Input** | `SpeechRecognition` API parses spoken math expressions into the display |
| 42 | **Double-tap Copy** | `dblclick` on main display → clipboard write + brief "Copied!" toast |
| 43 | **QR Code of Result** | Uses `qrcode.js` CDN to generate QR in a modal when user clicks QR icon |
| 44 | **Share Calculation Link** | Encodes expression+result into URL hash (`#expr=3+4&res=7`) + copy-to-clipboard |

---

## New Header Buttons Added

| Button | Icon | Function |
|---|---|---|
| Notepad | 📝 | Toggle notepad panel |
| Unit Converter | 📐 | Toggle unit converter panel |
| Matrix Mode | ⬛ | Open matrix calculator modal |
| Timer | ⏱ | Toggle stopwatch |
| Voice Input | 🎙 | Start/stop speech recognition |
| Settings | ⚙️ | Open settings (color picker, font size slider) |

---

## CDN Libraries Used (no npm, no build step)

| Library | Purpose | CDN |
|---|---|---|
| `canvas-confetti` | Confetti animation (#39) | `cdn.jsdelivr.net` |
| `qrcode.js` | QR code generation (#43) | `cdn.jsdelivr.net` |

> [!NOTE]
> All other features are pure vanilla JS — no additional dependencies.

---

## Architecture Changes

- **CSS**: ~1,200 new lines — new panels, modals, responsive breakpoints, Ocean theme, animations
- **HTML**: ~400 new lines — new panel sections, modal overlays, input grids, timer display
- **JavaScript**: ~2,500 new lines — all 44 feature implementations, organized into labeled sections

**Final estimated file size**: ~6,500 lines, ~180 KB

---

## Verification Plan

### Automated
- Open in browser, check console for zero JS errors
- Keyboard shortcuts all work
- All 5 themes apply correctly

### Manual
- Click every one of the 44 features and verify behavior
- Test mobile layout at 375px viewport (Chrome DevTools)
- Test voice input, snake game, QR, confetti
- Verify localStorage persistence across page refresh
- Export history CSV, download graph PNG
