# UI craft research rules

The research behind the `ui-craft` skill: specific, checkable design details that keep pages, artifacts, and UIs Claude builds from looking machine-made, grouped by topic. Each rule names its source, and full links are at the end. The skill carries the rules that have held up in real builds, so a few rules here aren't in it yet.

## Process

From Charles Liu's [how to unslop](https://www.tiktok.com/@charles.unemployed/video/7712529370555927816).

- Gather references first: screenshots of sites you like or past work you're proud of. His sources: Construct Design, Mobbin, ScreensDesign, Spotted in Prod, Awwwards, One Page Love, Cosmos, Taste, Recent.
- Use familiar layouts (Jakob's law). Look at how comparable apps solve the screen before inventing one.
- Get the layout and flow right in a wireframe before choosing fonts and colors.
- For new designs, sketch several clearly different directions and combine the best parts, rather than polishing the first idea.

## Stock styles to avoid

Many of these are fine on their own. The tell is reaching for them by default.

- No purple-to-blue gradients, cyan on dark, or neon glow (Impeccable).
- No gradient text on headings or metrics (Impeccable).
- No large rounded icon above every heading (Impeccable).
- No pulsing "live" dots or sparkle icons as decoration (Charles Liu, [AI design trends](https://www.tiktok.com/@charles.unemployed/video/7705095150845824257)).
- No endless marquees or logo tickers (Charles Liu, [things AI overuses](https://www.tiktok.com/@charles.unemployed/video/7703999846109318408)).
- No decorative flowcharts or detailed diagrams that carry no real information (Charles Liu).
- No dark gradient hero sections (Charles Liu).
- No trend textures by default: pixel loaders, dithering, ASCII images over video, Monet or Renaissance painting backgrounds, "classical" branding (Charles Liu).
- Don't wrap text around shapes as a flourish (Charles Liu).
- No squircles (Charles Liu).
- No breadcrumbs where there's no real hierarchy (Charles Liu).
- No subtitle under every heading, and no periods at the end of titles (Charles Liu).
- No confetti on success screens (Charles Liu, [thank-you screen](https://www.tiktok.com/@charles.unemployed/video/7706223830523546900)).
- Tie the background to the subject instead of a generic surface, like a sky behind a flight tracker's login (Charles Liu, [login makeover](https://www.tiktok.com/@charles.unemployed/video/7705480372376980754)).

## Surfaces and depth

- Nested corners: inner radius = outer radius − padding. Clamp at 0, and skip the math for pills and full circles (Charles Liu).
- Use alpha colors for borders, such as `rgb(0 0 0 / 0.12)` on light and `rgb(255 255 255 / 0.1)` on dark, so they pick up the background. On tinted backgrounds, shift borders toward the background hue (Charles Liu).
- Use fewer borders. Separate with spacing first, then a background shift, then a shadow, and reach for a border last. Shadows show depth, borders show structure (Refactoring UI; ui-skills playbook).
- Don't overuse dividers (Charles Liu).
- Build shadows from two or more layers rather than one blurry gray one (Vercel; Josh Comeau).
- Tint shadows toward the surface or background hue instead of pure black (Josh Comeau).
- Combine a hairline semi-transparent border with a soft shadow for crisp edges (Vercel).
- Don't wrap everything in cards, and don't nest cards. Use spacing and type for hierarchy (Impeccable).
- Avoid pure `#000` and `#fff`. Tint neutrals toward the palette (Impeccable).
- Give images a thin neutral outline, not a tinted ring (ui-skills playbook).
- A blurred, translucent bar belongs only on the floating layer of controls and navigation over scrolling content. Never use it in the content layer, and never stack one translucent surface on another (Apple HIG materials; Emil Kowalski's apple-design).
- Behind dense text, use a thicker, more opaque material. Keep thin, see-through material for chrome with little text (Apple HIG materials).
- Under `prefers-reduced-transparency: reduce`, raise the bar's opacity and drop the blur. Under `prefers-contrast: more`, use a near-solid background with a defined border (Emil Kowalski's apple-design).
- In dark mode, show depth with lighter surfaces, because shadows barely read. Set `color-scheme: dark` and a matching `theme-color` (Charles Liu).

## Color

- Build palettes in OKLCH. For a shade scale, hold chroma and hue and step lightness. For a set of accents, hold lightness and chroma and change hue. Keep chroma modest so colors stay in gamut (Charles Liu).
- High-chroma OKLCH values can fall outside sRGB. Check them in the oklch.com picker before shipping (Evil Martians).
- Define the palette before building: 8–10 grays, 5–10 shades of one primary, and semantic colors for success, warning, and error. Nine shades divides cleanly (Refactoring UI).
- Don't scatter many shades and opacities of one color (Charles Liu).
- Gray text on a colored background looks dead. Use a darker shade of the background's own hue (Impeccable).
- Derive state colors with relative color syntax so they stay in step with the base: `oklch(from var(--accent) calc(l + 0.08) c h)` for hover (Evil Martians).
- Hover, active, and focus states need more contrast than the resting state (Vercel).
- Don't rely on color alone for status. Pair it with a label (Vercel).
- No glow on primary buttons. Use contrast and spacing instead (ui-skills baseline-ui).
- Charts use color-blind-safe palettes (Vercel AGENTS.md).

### Gradients

- No gradients unless the page calls for one, and never more than two stops (ui-skills baseline-ui; Laith0003).
- Add an interpolation space so the midpoint doesn't go gray. `in oklch` keeps chroma but can drift out of gamut, so use `in oklab` for a clean two-color blend and `in oklch` when the gradient should travel through hues (Charles Liu; Chrome).
- When a gradient must look right in older browsers, precompute midpoints in a perceptual space and pass them as extra stops (Josh Comeau).
- Dark gradients band. Use a very subtle noise overlay or skip the gradient (Vercel AGENTS.md).

### Choosing the accent

- One accent color per view. Secondary actions stay neutral, and brand color is reserved for links and actions (ui-skills baseline-ui and playbook).
- Make the accent the brightest color on the page so nothing competes with it (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7712140213845331221)).
- Pick it from across the color wheel from the page's colors (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7708051977237761281)).
- Warm page, cool accent. Cool page, warm accent (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7708791593809104149)).
- On a dark page, go bright. On a bright page, go deep (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7712927216576908565)).
- Take the accent from the subject itself: the paint, the fabric, the light in the photo (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7711030809443994881)).
- Add the color the page is missing, not one you happen to like (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7707328470711422214)).
- Two colors that get along, then one that doesn't (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7708437849615453446)).
- If two colors fight for attention, lower the chroma of one (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7709208047117241607)).
- Squint test: if more than one thing stands out, there's too much brand color (Charles Liu, [reel](https://www.tiktok.com/@charles.unemployed/video/7711428163355577621)).

### Contrast

- Check text contrast with APCA. Body text needs at least Lc 75, ideally Lc 90. Other content text, like captions, buttons, and nav, needs Lc 60. Text above 36px needs Lc 45 (APCA Bronze Simple Mode; Vercel prefers APCA over WCAG 2). WCAG 2 AA stays the legal floor, but APCA judges dark mode better.
- Muted text still has to pass. Most AI-made pages fail here on secondary text (ui-skills playbook).

## Typography

- Body text on screen runs 15–25px, and 16–17px is a safe default. A 14px floor is a minimum for small text, not a body size (Butterick; Apple HIG, 17pt iOS default).
- Body line height is 1.2–1.45. Headings tighten toward 1.1. Leading goes down as size goes up, and text of three or more lines never gets tight leading (Butterick; Apple HIG; ui-skills playbook).
- Cap the measure at 45–90 characters, ideally 60–75. Set it once with `max-inline-size: 65ch` on text elements rather than per component (Butterick; ui-skills playbook; Every Layout).
- Tracking depends on size. Large display text gets slightly negative tracking, body stays at 0, and all caps or small caps get 5–12% extra (`letter-spacing: 0.05em`–`0.12em`) (Butterick; Apple WWDC via Emil Kowalski's apple-design skill).
- All caps only for less than a line, and never on headings above 14px (Butterick; Laith0003).
- Bold or italic as little as possible, and never both at once. Build hierarchy from weight and color before size, using two or three weights at most (Butterick; Refactoring UI).
- Avoid thin and light weights for interface text, especially at small sizes (Apple HIG).
- Separate paragraphs with a first-line indent or 4–10pt of space, never both (Butterick).
- Never underline except links (Butterick).
- Never fake small caps. Use them only when the font has real ones (`font-variant-caps`) (Butterick).
- Use monospace only for real code, not as a "techy" costume (Impeccable).
- Use `font-variant-numeric: tabular-nums` for numbers that change or get compared (Vercel; Jakub Krehel).
- Use `text-wrap: balance` on headings and `text-wrap: pretty` on body text to avoid widows (Vercel; Jakub Krehel).
- Use the right characters: curly quotes, a real ellipsis (…), en dash for ranges, em dash for breaks, × for dimensions, straight primes for feet and inches, real © and ™, and non-breaking spaces between numbers and units, such as `10&nbsp;MB` (Vercel; Butterick; Typewolf).
- Sentence case for UI labels and headings, and no Title Case Headlines (ui-skills playbook; Laith0003).
- Size text and text-adjacent spacing in `rem`, so a person's larger default text size scales the layout instead of breaking it (Apple HIG Dynamic Type, translated by Emil Kowalski).
- For reading pages, use a fluid type scale: about 1.2 at a 320px viewport and 1.25–1.333 at 1240px and up, interpolated with `clamp()` in `rem` so browser zoom still works (Utopia). For dense app UI, a hand-picked fixed scale is fine (Refactoring UI).

### Typefaces

- Use as few typefaces as possible. Before adding a second family, check whether the first one's weights, widths, and italics can do the job (Apple HIG; Google Fonts Knowledge).
- When pairing, look for shared x-height, stroke weight, and width with a clear difference in classification, usually a serif with a sans. A body face needs regular, italic, bold, and bold italic, with low stroke contrast and open apertures (Typewolf; Google Fonts Knowledge).
- Serifs suit editorial and reading pages, not dense dashboards or data tables (Laith0003).

## Layout and spacing

- Start with too much white space and remove it until it feels right (Refactoring UI).
- Use a non-linear spacing scale, such as 4, 8, 12, 16, 24, 32, 48, 64, and pick only from it. Put more space between groups than within them (Refactoring UI).
- Vary spacing to make rhythm instead of using one gap everywhere (Impeccable).
- Don't center everything. Left-align text and allow asymmetry (Impeccable).
- Don't stretch content to fill the screen. Give each element the width it needs (Refactoring UI).
- Break up identical card grids with different sizes or no containers (Impeccable).
- Align to a grid, a baseline, or an optical center, and nudge by a pixel when geometry looks wrong (Vercel).
- Not every button is primary. Use secondary, ghost, and text-link styles (Impeccable).
- For full-height sections, use `100dvh` with a `100vh` line above it as a fallback. Use `100svh` when the height must not jump as mobile toolbars move (Charles Liu).
- Horizontal scrollers show 16–32px of the next item so people know to scroll (ui-skills playbook). Fade carousel edges with `mask-image: linear-gradient(90deg, transparent, black 15% 85%, transparent)` (Charles Liu).
- Leave about 12px between adjacent bordered controls (ui-skills playbook).
- Fixed and sticky elements respect `env(safe-area-inset-*)` (Vercel AGENTS.md; ui-skills baseline-ui).
- Use a fixed z-index scale, not arbitrary numbers (ui-skills baseline-ui).
- Text containers survive long content: `min-width: 0` on flex children, `line-clamp` or a fade where space is tight (Vercel AGENTS.md; ui-skills playbook).
- Product shots on white: `mix-blend-mode: multiply` makes the white disappear, but only on light backgrounds. In dark mode it darkens the photo, so give the image its own light panel or use a cut-out (Charles Liu).
- Check every page at 360px, laptop width, and ultra-wide (Vercel AGENTS.md).

## Icons

- Outline icons by default, filled for the active state (ui-skills playbook).
- Match stroke width to the weight of adjacent text: about 1.5px beside regular text and 2px beside semibold. Color icons with `currentColor` (Charles Liu; ui-skills playbook).
- Icon-only buttons get an `aria-label`, and emoji are never icons (Vercel AGENTS.md; Laith0003).
- For icon swaps, blur the outgoing icon as it fades (`filter: blur(4px)`), paired with a small scale change. Drop the blur under `prefers-reduced-motion` (Charles Liu).

## Motion

- Animate only `transform` and `opacity`, and never use `transition: all` (Vercel; Impeccable).
- Default to ease-out, and skip bounce or elastic easing (Emil Kowalski; Impeccable). For drag and swipe, use critically damped springs, and add bounce only when the gesture carried momentum, like a flick (Emil Kowalski's apple-design).
- Interaction feedback finishes within 200ms, and exits run shorter than entrances (ui-skills baseline-ui and playbook).
- Respond on pointer-down, not on release (Apple WWDC via Emil Kowalski's apple-design).
- Don't animate things people see hundreds of times a day, such as a command menu (Emil Kowalski).
- Buttons scale to about 0.96–0.97 on press (Emil Kowalski; Jakub Krehel).
- Elements enter from a slightly smaller scale, not from 0 (Emil Kowalski).
- Anchor `transform-origin` where the motion starts, like a menu growing from its trigger (Vercel).
- Things leave the way they came. A panel that slides in from the right exits to the right (Apple HIG motion; Emil Kowalski's apple-design).
- Never lock input during a transition. Every animation can be interrupted or cancelled (Vercel AGENTS.md; Apple HIG motion).
- Motion that plays on its own must be muted and non-essential, pause when off-screen, and offer a pause control if it runs longer than 5 seconds (Vercel AGENTS.md; ui-skills baseline-ui).
- Avoid slow looping oscillation near one cycle every five seconds (0.2 Hz), which people are especially sensitive to (Apple HIG motion).
- Don't animate large `blur()` or `backdrop-filter` surfaces (ui-skills baseline-ui).
- Ease the switch between light and dark themes instead of jumping brightness (Emil Kowalski's apple-design).
- Stagger a hero's entrance by about 100ms on first load only, never on routine interactions (ui-skills playbook).
- Every animation has a `prefers-reduced-motion` variant (Vercel; Emil Kowalski).

## Interaction

- Hit targets are at least 24px, and 44px on touch. Extend small controls with a pseudo-element (Vercel).
- Visible focus rings with `:focus-visible`. Never `outline: none` without a replacement (Vercel).
- Mobile inputs use 16px text or larger to stop iOS zoom (Vercel).
- Never disable zoom with `user-scalable=no` or `maximum-scale=1` (Vercel AGENTS.md; Laith0003).
- Set `touch-action: manipulation` to stop double-tap zoom delay (Vercel AGENTS.md).
- Navigation uses real links, and in Claude artifacts the only shareable state is a plain `#hash` (Vercel AGENTS.md; Claude artifact page rules).
- Every form field has a visible label. Placeholder text is never the only label (ui-skills playbook; Laith0003).
- A loading button keeps its label and adds a spinner (Vercel AGENTS.md).
- Design the empty, loading, error, and dense states, not just the happy path (Vercel). An empty state offers one clear next action, not just an explanation (ui-skills baseline-ui).
- `cursor: pointer` only on things that are clickable, and anything that looks clickable is (Laith0003; Vercel AGENTS.md).
- Native `<select>` gets an explicit background and text color so it reads in dark mode on Windows (Vercel AGENTS.md).

## Content

- Replace "Label: value" pairs with phrasing where you can, such as "12 left in stock" instead of "In stock: 12" (Refactoring UI).
- Name the destination in link and button text. No "Learn more," "Click here," or "Get started" alone (Laith0003).
- No placeholder content tells: "John Doe," "Acme," round-number stats like "99.9%," or filler verbs like "elevate" and "unleash" (Laith0003).

## House defaults

Two rules that are my own choices rather than findings from the research.

- **Theme toggle.** Every page Claude builds gets a light/dark toggle. It follows the system theme (`prefers-color-scheme`) on first load, and a manual choice overrides it. One-off throwaway pages may skip the toggle.
- **Minimum text size.** No text below 14px, including captions, labels, and buttons. Mobile inputs stay at 16px or larger.

## Sources

- [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines), the broadest checklist. Also on GitHub as `vercel-labs/web-interface-guidelines`.
- [Rauno Freiberg's interface guidelines](https://interfaces.rauno.me/), the original document Vercel's grew from.
- [Jakub Krehel, make-interfaces-feel-better](https://skills.sh/jakubkrehel/make-interfaces-feel-better/make-interfaces-feel-better), a skill on concentric radius, optical alignment, shadows, icons, and motion restraint.
- [Emil Kowalski's design engineering skill](https://emilkowal.ski/skill) and his essays on [great animations](https://emilkowal.ski/ui/great-animations) and [good vs. great animations](https://emilkowal.ski/ui/good-vs-great-animations).
- [Impeccable anti-patterns](https://www.mintlify.com/pbakaus/impeccable/concepts/anti-patterns), a list of AI-slop fingerprints, each with a "do instead."
- [Josh Comeau, designing shadows](https://www.joshwcomeau.com/css/designing-shadows) and his [shadow palette generator](https://www.joshwcomeau.com/shadow-palette).
- [Chrome's guide to visual effects](https://developer.chrome.com/docs/modern-web-guidance/guides/visual-design/visual-effects), on color spaces for gradients.
- [Butterick's Practical Typography, summary of key rules](https://practicaltypography.com/summary-of-key-rules.html): body size, leading, measure, caps, punctuation.
- Refactoring UI (Wathan and Schoger), via [refactoringui.com](https://refactoringui.com/) and [Sébastien Lavoie's chapter notes](https://www.sglavoie.com/posts/book-summary-refactoring-ui/): hierarchy, spacing scales, palettes, fewer borders.
- Apple Human Interface Guidelines: [Typography](https://developer.apple.com/design/human-interface-guidelines/typography), [Materials](https://developer.apple.com/design/human-interface-guidelines/materials), [Motion](https://developer.apple.com/design/human-interface-guidelines/motion).
- [Emil Kowalski's apple-design skill](https://github.com/emilkowalski/skills/blob/HEAD/skills/apple-design/SKILL.md), WWDC talks (Designing Fluid Interfaces, The Details of UI Typography) translated for the web. MIT.
- [Vercel web interface guidelines, AGENTS.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/AGENTS.md), the full MUST/SHOULD/NEVER list.
- [ui-skills.com playbook](https://www.ui-skills.com/playbook) and [ibelick's baseline-ui skill](https://www.ui-skills.com/skills/ibelick/baseline-ui).
- [Laith0003 ux-skill, anti-patterns](https://github.com/Laith0003/ux-skill/blob/main/references/foundations/anti-patterns.md), 30 lintable AI fingerprints, each with a detection regex. The full linter has 152.
- [Evil Martians, OKLCH in CSS](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) and the [oklch.com picker](https://oklch.com).
- [APCA easy intro](https://git.apcacontrast.com/documentation/APCAeasyIntro) and [Bronze Simple Mode thresholds](https://readtech.org/ARC/tests/bronze-simple-mode/?tn=criterion).
- [Josh Comeau, make beautiful gradients](https://www.joshwcomeau.com/css/make-beautiful-gradients/).
- [Utopia, designing with fluid type scales](https://utopia.fyi/blog/designing-with-fluid-type-scales/) and the [type calculator](https://utopia.fyi/type/calculator).
- [Every Layout, axioms](https://every-layout.dev/rudiments/axioms/), on measure as a global `ch` rule.
- [Typewolf typography cheatsheet](https://www.typewolf.com/cheatsheet), [40 best Google Fonts](https://www.typewolf.com/google-fonts), and [Google Fonts Knowledge on pairing](https://fonts.google.com/knowledge/choosing_type/pairing_typefaces).
- [Charles Liu on TikTok](https://www.tiktok.com/@charles.unemployed), which mirrors his [Instagram reels](https://www.instagram.com/charles.unemployed/): AI-slop fingerprints, accent picking, process, and the [screenshot of craft rules](https://www.tiktok.com/@charles.unemployed/video/7708439548958723348) this research started from.
