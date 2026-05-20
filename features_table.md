# Lumina Workstation — Features & Changes Table

> Single-file calculator (`calculator.html`, 1,951 lines) pushed to [code_alpha_task_3](https://github.com/hriday9492865027-dev/code_alpha_task_3)

---

## 🎨 Themes

| Theme | Color Palette | Background Particles | Button Sound |
|---|---|---|---|
| **Midnight Glass** | Deep navy + amber accent | 70 shimmering drifting stars | Deep mechanical keypress (sine sweep) |
| **Cyberpunk Neon** | Dark purple + hot pink/cyan | 35 falling binary 0/1 streams | Chiptune 8-bit laser sweep (triangle) |
| **Nordic Aurora** | Deep teal + emerald green | Aurora-glow particles | Liquid water droplet (sine) |
| **Sakura Blossom** | Soft pink / white (light mode) | 25 falling cherry blossom petals | Hollow bamboo block hit (triangle) |

All themes support **smooth 0.8s CSS transitions** and are **persisted in `localStorage`**.

---

## 🖩 Calculator Modes

| Mode | Toggle | Panel Size | What It Adds |
|---|---|---|---|
| **Standard** | Always on | 340 px wide | 4-op arithmetic, %, +/−, backspace, decimal |
| **Scientific** | 🔬 header button | +210 px (total 616 px) | sin, cos, tan, ln, log, x^y, √, x², 1/x, π, e, DEG/RAD |
| **Graphing** | 📈 header button | +300 px (total 710 px) | Canvas graph plotter, pan/zoom/reset |
| **Scientific + Graphing** | Both active | 936 px | Full workstation layout |

Panel widths animate with a smooth `cubic-bezier(0.25, 1, 0.3, 1)` spring easing.

---

## 🔢 Standard Calculator Features

| Feature | Detail |
|---|---|
| Basic Operations | +, −, ×, ÷ |
| Percentage | `%` key |
| Sign Toggle | `+/−` key |
| Decimal Input | `.` key (prevents double decimal) |
| Backspace | ⌫ key |
| Clear | `AC` / `C` (context-aware) |
| Chained Operations | Supports sequential operator chaining |
| Keyboard Support | Full keyboard mapping (0–9, operators, Enter, Backspace, Escape) |

---

## 🔬 Scientific Panel Features

| Function | Button |
|---|---|
| Trigonometry | sin, cos, tan (DEG or RAD) |
| Logarithm | ln (natural), log (base-10) |
| Power | xʸ (binary operator) |
| Square Root | √ |
| Square | x² |
| Reciprocal | 1/x |
| Constants | π, e |
| Angle Mode | DEG ↔ RAD toggle (persisted, indicator shown in display) |

---

## 📈 Graphing Panel Features

| Feature | Detail |
|---|---|
| Formula Input | Text bar — type any expression (e.g. `sin(x)`, `x^2`) |
| Plot Button | Renders the curve on canvas instantly |
| Zoom In / Out | Scales by ×1.3 or ×0.7 per click |
| Pan | Click-drag on canvas to move the origin |
| Reset View | Returns to default scale & origin |
| Responsive Canvas | Auto-resizes with the calculator width |
| Grid & Axes | Faint grid lines + axis lines with theme-aware colors |

---

## 💾 Memory Register (MC / MR / M+ / M− / MS)

| Button | Action |
|---|---|
| **MC** | Memory Clear — resets to 0 |
| **MR** | Memory Recall — loads stored value |
| **M+** | Adds current value to memory |
| **M−** | Subtracts current value from memory |
| **MS** | Memory Store — saves current value |

Memory value is **persisted in `localStorage`**. A **"M" badge** appears in the display when memory ≠ 0.

---

## 📋 History Drawer

| Feature | Detail |
|---|---|
| Slide-up Sheet | Animates up from bottom of calculator card |
| Entry Display | Shows expression + result for every calculation |
| Tap to Recall | Click any history entry to reload its result |
| Copy Button | Per-entry copy-to-clipboard icon |
| Clear History | Trash icon wipes all entries |
| Persistence | Saved to `localStorage` across sessions |

---

## ✨ Micro-Animations & Visual Effects

| Effect | Trigger |
|---|---|
| **Ripple Wave** | Every button press |
| **Success Sparks** | Emitted from display on `=` press (16 particles) |
| **Button Press Spring** | `scale(0.93) translateY(1px)` on `:active` |
| **Operator Highlight** | Active operator button glows with accent color |
| **Display Font Scaling** | Shrinks automatically for long numbers (54px → 34 → 24 → 19px) |
| **Background Particles** | Continuous canvas animation (theme-specific) |
| **Theme Transition** | Smooth 0.8s color interpolation across all elements |

---

## 🔊 Audio / Haptics Engine

| Feature | Detail |
|---|---|
| Web Audio API | Synthesized click sounds (no audio files needed) |
| Theme-specific sounds | Each theme has a unique oscillator waveform + frequency envelope |
| Mute Toggle | Speaker icon in header, state saved in `localStorage` |

---

## ⌨️ Keyboard Shortcuts

| Key | Action |
|---|---|
| `0–9` | Digit input |
| `+`, `−`, `*`, `/` | Operators |
| `Enter` or `=` | Calculate |
| `Backspace` | Delete last digit |
| `Escape` | Clear all (AC) |
| `.` | Decimal point |

---

## 💾 LocalStorage Persistence

| Key | Stores |
|---|---|
| `calci_theme` | Active theme name |
| `calci_audio` | Sound on/off |
| `calci_history` | Array of past calculations |
| `calci_scientific` | Scientific panel open/closed |
| `calci_graphing` | Graphing panel open/closed |
| `calci_memory` | Memory register value |
