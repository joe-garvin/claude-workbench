# UI craft

**Date:** 2026-11-23

The rules I give Claude when it builds web pages, HTML artifacts, dashboards, and small sites for me. They exist so the work looks chosen by a person rather than generated: no stock AI styles, and a set of small, checkable craft details drawn from people who have written carefully about interfaces. Credits are at the end.

To use it, paste it into a Claude project's instructions or knowledge, or turn it into a skill. Two habits make it work. Choices you mark in a page's code as deliberate (I use the comment "Joe's pick") override every rule here, and Claude should flag the conflict rather than change them. When refreshing an existing page, Claude audits first, lists each problem with its fix, and waits for an OK before applying them in one batch.

Claude artifacts can only load fonts from Google Fonts or from files shipped with the artifact, which shapes the font rules below. Outside artifacts, the same rules apply with more font choices.

## Fonts

### Banned

Inter, Roboto, Arial, Instrument Serif, Fraunces, Playfair Display, Geist, Space Grotesk, Bricolage Grotesque, Instrument Sans, JetBrains Mono, Space Mono. Refreshes also replaced Inter Tight and Public Sans as too generic.

### Approved for Claude artifacts

Claude artifacts can only load fonts from Google Fonts or from files shipped with the artifact. These Google Fonts are the defaults:

- Familjen Grotesk for sans, the default for UI. Use weights 400 and 600, with the stack `"Familjen Grotesk", ui-sans-serif, system-ui, -apple-system, "Segoe UI", sans-serif`.
- EB Garamond for serif. It's an editorial and reading face, not for dense dashboards or tables.
- IBM Plex Mono for mono, only for real code or data. Never for labels, eyebrows, or metadata.

### Self-hosted only

Switzer, Commit Mono, and Departure Mono are free but not on Google Fonts. Use them only where you self-host the files. Commit Mono is on npm as `@fontsource/commit-mono`.

Switzer's license (ITF Free Font License v2.0, as I read it in November 2026) allows self-hosting on your own sites. This is my reading, not legal advice. So:

- Switzer may ship as its official, unmodified WOFF2 files inside your own multi-file artifacts or sites.
- No subsetting, format conversion, or base64 `data:` URIs. That rules out Switzer in single-file artifacts.
- Never put Switzer files in a public repo, a skill other people install, or a template others use.
- For a page shared widely, Familjen Grotesk is the zero-risk choice.

### Paid fonts

Many of the fonts that read as chosen by a person come from paid foundries (Dinamo, Klim, Grilli Type, Commercial Type, Pangram Pangram, Displaay). Use one only with a licensed file.

### Type pairing

Use as few families as possible. Before adding a second family, check whether the first one's weights and italics can do the job. When pairing, look for shared x-height, stroke weight, and width with a clear difference in classification, usually a serif with a sans.

## Banned stock styles

Without design direction, never use:

- A cream, beige, or off-white page background (use a cool or faintly tinted neutral instead)
- Italic or highlighted accent words in headlines
- Numbered section labels like 01, 02, 03
- Monospace labels
- Pill-shaped buttons, tags, chips, or badges
- Tracked-out uppercase eyebrows
- Purple-to-blue gradients, cyan or neon on dark, glow effects, gradient text
- Glassmorphism and dotted-grid canvases
- A large rounded icon tile above every heading, or emoji as icons
- Identical card grids, nested cards, colored bars down card edges or across card tops, thick colored left borders on panels
- A row of big-number stat tiles when the page has no real metrics
- Metadata strung together with middle dots
- Centering everything
- Rust accents with big serif headlines (the stock "warm editorial" AI look)
- Placeholder content: "John Doe," "Acme," round-number stats like "99.9%," and filler verbs like "elevate" and "unleash"

## Color

