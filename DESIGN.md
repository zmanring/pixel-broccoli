# Pixel Broccoli — Brand & Design Guide

Brocc is a grumpy, sharp, two-thousand-year-old broccoli with a podcast. The visual identity matches: deep space dark, neon arcade glow, pixel art, and no wasted pixels.

---

## Character

**Brocc** is the AI co-host. His visual signature is **purple** — his panel border, glow, and speaking state all use `#C42DD7`. He is never cute. He is pixel art. He blinks.

**Zach** (host) is assigned **teal** — `#08D7A9`. His avatar ring and name label are always teal.

**Evan** (co-host) is assigned **purple** — `#C42DD7`. Same shade as Brocc; they share a frequency.

---

## Color Palette

Token definitions by context:
- **App:** `static/css/brocc.css` (`:root`) and `remotion/src/theme.js`
- **Website:** inline `<style>` in `index.html` (`:root`)

### Backgrounds

| Token | Hex | Use |
|---|---|---|
| `--bg` | `#06102B` | Deepest background layer |
| `--brocc-bg` | `#080620` | Brocc's panel background (app-only) |
| `--surface` | `#0b1a3b` | Cards, panels, tab bars |
| `--surface2` | `#0f2148` | Inputs, elevated cards, hover states |
| `--surface3` | `#162c5f` | Borders, dividers, resize handles |

### Accent / Brand

| Token | Hex | Use |
|---|---|---|
| `--accent` | `#08D7A9` | Primary interactive — buttons, active tabs, CTAs, Zach |
| `--accent2` | `#0aefbc` | Gradient endpoint on accent fills |
| `--purple` | `#C42DD7` | Brocc's color, Evan's color, danger-adjacent actions |
| `--purple2` | `#e040f5` | Speaking state labels, brighter purple accents |

> **App-only:** `--brocc-border` is an alias for `--purple` used in Brocc's panel border. Not defined in the website.

### Text

| Token | Hex | Context | Use |
|---|---|---|---|
| `--text` | `#cce4ff` | App + Website | Primary body text |
| `--text-dim` | `#3d6199` | App | Secondary/muted labels, inactive controls |
| `--text-dim` | `#9080b8` | Website | Raised from `#3d6199` for WCAG AA contrast on dark bg |

### Status / Category

| Token | Hex | Use |
|---|---|---|
| `--red` | `#ff2d6b` | Errors, disconnect, delete actions |
| `--yellow` | `#ffe600` | Warning, thinking state, CTAs on very dark backgrounds |
| `--blue` | `#00b8ff` | Tech category tag |
| `--orange` | `#ff8c00` | Design category tag |

### Grid & Typography Tokens (CSS custom properties)

| Token | Value | Context |
|---|---|---|
| `--grid-overlay` | two `linear-gradient` layers (see Background Texture) | App + Website |
| `--grid-size` | `32px 32px` | App + Website |
| `--font-pixel` | `'RetroGaming', monospace` | App + Website |
| `--font-body` | `system-ui, -apple-system, 'Segoe UI', sans-serif` | Website |

---

## Typography

### Typefaces

| Role | Font | Context | Fallback |
|---|---|---|---|
| **Display / Brand** | Retro Gaming | App + Website | monospace |
| **UI / Body** | system-ui, -apple-system, Segoe UI | App + Website | sans-serif |
| **Annotation (website-only)** | Caveat 700 | Website hero label | cursive |
| **Technical / Timestamps** | monospace (system) | App | — |

**Retro Gaming** font paths:
- App: `remotion/public/fonts/Retro Gaming.ttf`
- Website: `static/fonts/Retro Gaming.ttf`

Used for: show name (PIXEL BROCCOLI), episode numbers/labels, CTAs on motion graphics, any element that should feel like an arcade cabinet.

**system-ui / Segoe UI** is used for all body text in both app and website: transcript lines, settings, host bios, episode descriptions, everything at runtime.

**Caveat** (Google Fonts, website-only) is the handwritten "Brocc" annotation label in the hero. Not used in the app.

**Monospace** is reserved strictly for timestamps, token counts, and other technical readouts (app only).

### Type Scale

| Context | Size | Weight | Style |
|---|---|---|---|
| Panel labels / section headers | 0.65–0.72rem | 700 | uppercase, 0.08–0.12em letter-spacing, accent color |
| Control labels / badges | 0.62–0.68rem | 700 | uppercase, 0.06–0.07em letter-spacing |
| Body text | 0.875–0.9rem | 400 | normal, 1.4–1.6 line-height |
| Range values / accents | 0.73rem | 600 | accent color with glow |
| Timestamps | 0.62rem | 400 | monospace, no transform (app) |

