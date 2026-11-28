---
name: "ui-craft"
description: "Apply UI craft rules to every web page, HTML artifact, dashboard, site, or UI component Claude builds or refreshes, so the result looks chosen by a person rather than generated. Use whenever Claude writes HTML or CSS for a page, restyles an existing one, or reviews a page's design."
---

# UI craft

Apply these rules to every web page, HTML artifact, dashboard, site, or UI component you build or refresh, unless the user gives design direction that overrides them. They exist so the work looks chosen by a person rather than generated.

The full research behind each rule, with sources, is in `references/research-rules.md`. Worked refreshes are in `examples/before-and-after.md`. Read them when a rule here is unclear or a refresh needs a precedent.

## Working method

- Choices the user has marked as deliberate in a page's code (a comment such as "my pick" or "keep") override every rule here. Never change them. Flag the conflict instead.
- When refreshing an existing page, audit first. List each problem with its proposed fix and wait for an OK before editing. Then apply the changes in one batch.
- Before editing an existing artifact or page, note its current version so it can be rolled back.

## Fonts

Never use: Inter, Roboto, Arial, Instrument Serif, Fraunces, Playfair Display, Geist, Space Grotesk, Bricolage Grotesque, Instrument Sans, JetBrains Mono, Space Mono.

Claude artifacts can only load fonts from Google Fonts or from files shipped with the artifact. Default to these Google Fonts:

- Familjen Grotesk for sans, the default for UI. Weights 400 and 600.
- EB Garamond for serif, on editorial and reading pages only, not dense dashboards or tables.
- IBM Plex Mono for mono, only for real code or data.

Use any other font only where its license allows and the files are hosted with the page. Use a paid font only when the user supplies a licensed file.

## Banned stock styles

Without design direction from the user, don't use: a cream or off-white page background, italic accent words in headlines, numbered 01/02/03 section labels, monospace labels, pill-shaped buttons, tracked-out uppercase eyebrows, purple-to-blue gradients, cyan or neon on dark, glow effects, gradient text, glassmorphism, a large rounded icon above every heading, identical card grids, nested cards, colored bars on card edges, or centering everything.

## Surfaces

- Nested corners: inner radius = outer radius minus padding, clamped at 0. Skip for pills and circles.
- Borders use alpha colors: `rgb(0 0 0 / 0.12)` on light, `rgb(255 255 255 / 0.1)` on dark. On tinted backgrounds, shift borders, shadows, and muted text toward the background hue.
- Shadows have at least two layers and are tinted toward the surface hue, not pure black. Pair a hairline alpha border with a soft shadow.
- Avoid pure `#000` and `#fff`. Tint neutrals toward the palette.
- Use spacing and type for hierarchy before reaching for a card.
- A blurred, translucent bar belongs only on a floating layer of navigation over scrolling content. Never in the content layer, and never stacked. Under `prefers-reduced-transparency: reduce`, raise its opacity and drop the blur.

## Color

- Build palettes in OKLCH. Shade scales: hold chroma and hue, step lightness. Accent sets: hold lightness and chroma, vary hue. Keep chroma modest to stay in gamut.
- One accent color per view. Secondary actions stay neutral, and the accent is kept for links, selection, focus, and the one action that matters.
- No gradients unless the page calls for one, and never more than two stops. Gradients always declare a space: `in oklab` for a clean two-color blend, `in oklch` when traveling through hues.
- Muted text on a colored background is a darker shade of that background's hue, not gray.
- Hover, active, and focus states have more contrast than rest. Status never relies on color alone.

## Contrast

Check text contrast with APCA. WCAG 2 AA stays the legal floor.

- Body text: at least Lc 75, ideally Lc 90.
- Other content text (captions, buttons, nav): Lc 60.
- Text above 36px: Lc 45.
- Muted text has to pass too, in both themes.

## Theme and dark mode

- Every page gets a light/dark toggle. On first load it follows the system theme (`prefers-color-scheme`). A manual choice overrides it and persists in `localStorage`. One-off throwaway pages may skip the toggle.
- Show depth with lighter surfaces, not shadows.
- Set `color-scheme` on `html` to match the active theme, with a matching `<meta name="theme-color">`.

## Typography

- Minimum text size is 14px, including captions, labels, and buttons. Body text is about 16 to 17px.
- Body line height 1.2 to 1.45. Headings tighten toward 1.1.
- Cap the measure with `max-inline-size: 65ch` on text elements.
- Size text and text-adjacent spacing in `rem`.
- Tracking: large display text slightly negative, body at 0, all caps or small caps 0.05 to 0.12em extra.
- `font-variant-numeric: tabular-nums` on changing or compared numbers.
- `text-wrap: balance` on headings, `text-wrap: pretty` on body.
- Curly quotes, a real ellipsis, and a non-breaking space between numbers and units.
- Headings and UI labels in sentence case.

## Layout

- `min-height: 100vh; min-height: 100dvh;` for full-height sections. Use `svh` when the height must not jump.
- Left-align text, allow asymmetry, and vary spacing to create rhythm.
- Align to a grid, baseline, or optical center. Nudge a pixel when geometry looks wrong.
- One primary button per view. Others are secondary, ghost, or text links.
- Product shots on a white background get `mix-blend-mode: multiply` only on light surfaces. In dark mode, give the image its own light panel.
- Carousels fade their edges with `mask-image: linear-gradient(90deg, transparent, black 15% 85%, transparent)`.

## Icons

- Stroke width matches the weight of adjacent text. Color with `currentColor`.
- Icon swaps: the outgoing icon fades with `filter: blur(4px)` and a small scale change.

## Motion

- Animate only `transform` and `opacity`. Never `transition: all`.
- Default easing is ease-out. No bounce or elastic.
- Interaction feedback finishes within 200ms, and exits run shorter than entrances.
- Don't animate things seen many times a day.
- Buttons scale to 0.97 on `:active`. Elements enter from a slightly smaller scale, not from 0.
- Set `transform-origin` where the motion starts.
- Motion that plays on its own is muted and non-essential, pauses when off-screen, and has a pause control if it runs longer than 5 seconds.
- Don't animate large `blur()` or `backdrop-filter` surfaces.
- Every animation has a `prefers-reduced-motion` variant, which also drops blur.

## Interaction

- Hit targets at least 24px, 44px on touch. Extend small controls with a pseudo-element.
- Visible `:focus-visible` rings. Never `outline: none` without a replacement.
- Mobile inputs use 16px text or larger.
- Every form field has a visible label. Placeholder text is never the only label.
- Design empty, loading, error, and dense states.

## Content

- No placeholder giveaways: "John Doe," "Acme," round-number stats like "99.9%," or filler verbs like "elevate" and "unleash."
- Link and button text names the destination. Never "Learn more" or "Click here" alone.

## Review pass

Before delivering, check the page against every section above and fix what fails. When refreshing an existing page, list the violations you found and what you changed.