- Build palettes in OKLCH. Shade scales hold chroma and hue and step lightness. Accent sets hold lightness and chroma and vary hue. Keep chroma modest so colors stay in the sRGB gamut, and check high-chroma values at oklch.com.
- Define the palette before building: 8 to 10 grays, 5 to 10 shades of one primary, and semantic colors for success, warning, and error.
- One accent color per view. Secondary actions stay neutral. Accent is reserved for links, selection, focus, and the one action that matters. A second brand color can act as the accent's deep shade (for example, links and pressed states) but not as a second accent.
- A rough proportion that works: about 85% tinted neutrals, 10% surface tint, ink for text, accent under 5%.
- Avoid pure `#000` and `#fff`. Tint neutrals toward the palette.
- Muted text on a colored background is a darker shade of that background's hue, not gray.
- Derive state colors with relative color syntax, such as `oklch(from var(--accent) calc(l + 0.08) c h)` for hover.
- Hover, active, and focus states have more contrast than rest. Status never relies on color alone.
- No gradients unless the page calls for one, and never more than two stops. Gradients always declare a space: `in oklab` for a clean two-color blend, `in oklch` when traveling through hues. Dark gradients band, so add faint noise or skip them.
- No glow on primary buttons.
- Charts use color-blind-safe palettes.

### Contrast

Check text contrast with APCA. WCAG 2 AA stays the legal floor, but APCA judges dark mode better.

- Body text: at least Lc 75, ideally Lc 90.
- Other content text (captions, buttons, nav, metadata): Lc 60.
- Text above 36px: Lc 45.
- Muted text still has to pass. Most AI-made pages fail on secondary text.
- Non-text controls such as checkbox outlines need at least 3:1.
- Bright accents often fail as small text. Coral on near-white measured about Lc 56, so small accent text uses a darker shade.


## Theme and dark mode

- Every page gets a light/dark toggle. On first load it follows the system (`prefers-color-scheme`). A manual choice overrides it and persists in `localStorage`. One-off throwaway pages may skip the toggle.
- Good toggle forms: a word ("dark" or "light") at the end of the nav, a sun/moon icon at top right, or a text button in a sticky header.
- Set `color-scheme` on `html` to match the active theme, with a matching `<meta name="theme-color">` for each theme.
- Load theme logic in the `head` so the page doesn't flash the wrong theme.
- Show depth with lighter surfaces, not shadows. Shadows can appear in light mode only.
- Ease the switch between themes instead of jumping brightness.
- Native `<select>` gets an explicit background and text color so it reads in dark mode on Windows.

## Typography

- Minimum text size is 14px everywhere, including captions, labels, buttons, and metadata. Mobile inputs use 16px or larger. Exceptions are rare and written down on the page, such as tiny SVG map labels, book spine labels, and DAW-style meter ticks.
- Body text runs 15 to 25px, and 16 to 17px is a safe default. The 14px floor is for small text, not a body size.
- Body line height 1.2 to 1.45 (1.45 is a good default). Headings tighten toward 1.1 to 1.2. Three or more lines never get tight leading.
- Cap the measure at 45 to 90 characters, ideally 60 to 75. Set `max-inline-size: 65ch` once on text elements.
- Size text and text-adjacent spacing in `rem` so browser zoom and larger default text work.
- For reading pages, use a fluid type scale (about 1.2 at 320px, 1.25 to 1.333 at 1240px and up) with `clamp()` in `rem`. For dense app UI, a fixed scale is fine. One that worked: 14px metadata, 16px body, 18px semibold panel titles, 22px semibold view titles.
- Tracking: large display text slightly negative, body at 0, all caps or small caps get 0.05 to 0.12em extra.
- All caps only for less than a line, and never on headings above 14px.
- Hierarchy from weight and color before size, with two or three weights at most. Never bold and italic at once. Avoid thin and light weights for UI text.
- Separate paragraphs with a first-line indent or space, never both. Never underline except links. Never fake small caps.
- `font-variant-numeric: tabular-nums` on changing or compared numbers, dates, counts, and times.
- `text-wrap: balance` on headings, `text-wrap: pretty` on body.
- Headings and UI labels in sentence case. No Title Case.
- Right characters: curly quotes, a real ellipsis, en dashes for ranges, em dashes for breaks, × for dimensions, real © and ™, and a non-breaking space between numbers and units (`10&nbsp;MB`).