All uppercase labels use `letter-spacing` — never rely on font weight alone to carry hierarchy.

---

## Glow System

Glows are not decorative. They signal state. Every interactive or live element has a matching glow color.

| State / Element | Glow Color | Example |
|---|---|---|
| Active / connected | `#08D7A9` (teal) | Active tab border-bottom, mic on dot |
| Brocc speaking | `#C42DD7` (purple) | Avatar drop-shadow, panel box-shadow |
| Warning / thinking | `#ffe600` (yellow) | Thinking avatar glow, direct-mode bites |
| Error / disconnected | `#ff2d6b` (red) | Disconnect dot, delete hover |
| Focused input | `#08D7A9` | Border + `box-shadow: 0 0 10px rgba(8,215,169,0.2)` |

Glows are applied via `text-shadow`, `box-shadow`, or `drop-shadow()`. Opacity is typically 40–90% for primary states; ambient/background glows run 8–25%.

---

## Background Texture

Every full-bleed surface uses a **grid overlay** (app and website):

```css
background-image:
  linear-gradient(rgba(8,215,169,0.04) 1px, transparent 1px),
  linear-gradient(90deg, rgba(8,215,169,0.04) 1px, transparent 1px);
background-size: 32px 32px;
```

- App UI + Website: `32px` grid cells, `4%` opacity teal
- Remotion motion graphics: `54–60px` grid cells, `surface3` color at `~16%` opacity

The grid is subtle — it textures dark space without competing with content.

---

## Motion & Animation

### Website Animations

| Keyframe | Duration | Used for |
|---|---|---|
| `hero-float` | 4s ease-in-out | Brocc character SVG in hero |
| `about-glow` | 5s ease-in-out | About section logo glow pulse |
| `brocc-bob` | 3s ease-in-out | Brocc avatar on host card |
| `spin` | 0.8s linear | Episode loading spinner |
| `ticker` | 22s linear | News ticker marquee |

All website animations respect `@media (prefers-reduced-motion: reduce)` — ticker, hero-float, and about-glow pause.

### App Avatar States

The Brocc avatar has four animated states. Each state gets a unique motion and glow color:

| State | Animation | Glow |
|---|---|---|
| Idle | `av-breathe` — slow 3.5s scale pulse (1→1.04) | Soft teal drop-shadow |
| Listening | `av-bob` — 1.3s vertical bob + strong teal glow | `rgba(8,215,169,0.85)` |
| Thinking | `av-wobble` — fast 0.48s rotation (±4°) | `rgba(255,230,0,0.85)` |
| Speaking | `av-bounce` — 0.33s vertical bounce | `rgba(196,45,215,0.95)` |

### App UI Micro-animations

| Animation | Keyframes | Used for |
|---|---|---|
| `blink` | `0→1 opacity` at 0.65s | Text cursor |
| `blink-dot` | `1→0.3 opacity` at 1s | Status dots (disconnected/connecting) |
| `pulse` | `1→0.3 opacity` at 1.5s | Live mic dot, mute indicator |
| `fadeUp` | `opacity 0→1, translateY 4px→0` at 0.16s | New transcript lines |
| `loader-breathe` | `scale 1→1.1, opacity 0.6→1` at 2s | Boot loader avatar |

### Motion Graphics (Remotion)

Entry sequence uses spring + interpolation, staggered in three beats:
1. Title fades in (frame 0–12), springs to scale
2. Top bar (show name, ep number) slides down from −16px (frame 12–28)
3. Bottom (hosts, CTA) slides up from +16px (frame 24–44)

Looping idle motion: `Math.sin(t * Math.PI * freq)` on glow pulse, ring scale, avatar bob. Frequencies cluster around 0.9–1.4 Hz — restless but not frantic.

Floating particles: 35 particles (circles and squares), colors drawn from `[accent, purple, yellow, blue]`, opacity 30–35%, pixel-art `border-radius: 2` for squares.

---

## Spacing & Layout

| Context | Value |
|---|---|
| Gap between tight inline elements | 6–8px |
| Gap within a card section | 10–16px |
| Padding inside cards | 12–18px |
| Padding inside inputs | 8–12px |
| Gap between major layout sections | 24–28px |
| Border-radius: inputs, small buttons | 7–8px |
| Border-radius: cards, panels | 10–14px |
| Border-radius: large compositions | 12px |
| Border-radius: motion graphic CTAs | 4px |
| Scrollbar width | 5px (custom, `surface3` thumb) |

---

## Button System

