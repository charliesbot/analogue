# Design System: Analogue

_A PWA for completing things, not collecting them. Vintage in vibe, restrained in density._

---

## ⚠ READ THIS FIRST — Non-Negotiable Rules for Stitch

Stitch has a documented tendency to silently substitute font specs it doesn't recognize (it has already replaced `Departure Mono` → Space Grotesk and `VT323` → Inter on this project). The following rules are **absolute and must survive every generation**. If a generated screen violates any of them, the output is wrong and must be regenerated.

### 1. Typography — MANDATORY

- **Heading / display / button-label / caption / all UPPERCASE readouts:** `VT323` (Google Fonts — https://fonts.google.com/specimen/VT323). No substitutes. Not Space Grotesk. Not Inter. Not Press Start 2P. **VT323.**
- **Body / review prose / input values / paragraph text:** `IBM Plex Mono` (Google Fonts — https://fonts.google.com/specimen/IBM+Plex+Mono). No substitutes. Not Inter. Not Roboto Mono.
- **There is no third font.** There is no sans-serif anywhere in this UI. There is no serif anywhere in this UI. The entire interface is monospaced.
- **If Stitch output shows Inter, Space Grotesk, Geist, Satoshi, Roboto, or any sans-serif — the generation failed.** Regenerate with the font requirement restated.
- Both fonts must be loaded via the Google Fonts link: `<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=VT323&display=swap" rel="stylesheet">`

### 2. Dashboard Layout — MANDATORY

- Four rows, stacked vertically. **One item per row. Always.** Never a 2×2 grid, never a 2-up, never a multi-column dashboard.
- Cover art is the hero of each row — square, large, left-anchored, CRT-treated (scanlines + chromatic fringe).
- The dashboard does not stretch on desktop. Max-width `560px`, centered, phone-shaped at every breakpoint.

### 3. No Progress Tracking — MANDATORY

- No progress bars, rings, percentages, chapter/page/playtime counters, "X of Y" widgets, or "resume" affordances anywhere inside an item's representation. Items are **backlog / active / completed / dropped** — four states, nothing in between.

### 4. No Chrome at Root — MANDATORY

- **Root dashboard has zero navigation chrome.** No top bar, no bottom tab bar, no hamburger menu, no side drawer, no floating action button, no wordmark, no logo, no app-name header, no settings gear, no search icon at root. The four rows are the entire interface.
- **The categories themselves are the navigation.** Tapping a row opens that category's detail view. There is no other nav.
- **Chrome only appears in nested views** — a thin top bar with a pixel-cursor-hand back affordance and the category sticker. Never persistent, never at the root.
- **Fewer decisions in front of the user, always.** If a control can be removed, remove it. If a decoration isn't load-bearing, delete it. The content is the app.

### 5. Palette — MANDATORY

- Warm cream canvas (`#F3EAD6`), warm ink (`#1F1B17`). **No pure black, no pure white, no cool grays, no purple neon, no gradients.**
- Category colors (Games `#E07A5F`, Music `#8FB5A5`, Books `#C9A57A`, Movies `#9B7FA0`) appear only in their own category's surfaces — never four competing accents on one screen.

### 6. No Emojis, No AI Clichés

- No Unicode emoji anywhere in the UI. Icons are SVG pixel-art stickers only.
- No "Elevate / Seamless / Unleash / Next-Gen" copy. No `LABEL // YEAR`. No fake metrics.

### How to prompt Stitch

When pasting this document into Stitch's context, **always restate rules 1–3 verbatim at the top of your prompt.** Stitch weights recent prompt text heavily; rules buried mid-document can be overridden by its defaults. Example opener:

> _"Fonts: VT323 for all headings, labels, buttons, and captions. IBM Plex Mono for all body text. Both Google Fonts. No Inter, no sans-serif, no serif — ever. Layout: four rows stacked vertically, one item per row, cover art as the hero. No progress bars or percentages. See DESIGN.md for full rules."_

---

## 0. Project Brief

Analogue is a four-slot media tracker — one active game, one album, one book, one movie. No feed, no streaks, no discovery. The product thesis is _presence_: you commit to what you're experiencing now, and the app asks you to reflect before moving on. See `docs/PRD.md` for full product context.

The design language borrows the **vocabulary of vintage personal electronics** — Poolsuite's cream-canvas tactility, Playdate/Poyo-color handheld chrome, IsaacOS pixel-sticker iconography, 90s desktop-OS micro-motifs — without ever becoming a skeuomorphic device frame. This is a flat, calm PWA that _feels_ like an object you'd hold.

**Reference screenshots** (design vocabulary source of truth, in `inspiration/`):

- `Screenshot 2026-03-30 at 8.02.11 PM.png` — Poolsuite twin-screens (cream/mint, CD, transport buttons, ALL-CAPS mono headers)
- `Screenshot_20260330-170046.png` — Poolsuite full app (channel dropdown, tactile transport row, sticker-tab navigation)
- `Screenshot 2026-04-19 at 5.05.39 PM.png` — Poyo Color handheld (CRT screen with chromatic fringe, pixel display font, colored bezel)
- `fpixM9jxzddfxLmPiITWjw.webp` — IsaacOS pixel stickers (CD, pixel cursor hand, CRT TV, outlined pixel logotype)
- `Screenshot 2026-03-30 at 7.34.49 PM.png` — existing Pencil wireframes (mono, bracket labels, folder/window metaphor)

---

## 1. Visual Theme & Atmosphere

A warm, paper-textured canvas holding four small pieces of vintage electronic chrome. The mood is **a weekend morning on a sunlit desk** — quiet, tactile, unhurried, slightly handmade. Every surface is low-saturation and matte; every interactive element has weight and depth. Cover art is the only "screen" in the experience, treated like a tiny CRT display set into the paper.

- **Density: 3 / 10 — Art Gallery Airy.** The dashboard shows four rows and nothing else. Breathing room is the loudest element — cover art is the hero, and it gets the space to _be_ the hero.
- **Variance: 5 / 10 — Offset Asymmetric.** The dashboard is a vertical stack of four rows, symmetric at the macro level; _inside_ each row, composition is asymmetric — a large square cover-art screen on the left, title and secondary metadata stacked to its right, sticker badge floating over the top-right corner, bracket caption anchored bottom-right. Nested views lean further asymmetric.
- **Motion: 2 / 10 — Static Restrained.** This project **overrides** the default perpetual-micro-motion rule. The product philosophy forbids attention-seeking animation. Motion is reserved for direct user input (button press, screen transition) and one thematic exception (cover-art CRT flicker, imperceptible). No pulses, no shimmers, no floating elements.
- **Creativity: 9 / 10.** The aesthetic is highly specific. Generic "dashboard card" patterns are forbidden.

### The "Quiet but Decorated" Discipline — First-Class Rule

This project lives in a tension the skill's defaults don't cover: it is visually _decorated_ (stickers, chrome, bezel vocabulary, pixel type, CRT texture) but emotionally _quiet_ (no gamification, no notifications, no streaks, no feed). Poolsuite is the reference — lots of chrome, very little content per screen, nothing blinks.

**Rule:** Decoration happens in _chrome_ (borders, bezels, stickers, labels, transport buttons). Decoration never happens in _state_ (no glowing CTAs, no bouncing badges, no celebratory confetti, no "You've completed 3 books this month!" surfaces). If you are tempted to add a pulsing dot, a progress ring, a streak counter, or a trophy — stop and delete.

### No Progress Tracking — First-Class Rule

Analogue does not track progress within an item. An item has exactly four states: **backlog**, **active**, **completed**, or **dropped**. There is no "45% through this book", no chapter counter, no playtime log, no pages-read, no "on hold", no partial-album marker. You are either experiencing the thing or you finished it (or you consciously walked away from it).

**Rule for every surface:**

- Never render a progress bar, progress ring, percentage number, page/chapter counter, playtime total, or "X of Y" completion widget inside an item's representation.
- Never render a "resume" or "continue from where you left off" affordance. The whole item is the unit; there is no partial state to resume.
- The only counters allowed anywhere in the UI are: backlog capacity (`[3/5]`), completed-history count (`// completed [12]`), dropped-log count (`// dropped [2]`), voice-recording elapsed time (`00:12`), and channel-style clock readouts. These count _items_ or _seconds of input_, never _progress within an item_.
- "Started on Feb 3" is metadata (when you began), not progress. It lives in the item detail view only — not on the dashboard slot, not on backlog list rows.

If Stitch generates a screen with a progress bar, chapter counter, reading-time estimate, or percentage glyph — regenerate. It violates the product thesis.

### No Chrome at Root — First-Class Rule

The root dashboard is **content-only**. No navigation, no branding, no decoration for decoration's sake. Every pixel the user sees on the dashboard must be either a slot row, the cover art inside a row, or the negative space around them. Nothing else belongs.

**Banned at root:**

- No top bar, no header, no app-name wordmark, no logo, no "Analogue" title anywhere.
- No bottom tab bar, no hamburger menu, no side drawer, no slide-out nav.
- No floating action button, no global "+", no search icon, no settings gear, no profile avatar.
- No breadcrumbs, no subtitle, no tagline, no welcome message, no "Hi, Charlie".
- No status pills, no count badges, no "4 items active" summary.
- No illustrations or hero graphics separate from the slot rows.

**Allowed at root:**

- The four slot rows (see §6 Slot Rows).
- The canvas grain (§5).
- That's it.

**Chrome only earns its place in nested views.** Category detail, item detail, add-item, completion review, and modals each get the minimum chrome they need — a pixel-cursor-hand back affordance, a category sticker as the title, and at most one contextual action. Nothing more.

**The underlying principle: fewer decisions in front of the user, always.** A navbar that only displays the app name is dead weight — the user already knows which app they opened. A settings icon the user visits once a year does not belong in the root surface. A search bar on a four-slot home is noise. When in doubt, remove it. The whole product thesis is presence, not choice architecture.

---

## 2. Color Palette & Roles

Warm, desaturated, paper-forward. All neutrals carry a cream/amber bias — **never cool gray.** No pure black, no neon, no gradients. Maximum saturation across the entire palette: **65%**.

### Canvas & Ink (System Neutrals)

| Token                | Hex                      | Role                                                                             |
| -------------------- | ------------------------ | -------------------------------------------------------------------------------- |
| **Paper Cream**      | `#F3EAD6`                | Primary background. Warm, slightly yellowed. Carries a 1–2% noise grain overlay. |
| **Paper Cream Deep** | `#EADFC6`                | Secondary surface (nested cards, input fills, inset panels).                     |
| **Ink Charcoal**     | `#1F1B17`                | Primary text and structural borders. Warm near-black, never `#000`.              |
| **Ink Muted**        | `#6B6055`                | Secondary text, metadata, timestamps, helper copy.                               |
| **Ink Whisper**      | `rgba(31, 27, 23, 0.14)` | Hairline dividers, disabled borders, soft separators.                            |
| **Shadow Warm**      | `rgba(31, 27, 23, 0.18)` | Button/slot drop shadow. Slightly warm-tinted, never neutral gray.               |

### Category Tokens (Contextual Accents)

Per-category accents. **These are not four competing brand accents** — a category color appears only inside that category's own surfaces (its slot on the dashboard, its detail view, its sticker background, its CTAs within context). On the root dashboard, they sit side-by-side as quiet cartridge colors, not as competing hotspots.

| Category | Token             | Hex       | Feel                                                      |
| -------- | ----------------- | --------- | --------------------------------------------------------- |
| Games    | **Coral Dust**    | `#E07A5F` | Warm, slightly ruddy. Arcade coral washed to matte.       |
| Music    | **Mint Cassette** | `#8FB5A5` | Muted teal-green. Poolsuite-adjacent.                     |
| Books    | **Tan Paperback** | `#C9A57A` | Warm pulp-paper tan. Pulls from Paper Cream but stronger. |
| Movies   | **Plum Dusk**     | `#9B7FA0` | Dusty violet-mauve. Never purple-neon.                    |

**Use-within-context rule:** inside the Games category view, Coral Dust is the CTA fill, the active-indicator color, the sticker backer. Inside Music, it's Mint Cassette. The four colors **do not mix** within a single nested screen.

### System Accent (Non-Category Actions)

| Token           | Hex       | Role                                                                                                                                                                                                      |
| --------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Rust Signal** | `#B85C38` | For system-level CTAs that aren't scoped to a category (global empty-state prompts, error confirmations, the "Drop it" destructive action). Used sparingly — often a category color will step in instead. |

### Banned Colors

- Pure black `#000000` — use Ink Charcoal.
- Pure white `#FFFFFF` — use Paper Cream.
- Any color with saturation > 65%.
- Purple-neon, blue-neon, any "AI gradient" violet.
- Cool grays (`#71717A` and the Zinc/Slate families). Analogue is warm-only.

---

## 3. Typography Rules

Two typefaces. No third. No serif anywhere. No sans-serif anywhere. The entire UI is monospaced — either pixel-bitmap or humanist mono.

**Google Fonts only.** Every font in this system must be available on [fonts.google.com](https://fonts.google.com). Stitch silently substitutes unknown font names with Space Grotesk or Inter, which destroys the entire aesthetic. If a font isn't on Google Fonts, it is not in this system.

### Display Pixel — `VT323`

A bitmap/CRT-terminal monospace with honest pixel edges — the classic green-phosphor-terminal silhouette. **Used exclusively for short display text:** section headings, category names, button labels, star-rating glyphs, recording timers, channel readouts, backlog/completed/dropped counters, empty-slot prompts.

- **Fallback stack:** `"VT323", "IBM Plex Mono", ui-monospace, monospace`
- **Sizes:** `14px`, `16px`, `18px`, `20px`, `24px`, `28px`. VT323 renders cleanly at these sizes. **Do not scale above 32px** — at larger sizes, pixel-bitmap fonts lose crispness; use weight (there's only `400`), casing, and letter-spacing to emphasize instead of size.
- **Casing:** ALL CAPS for major headers and readouts (Poolsuite convention — `[GAMES]`, `NOW PLAYING`, `08:42`). lowercase for sticker captions and snake_case labels (`[mark_complete]`).
- **Letter-spacing:** `0.04em` on ALL CAPS, `0` on lowercase.
- **Rendering:** `image-rendering: pixelated` is not applied to text (text is vector). VT323's own outlines carry the pixel silhouette.

### Body Mono — `IBM Plex Mono`

For any text longer than a button label: review prose, descriptions, metadata lines, input values, dialog body copy. Pixel display font would destroy readability for prose — this is the non-negotiable split.

- **Fallback stack:** `"IBM Plex Mono", "JetBrains Mono", ui-monospace, monospace`
- **Body size:** `15px` base, `line-height: 1.65`, max line length **60 characters** (monospace compresses naturally — 60 feels like ~72 proportional).
- **Weight range:** `400` regular, `500` medium, `600` semibold. No bold `700`.
- **Italic:** reserved for `//comment` microcopy only.

### Typographic Motifs (Required Conventions)

The following visual patterns are part of the product's voice. Use liberally but not redundantly.

- **Bracket labels** — `[games]`, `[backlog]`, `[5/5]`, `[mark_complete]`. Used as machine-readable captions beneath pixel stickers and as button labels. Always snake_case inside the brackets.
- **Comment microcopy** — `// you started this on feb 3` or `// 4 of 5 slots filled`. Italic, Ink Muted color, IBM Plex Mono. Used for context-sensitive metadata that would feel clinical as plain labels.
- **Channel-style readouts** — `CH.03`, `08:42`, `★★★★☆` (rendered via pixel-star glyphs, not Unicode). Display Pixel, ALL CAPS.

### Banned Typography

- **No Inter, no Geist, no Satoshi, no sans-serif at all.** This project is mono-only.
- **No serif.** No Fraunces, no Instrument Serif. (Row 1 and Row 5 of the Pencil exploration were rejected.)
- **No generic system fonts** (`system-ui`, `-apple-system`) as primary — only as fallback.
- **No text gradients, no text shadows** (except the single CRT-glow allowance on cover-art overlays — see §6).
- **No weight `700` or heavier.** The heaviest weight in the system is `600`.
- **No `LABEL // YEAR` patterns** (`SYSTEM // 2026`). That's lazy AI convention, not this project's voice. Use `// comment-style` prose instead.

---

## 4. Iconography & Stickers

Every category has **two parallel identifiers** that always appear together: a **pixel-art sticker** (primary glyph) and a **`[snake_case]` bracket caption** (accessible label). Never one without the other.

### Sticker System

SVG pixel-art, rendered at integer pixel scales (`image-rendering: pixelated`), sized to multiples of 4px so the pixel grid never smears. Each sticker has a solid category-color backer with a 1px Ink Charcoal outline and a soft Shadow Warm drop — the "peel-and-stick" Poolsuite/IsaacOS feel.

Core sticker set (minimum viable):

| Sticker                      | Use                                        | Visual                                                       |
| ---------------------------- | ------------------------------------------ | ------------------------------------------------------------ |
| **cartridge**                | Games category                             | Pixel Game-Pak silhouette, label strip in category color     |
| **cd**                       | Music category                             | Pixel CD with center-hole highlight and rainbow-sheen pixels |
| **paperback**                | Books category                             | Pixel book with spine + pages edge                           |
| **vhs**                      | Movies category                            | Pixel VHS cassette with label window                         |
| **cursor_hand**              | Back-navigation affordance in nested views | Classic Windows/Mac pixel pointer hand                       |
| **floppy**                   | Save / add-to-backlog action               | 3.5" floppy disk                                             |
| **crt**                      | Empty active slot illustration             | Pixel CRT television, static pattern on screen               |
| **star_filled / star_empty** | Rating glyphs                              | 5×5 pixel star, filled = category color, empty = Ink Whisper |

Stickers are **decorative chrome**, not emoji. They render as `<svg>` or `<img src="*.svg" class="pixelated">`. Never use Unicode emoji anywhere in the UI — see Anti-Patterns.

### Caption Pairing

```
[sticker]
[games]
```

Caption sits directly below the sticker, Display Pixel at 12px, Ink Charcoal, centered. On hover/focus of any sticker, the caption underlines in the category color.

---

## 5. CRT & Texture Treatment

Texture lives in two places only: the canvas (subtle paper grain) and cover art thumbnails (full CRT treatment). **Everywhere else is clean matte** — buttons, cards, inputs, stickers, text. No global scanlines.

### Canvas Grain

A fixed `::before` pseudo-element on `<body>` with a tiled noise PNG at 2–3% opacity, Paper Cream base. Gives the interface the feel of printed stock without interfering with text.

### Cover Art CRT Effect

Applied to every cover-art image in the app (dashboard slots, item details, backlog list, history list). This is the signature visual moment.

Recipe:

1. **Base image** — cover art from API (IGDB/TMDB/Google Books/MusicBrainz), CSS `filter: saturate(0.85) contrast(1.05)` to knock off stock-photo gloss.
2. **Scanline overlay** — a `::after` pseudo-element with `repeating-linear-gradient(0deg, rgba(31,27,23,0.12) 0 1px, transparent 1px 3px)`. 3px cycle, subtle.
3. **Chromatic fringe** — a duplicated image layer offset `+1px, 0` with `mix-blend-mode: screen` and a subtle red/cyan channel split (Poyo Color reference). Can be achieved with CSS `filter: drop-shadow(1px 0 0 rgba(224,122,95,0.5)) drop-shadow(-1px 0 0 rgba(143,181,165,0.5))`.
4. **Corner vignette** — radial-gradient `::before` at 15% opacity, darker at edges, suggesting CRT curvature.
5. **Optional flicker** — `@keyframes` 2s ease-in-out cycle on opacity `0.96 ↔ 1.0`. Imperceptible unless you stare. **Must honor `prefers-reduced-motion: reduce`** — if set, flicker is disabled.

Cover art always has **sharp 0px corners** — it's a CRT, not a card. The _container_ around it (the slot card) has the soft chrome; the screen itself does not.

### What NOT to Texture

- Text is never textured. No scanlines across body copy.
- Buttons are never textured. Matte paper fills only.
- Stickers are never CRT-treated — they're crisp pixel art.
- The canvas grain never exceeds 3% opacity.

---

## 6. Component Stylings

All components are built from the same vocabulary: thin ink outline, matte category/cream fill, soft warm drop shadow, crisp low-radius corners. No glassmorphism, no neumorphism, no gradient fills.

### Buttons (Default)

- **Shape:** 2px solid Ink Charcoal border, corner-radius `4px` (not round, not soft — crisp). Fill varies by context.
- **Size:** Minimum 44px tap target (`padding: 12px 20px` typical).
- **Label:** Display Pixel, ALL CAPS, 14px, letter-spacing `0.04em`.
- **Default (secondary):** Paper Cream fill, Ink Charcoal text.
- **Primary (in category context):** Category color fill, Ink Charcoal text and border.
- **Primary (system-level):** Rust Signal fill, Paper Cream text.
- **Drop shadow:** `2px 2px 0 Ink Charcoal` — hard offset, no blur. The button sits on the page like a sticker.
- **Active/pressed state:** translate `2px 2px` on press, shadow collapses to `0 0 0 Ink Charcoal`. 80ms ease-out. The button depresses into the page — tactile Poolsuite feel.
- **Disabled:** Ink Whisper border, Ink Muted text, no shadow, 60% opacity.
- **Focus ring:** 2px dashed outline in category color (or Rust Signal), offset 2px.

**No outer glow, no neon, no gradient fill, no rounded-2xl blobs.**

### Transport Buttons (Player Controls)

For the voice-transcription recorder and any playback context. Poolsuite-style chunky circular buttons with glyph centered.

- **Size:** 56px × 56px.
- **Shape:** `border-radius: 50%`, 2px Ink Charcoal border.
- **Fill:** Paper Cream Deep.
- **Glyph:** Pixel play / pause / record / stop, 24px, Ink Charcoal.
- **Shadow:** `3px 3px 0 Ink Charcoal` — more pronounced than default buttons. Hardware feel.
- **Active state:** same depress recipe, 3px offset collapse.
- **Recording (mic button):** fill becomes Rust Signal, glyph flips to a pixel waveform that animates (the _only_ perpetual animation allowed — see Motion). Stop button appears adjacent.

### Slot Rows (Dashboard)

Each of the four dashboard rows. **One item per row, always — never a two-up or grid layout.** Cover art is the hero of each row and must be given the room to look cool. This is the single most important layout rule in the app.

- **Shape:** `border-radius: 6px`, 1.5px Ink Charcoal border, Paper Cream fill.
- **Shadow:** `4px 4px 0 Shadow Warm` — sticker-like, offset hard shadow.
- **Row size:** fixed height of `180px` on phone, scaling to `200px` at ≥ 600px. Full available width (container handles max-width — see §7).
- **Internal gap:** `16px` between cover art and the text column.
- **Occupied layout (internal, horizontal):**
  - **Cover art:** left-anchored, square, `160px × 160px` on phone (`180px × 180px` at ≥ 600px). Fills nearly the full row height — this is the hero. CRT treatment per §5 (scanlines, chromatic fringe, corner vignette, optional flicker). Sharp `0px` corners — it's a screen, not a card. `16px` inset from the row's left/top/bottom edges.
  - **Pixel sticker badge:** floats over the top-right corner of the cover art, overlapping by ~8px (intentional Poolsuite "peeled sticker" move). `40px`, category-color backer, 1.5px Ink Charcoal outline.
  - **Text column:** starts right of the cover art's right edge + gap. Vertically centered in the row.
    - **Category bracket label:** `[GAMES]`, VT323, 14px ALL CAPS, Ink Muted, letter-spacing `0.04em`. Top of the text column.
    - **Title:** VT323, 22–24px (scales with row height), Ink Charcoal. Two-line max, truncates with `…`.
    - **Secondary metadata:** IBM Plex Mono, 14px, Ink Muted. Artist / author / developer / director. One line, truncates.
  - **Bracket caption:** `[games]` in lowercase, VT323, 12px, Ink Muted, anchored bottom-right of the row, 16px inset from edge. (The ALL-CAPS label at the top is the primary identifier; this lowercase caption is the quiet paired tag.)
- **Empty layout:**
  - Cover-art zone becomes a CRT-frame with static: same `160px`/`180px` square, 0px corners, Paper Cream Deep fill, thin Ink Whisper inner border. Centered inside: the `crt` pixel sticker at `56px` with static pattern, category-color backer at 40% opacity.
  - Text column right of it: `[GAMES]` category label at top as usual, then the prompt: `// your slot is empty` in IBM Plex Mono 14px Ink Muted italic, then `[add_game]` VT323 button-style caption with a faint hairline underline (the whole row is tappable; this reads as the CTA).
  - Row's outer border becomes dashed 1.5px Ink Whisper, replacing the solid border. On hover/focus: border firms up to solid Ink Charcoal, shadow extends by `2px`.
- **Tap behavior:** occupied → category detail view. Empty → add-item flow for that category.
- **No progress indicator of any kind** inside the row. No bar, no ring, no "started Feb 3", no elapsed days. The row shows _what_ you're experiencing, not _how far in_ you are (see §1 "No Progress Tracking").

### Inputs

- **Label:** Display Pixel, `[snake_case]` in brackets, 12px, Ink Charcoal, above the input.
- **Input field:** Paper Cream Deep fill, 1.5px Ink Whisper bottom border (no top/side borders — underline style). 15px IBM Plex Mono, Ink Charcoal text. Padding `10px 4px`.
- **Focus:** bottom border thickens to 2px Ink Charcoal, adds a 2px Ink Charcoal underline below (double-line effect — paper-form feel).
- **Helper microcopy:** `// optional field` style, Ink Muted italic, below input.
- **Error:** Rust Signal bottom border, Rust Signal helper text beneath starting with `// `.
- **No floating labels. No rounded pill inputs.**

### Review Component (Completion Flow)

The heart of the app. Warrants bespoke treatment.

- **Star rating:** 5 pixel stars, 32px each, category-color fill when active. Tap to set. Hover state fills to the hovered index. No half-stars.
- **Review textarea:** IBM Plex Mono 15px, line-height 1.7, min 5 rows, max-width 60ch. Paper Cream Deep fill, 1.5px Ink Whisper border, `6px` radius. Placeholder: `// what did you think? what stuck with you?` in Ink Muted italic.
- **Voice transcription button:** mic transport button (see above) positioned below the textarea, right-aligned. When recording, pixel waveform animates inside the button; timer counts up in Display Pixel below (`00:12`).
- **Submit:** primary button in category color — `[mark_complete]`.

### Drop Confirmation Dialog

Modal overlay, Paper Cream fill card centered on Shadow Warm scrim.

- **Header:** `// drop this?` Display Pixel, 16px, Ink Charcoal.
- **Body:** IBM Plex Mono 15px — `"You started this on Feb 3. It'll move to the dropped log. No review needed."`
- **Buttons:** `[cancel]` (secondary) + `[drop_it]` (Rust Signal primary). Right-aligned.
- **No destructive red flashing, no warning triangle emoji.** The moment should feel considered, not alarming.

### Loading States

Skeletal shimmer matching exact layout dimensions. **Override the skill default** — no perpetual shimmer animation. Instead, skeleton blocks are static Paper Cream Deep rectangles with an Ink Whisper border. If motion is absolutely required to indicate loading, use a single pixel dot scanning left-to-right along the bottom edge of the skeleton at 1s linear cycle.

**Never use a circular spinner.**

### Empty States

Composed pixel-sticker compositions, never just text.

- **Empty active slot:** `crt` sticker (pixel CRT with static) centered, caption `[add_game]`.
- **Empty backlog:** `floppy` sticker + `// your queue is empty. add up to 5.`
- **Empty completed history:** `paperback` sticker on a tiny pixel shelf, `// nothing finished yet.`
- **Empty dropped log:** no sticker, just `// nothing dropped. yet.` in Ink Muted italic — deliberately understated.

---

## 7. Layout Principles

- **Grid, never flexbox percentage math.** CSS Grid for the inside of each dashboard row (cover art column + text column); flex only for small inline groups (bracket captions, button clusters).
- **Root dashboard:** four rows stacked vertically, **always one item per row**. Never a 2-up, 2×2, or multi-column layout at any breakpoint. Row gap: `20px` on phone, `24px` at ≥ 600px. Container max-width: `560px` centered on desktop — the dashboard deliberately stays phone-shaped even on wide screens; it does not stretch into a wide layout. Full-width with `20px` horizontal padding on phone.
- **Nested views (category detail, item detail):** max-width `720px` centered. Desktop (≥ 960px) allows a 2-column split — active item + review form left, backlog/history/dropped right.
- **Root has no chrome.** No top bar, no wordmark, no nav. Dashboard = content only. Per design doc.
- **Nested views earn chrome.** Thin top bar with `cursor_hand` back-sticker (pointing left), category sticker centered, and optional contextual action (e.g., `[drop]` button) right-aligned. No hamburger, no bottom tab bar.
- **No overlapping elements.** Pixel stickers that overlap slot corners are the single exception (intentional Poolsuite move) — and the overlap is always into margin/padding, never onto text.
- **Min-height:** use `min-h-[100dvh]`, never `h-screen`.
- **Safe areas:** respect `env(safe-area-inset-*)` on all edges for PWA standalone.

### Responsive Rules

- **< 600px:** Dashboard is four stacked rows at `180px` row height. Cover art `160px` square, left-anchored. Text column fills remaining row width.
- **600–960px:** Same four-row stack. Row height grows to `200px`, cover art to `180px` square. Container max-width is `560px`, centered.
- **≥ 960px:** Dashboard stays at `560px` centered — it does not widen or switch to multi-column. The phone-shaped layout is intentional (this is a handheld-object vibe, not a widescreen dashboard). Nested views (category detail, item detail) are the only surfaces that expand into a 2-column split on wide screens.
- **Touch targets:** 44px minimum. Transport buttons 56px.
- **Headlines scale:** `clamp(16px, 2.2vw, 20px)` for Display Pixel — but never above 28px (pixel font degrades).
- **Body scale:** 15px on phone, 16px on desktop.

### Banned Layouts

- **No 3-column equal-card grids** ever. The dashboard is always four rows stacked one-per-row; nested views are 1-column or 2-column asymmetric split.
- **No centered-hero marketing sections.** This is not a marketing site.
- **No sticky headers, no sticky footers, no floating action buttons.**
- **No carousel / horizontal scroll on desktop.** Backlogs are vertical lists.

---

## 8. Motion & Interaction

**This project explicitly overrides the skill's perpetual-micro-motion default.** The product's core philosophy is quiet, non-attention-seeking UX. Motion must justify itself against that rule.

### Allowed Motion

- **Button press depress** — 80ms ease-out, 2–3px translate + shadow collapse. Every tactile button does this.
- **Screen transitions** — 220ms ease-out, slide + fade. Category detail slides up from dashboard, item detail slides in from right.
- **Modal enter/exit** — 180ms ease-out scale from `0.96 → 1.0` + scrim fade.
- **Sticker caption underline on hover** — 120ms ease-out.
- **Star rating fill on hover** — instant (no animation — it's a cursor-position indicator, not a state change).
- **CRT flicker on cover art** — 2s ease-in-out opacity cycle between `0.96` and `1.0`. Thematic. **Disabled under `prefers-reduced-motion: reduce`.**
- **Voice-recording waveform** — pixel waveform animates while mic is active. The only perpetual loop in the app. Stops the moment recording stops.

### Spring Physics (When Used)

When spring physics is used (modal enter, screen transition), use **stiffness: 180, damping: 26** — snappier and less bouncy than the skill default. Vintage mechanical feel, not iOS bouncy.

### Performance

- Animate only `transform` and `opacity`. Never `width`, `height`, `top`, `left`.
- CRT flicker uses `opacity` only. Grain uses a fixed pseudo-element, not a repainting layer.
- `will-change` declared on transport buttons and modal wrappers.

### Banned Motion

- **No perpetual pulse, shimmer, float, bounce, or breathing effects on idle UI.**
- **No loading spinners.** Skeletons only.
- **No stagger cascades on list mount.** Lists appear.
- **No parallax.**
- **No confetti, no celebratory animations on completion** — the review _is_ the celebration.
- **No hover scale on cards** — cards are static until tapped.

---

## 9. Screen Specifications

### 9.1 Dashboard (Root)

- Four rows stacked vertically, one category per row. Never a grid. Cover art is the hero of every row — generous square footprint, CRT-treated, the thing your eye lands on.
- No top bar. No wordmark. No navigation. `20px` horizontal padding on phone, container centered at `560px` max-width on larger screens.
- Each row renders as §6 "Slot Rows" spec.
- Order is fixed top-to-bottom: **Games → Music → Books → Movies**. Muscle memory matters.
- No dashboard-level progress, no elapsed-time, no "started Feb 3", no percentage. Only the cover, the category label, the title, the secondary metadata, and the sticker badge appear on the dashboard. Everything else is in the detail view.

### 9.2 Category Detail

- Thin top bar: `cursor_hand` back-sticker left, category sticker + `[games]` caption centered, no right action.
- **Active section:** large slot card rendering the active item with full metadata + primary `[mark_complete]` button and secondary `[drop]` + `[move_to_backlog]` links.
- **Backlog section:** heading `// backlog [3/5]` in comment style. List of backlog items with small cover art (CRT treated, 48px), title + secondary metadata, drag handle (pixel 6-dot icon). `[add_to_backlog]` button below.
- **Completed section:** collapsed by default. Heading `// completed [12]`. Expand reveals a chronological list with rating stars and truncated review preview.
- **Dropped section:** collapsed, quiet. Heading `// dropped [2]`. Expand reveals start/drop dates only, no reviews.

### 9.3 Active Item Detail

- Full-width cover art at top with CRT treatment.
- Title (Display Pixel, 24px) + secondary metadata (IBM Plex Mono, 14px Ink Muted).
- `// started on feb 3` comment-style timestamp.
- Primary `[mark_complete]` button (category color).
- Secondary cluster: `[move_to_backlog]`, `[drop]`.

### 9.4 Add Item Flow

- Search input at top (§6 spec), placeholder: `// search for a game…`
- Debounced results list below: small cover thumbnail (CRT treated), title, year, metadata line.
- Bottom of results: `// can't find it?` + `[create_custom]` button.
- Custom-entry modal: just title input + `[save]`.

### 9.5 Completion Review

- Title: `// finishing neuromancer` (Display Pixel, 16px).
- Cover art (CRT treated) centered, 40% width.
- Star rating row (§6 spec).
- Textarea (§6 spec) with placeholder `// what did you think? what stuck with you?`.
- Voice transcription button below textarea, right-aligned.
- Bottom buttons: `[cancel]` secondary, `[mark_complete]` category-color primary.

### 9.6 Drop Confirmation

- Modal per §6 spec.
- Copy specifically references the start date: `"You started this on Feb 3. It'll move to the dropped log. No review needed."`

### 9.7 Empty Slot Tap

- Tapping an empty slot on the dashboard opens the Add Item flow (§9.4) pre-scoped to that category. No intermediate screen.

---

## 10. Anti-Patterns (Explicit Bans)

Encode these into Stitch prompts as hard constraints.

### Typography & Content

- **No emoji** anywhere in the UI. Stickers are SVG pixel art, not Unicode.
- **No Inter**, no Geist, no Satoshi, no Cabinet Grotesk, no sans-serif at all.
- **No serif** — no Fraunces, no Instrument Serif, no Georgia, no Times.
- **No text gradients, no text shadows** (CRT cover-art overlay exempt).
- **No ALL CAPS for body prose** — reserved for Display Pixel headings/labels.
- **No `LABEL // YEAR`** formatting (`SYSTEM // 2026`). Use `//comment` prose instead.
- **No fake metrics** — no "3 books completed this month", no "7-day streak", no stats dashboard. The app is anti-gamification by contract.
- **No AI copywriting clichés** — no "Elevate," "Seamless," "Unleash," "Next-Gen," "Effortless."
- **No placeholder names** — use real or clearly-marked `[placeholder]`.

### Color & Visual

- **No pure black** `#000000`. Use Ink Charcoal `#1F1B17`.
- **No pure white** `#FFFFFF`. Use Paper Cream `#F3EAD6`.
- **No neon, no glow, no outer shadow blur on interactive elements.** All shadows are hard-offset, no blur (`4px 4px 0 Shadow Warm`).
- **No purple-neon or blue-neon gradients.**
- **No cool grays.** Every neutral is warm-biased.
- **No glassmorphism, no backdrop-blur, no translucent overlays.** The app is paper, not glass.

### Layout

- **No 3-column equal card grids.**
- **No bottom tab bar, no hamburger, no side drawer.**
- **No sticky headers or FABs.**
- **No marketing-hero centered sections.**
- **No carousels on desktop.**
- **No horizontal scroll on mobile.**

### Motion

- **No perpetual pulses, shimmers, floats, breathing effects.**
- **No loading spinners.**
- **No hover scale on cards.**
- **No confetti or celebratory flourishes on completion.**
- **No parallax.**
- **No stagger list mounts.**

### Product/UX

- **No streaks, no badges, no levels, no achievements.**
- **No "trending" or "recommended" sections.**
- **No social features, no share buttons, no external posting.**
- **No notifications, no "come back!" reminders.**
- **No progress tracking of any kind.** No percentages, no progress bars, no progress rings, no chapter/page/track counters, no playtime totals, no "X of Y" widgets, no "resume" or "continue" affordances. Items have four states: backlog, active, completed, dropped. See §1 "No Progress Tracking" for the full rule.
- **No device bezel or skeuomorphic hardware frame.** We _borrow_ device vocabulary (pixel type, CRT texture, tactile buttons) but do not _render_ a device.
- **No full-screen scanlines.** Scanlines are confined to cover-art thumbnails.

---

## 11. Stitch Prompting Notes

When generating screens with Stitch using this document:

1. **Always reference the two typefaces explicitly, by their exact Google Fonts names** — "VT323 for display, IBM Plex Mono for body. Both from Google Fonts." Stitch silently substitutes off-catalog font names (it replaced an earlier `Departure Mono` spec with Space Grotesk). If the font isn't on fonts.google.com, Stitch will not render it.
2. **State the category context first** — "This is the Music category view. Primary color is Mint Cassette `#8FB5A5`." Per-category theming is the whole game.
3. **Remind Stitch of the `quiet but decorated` rule** in any prompt that involves gamification-adjacent elements (progress, completion, achievement). Otherwise it will add a pulse, a badge, or a streak.
4. **Link inspiration screenshots** — attach the relevant reference image from `inspiration/` when asking for player controls (Poolsuite), cover-art treatment (Poyo Color), or sticker iconography (IsaacOS).
5. **Enforce the mono-only rule** — "No sans-serif anywhere. No serif anywhere. Mono + pixel mono only."
6. **Tell Stitch what NOT to render** — explicitly list the anti-patterns from §10 that are most likely to appear in the requested screen.

---

_This design system is the source of truth. When the product design-doc (`docs/PRD.md`) and this document disagree, this document wins on visuals, the design-doc wins on product behavior._