## Surfaces

- Use fewer borders. Separate with spacing first, then a background shift, then a shadow, and a border last.
- Borders use alpha colors: `rgb(0 0 0 / 0.12)` on light, `rgb(255 255 255 / 0.1)` on dark. On tinted backgrounds, shift borders, shadows, and muted text toward the background hue. No hex border tokens.
- Shadows have at least two layers and are tinted toward the surface hue, not pure black. Pair a hairline alpha border with a soft shadow. Use shadows only on floating layers.
- Nested corners: inner radius equals outer radius minus padding, clamped at 0. A 6px radius on controls and rows and 10px on panels works well.
- Use spacing and type for hierarchy before reaching for a card. Don't nest cards.
- Images get a thin neutral outline, not a tinted ring.
- Blurred, translucent bars belong only on a floating layer of navigation over scrolling content. Never in the content layer, and never stacked. Behind dense text, use a more opaque material. Under `prefers-reduced-transparency: reduce`, raise opacity and drop the blur. Under `prefers-contrast: more`, use a near-solid background with a defined border. Several refreshes simply made the top bar solid.

## Layout and spacing

- Start with too much white space, then remove it.
- Use a non-linear spacing scale, such as 4, 8, 12, 16, 24, 32, 48, 64, and pick only from it. More space between groups than within them.
- Left-align text, allow asymmetry, and vary spacing to create rhythm.
- Don't stretch content to fill the screen.
- Align to a grid, baseline, or optical center. Nudge a pixel when geometry looks wrong.
- One primary button per view. Others are secondary, ghost, or text links.
- Full-height sections: `min-height: 100vh; min-height: 100dvh;`. Use `svh` when height must not jump. Side panels and rails use `dvh`.
- Fixed and sticky elements respect `env(safe-area-inset-*)`.
- Use a fixed z-index scale.
- Text containers survive long content: `min-width: 0` on flex children, `line-clamp` or a fade where space is tight.
- Horizontal scrollers show 16 to 32px of the next item. Carousels fade their edges with `mask-image: linear-gradient(90deg, transparent, black 15% 85%, transparent)`.
- Leave about 12px between adjacent bordered controls.
- Product shots on white get `mix-blend-mode: multiply` only on light surfaces. In dark mode, give the image its own light panel.
- Check every page at 360px, laptop width, and ultra-wide.

## Icons

- Few icons. Outline by default, filled for the active state.
- Stroke width matches adjacent text: about 1.5px beside regular text, 2px beside semibold. Color with `currentColor`.
- Icon-only buttons get an `aria-label`. Emoji are never icons.
- Icon swaps: the outgoing icon fades with `filter: blur(4px)` and a small scale change, with the blur dropped under reduced motion.

## Motion

- Animate only `transform` and `opacity`. Never `transition: all`.
- Default easing is ease-out. No bounce or elastic. Drag and swipe use critically damped springs, with bounce only after a flick.
- Interaction feedback finishes within 200ms. Exits run shorter than entrances.
- Don't animate things seen many times a day. No load-in animations or hover lifts on routine UI. A hero may stagger by about 100ms on first load only.
- Buttons scale to 0.97 on `:active` and respond on pointer-down.
- Elements enter from a slightly smaller scale, not from 0. Set `transform-origin` where the motion starts. Things leave the way they came.
- Never lock input during a transition. Every animation can be interrupted.
- Motion that plays on its own must be muted and non-essential, pause when off-screen, and offer a pause control if it runs longer than 5 seconds. Avoid slow loops near one cycle every five seconds.
- Don't animate large `blur()` or `backdrop-filter` surfaces.
- Every animation has a `prefers-reduced-motion` variant, usually a plain fade, which also drops blur.

## Interaction