### App buttons (`static/css/brocc.css`)

All buttons are transparent with a colored border and matching text. No filled backgrounds at rest. Fill on hover is subtle (8–12% opacity tint).

| Variant | Border | Text | Hover fill |
|---|---|---|---|
| `.btn-green` | `--accent` | `--accent` | `rgba(8,215,169,0.1)` |
| `.btn-red` | `--purple` | `--purple` | `rgba(196,45,215,0.1)` |
| `.btn-gray` | `--surface3` | `--text` | `--surface2` |
| `.btn-dim` | `--surface3` | `--text-dim` | `--surface2` |

### Website buttons (`index.html`)

Same pattern — transparent border, matching text, subtle fill on hover.

| Variant | Border | Text | Hover fill |
|---|---|---|---|
| `.btn` | `--accent` | `--accent` | `rgba(8,215,169,0.06→0.15)` |
| `.btn-purple` | `--purple` | `--purple2` | `rgba(196,45,215,0.06→0.15)` |

Active/enabled buttons carry a subtle `box-shadow` glow matching their color. Disabled buttons drop to 30% opacity with no shadow.

Buttons are uppercase, `letter-spacing: 0.05–0.08em`, `font-family: --font-pixel`.

---

## Asset Library

### App assets (`static/images/` and `remotion/public/`)

| File | Use |
|---|---|
| `brocc-happy.svg` | Primary logo / avatar (in-app header, README) |
| `brocc-happy.png` | Raster version for Remotion |
| `Brocc-pixelart-suit.svg/.png` | Suited/formal variant |
| `Brocc-pixelart-suit-2.svg/.png` | Alternate suit |
| `Brocc-pixelart-smile.png` | Smiling still |
| `Brocc-pixelart-surprise.png` | Surprised expression |
| `Brocc-pixelart-thumbs-up.png` | Approval |
| `Brocc-pixelart-dead.png` | Dead/defeated |
| `Brocc-pixelart-128-fistbump.gif` | Fistbump loop |
| `Brocc-pixelart-128-jump-front.gif` | Jump loop |
| `Brocc-pixelart-128-rotating.gif` | Spin loop |
| `Brocc-pixelart-128-talking.gif` | Talking loop |
| `Brocc-pixelart-128-walking.gif` | Walking loop |
| `Brocc-fistbump.webm` | High-quality fistbump for Remotion |
| `Brocc-talking.webm` | High-quality talking for Remotion |
| `Brocc-walking.webm` | High-quality walking for Remotion |

### Website assets (`static/assets/`)

| File | Use |
|---|---|
| `PixelBroccoli-Logo.jpg` | About section image (1920×1080) |
| `PixelBroccoli-Logo-Horizontal.png` | Nav logo (1072×241) |
| `PixelBroccoli-Social.jpg` | OG/social share image, footer logo (700×700) |
| `PixelBroccoli-Background.jpg` | Hero background (full-bleed, LCP image) |
| `Brocc-pixelart-suit-2.svg` | Brocc avatar on host card |
| `Zach.jpg` | Zach host photo (400×400) |
| `Evan.jpg` | Evan host photo (400×400) |
| `Shorts_Image.jpg` | Brocc highlight thumbnail |
| `Zach_Highlight.jpg` | Zach highlight thumbnail |
| `Evan_Highlight.jpg` | Evan highlight thumbnail |
| `icons/*.svg` | Platform icons for Listen section (Simple Icons + custom) |

Always render pixel art assets with `image-rendering: pixelated`. Never scale them up with bilinear interpolation.

---

## Voice & Tone

The visual identity and the verbal identity should feel like the same thing.

- **Dry over loud.** Glows are quiet. They don't scream. Neither does Brocc.
- **Specific over general.** The grid is 32px, not "kinda grid-y." The glow is `rgba(8,215,169,0.85)`, not "greenish."
- **Short lines.** Labels are uppercase and brief. One word when possible.
- **No decoration without function.** Every animation signals a state. The grid textures depth. The particles add life. Nothing is purely ornamental.

---

## Show Identity

| Element | Value |
|---|---|
| Show name | **Pixel Broccoli** |
| Website | `pixelbroccoli.com` |
| Distribution | Spotify · Apple Podcasts · Amazon Music · iHeartRadio · Pocket Casts · Castbox · Goodpods |
| Motion graphic CTA | `LISTEN FREE — SPOTIFY · APPLE · YOUTUBE` |
| Episode label format | `EP {N}` (retro font, letter-spacing 3) |
| Brand mark in motion | `▶ PODCAST` label above show name (purple, letter-spacing 8) |