- Hit targets at least 24px, 44px on touch. Extend small controls with a pseudo-element.
- Visible `:focus-visible` rings. Never `outline: none` without a replacement.
- Never disable zoom. Set `touch-action: manipulation`.
- Navigation uses real links. In Claude artifacts, the only shareable state is a plain `#hash`, which is a good place for the current selection.
- Every form field has a visible label. Placeholder text is never the only label.
- A loading button keeps its label and adds a spinner.
- Design empty, loading, error, long-name, and dense states. An empty state gets one line and one clear action.
- `cursor: pointer` only on clickable things, and anything that looks clickable is.
- Full keyboard use where it fits: arrows move, Enter selects, Esc closes.

## Copy and labels

- Sentence case everywhere. View and section names are plain nouns.
- No welcome text, taglines, or helper subtitles.
- Phrase facts instead of "Label: value." Write "12 left in stock" or "Weekly, Tuesdays 10 AM."
- Link and button text names the destination. Never "Learn more," "Click here," or "Get started" alone.
- No exclamation points or emoji in UI copy.
- Use realistic sample names and roles, never placeholders.

## Review pass

Before delivering any page, check it against every section above and fix what fails. A quick checklist:

1. No banned fonts. Fonts load from Google Fonts or shipped files.
2. No banned stock styles, especially cream backgrounds, mono labels, numbered labels, pills, and italic accent words.
3. Every text size is 14px or larger. Body is 16px or so.
4. Text passes APCA, muted text included, in both themes.
5. A theme toggle follows the system first and persists. `color-scheme` and `theme-color` match.
6. Borders are alpha. Shadows are layered and tinted. No pure black or white.
7. One accent per view, one primary button per view.
8. Motion uses transform and opacity, ease-out, under 200ms, with reduced-motion variants.
9. Focus rings, hit targets, labels, and the empty, loading, and error states are all present.
10. Choices the owner marked as deliberate are untouched, and any conflicts are flagged.

## Credits

- [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines) and the full [AGENTS.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/AGENTS.md)
- [Rauno Freiberg's interface guidelines](https://interfaces.rauno.me/)
- [Jakub Krehel, make-interfaces-feel-better](https://skills.sh/jakubkrehel/make-interfaces-feel-better/make-interfaces-feel-better)
- Emil Kowalski: [design engineering skill](https://emilkowal.ski/skill), [great animations](https://emilkowal.ski/ui/great-animations), and the [apple-design skill](https://github.com/emilkowalski/skills/blob/HEAD/skills/apple-design/SKILL.md)
- [Impeccable anti-patterns](https://www.mintlify.com/pbakaus/impeccable/concepts/anti-patterns)
- Josh Comeau on [shadows](https://www.joshwcomeau.com/css/designing-shadows) and [gradients](https://www.joshwcomeau.com/css/make-beautiful-gradients/)
- [Chrome's guide to visual effects](https://developer.chrome.com/docs/modern-web-guidance/guides/visual-design/visual-effects)
- [Butterick's Practical Typography](https://practicaltypography.com/summary-of-key-rules.html)
- [Refactoring UI](https://refactoringui.com/) by Adam Wathan and Steve Schoger
- Apple Human Interface Guidelines: [Typography](https://developer.apple.com/design/human-interface-guidelines/typography), [Materials](https://developer.apple.com/design/human-interface-guidelines/materials), [Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- [ui-skills.com playbook](https://www.ui-skills.com/playbook) and [baseline-ui](https://www.ui-skills.com/skills/ibelick/baseline-ui)
- [Laith0003 ux-skill anti-patterns](https://github.com/Laith0003/ux-skill/blob/main/references/foundations/anti-patterns.md)
- [Evil Martians, OKLCH in CSS](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) and the [oklch.com picker](https://oklch.com)
- [APCA](https://git.apcacontrast.com/documentation/APCAeasyIntro) and its [Bronze Simple Mode thresholds](https://readtech.org/ARC/tests/bronze-simple-mode/?tn=criterion)
- [Utopia fluid type scales](https://utopia.fyi/blog/designing-with-fluid-type-scales/), [Every Layout](https://every-layout.dev/rudiments/axioms/), and [Typewolf](https://www.typewolf.com/cheatsheet)
- [ITF Free Font License v2.0](https://www.fontshare.com/licenses/itf-ffl) for Switzer
