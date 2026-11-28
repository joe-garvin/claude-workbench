# Before and after

Changes from refreshing pages Claude had built for me earlier, in November 2026. Each entry names the kind of page, what was wrong, what changed, and the rule behind it. The pages themselves are private, so these are written descriptions rather than screenshots.

## Weekly music digest page

- **Before:** a monospace font for labels, numbered section labels, Title Case section names, and more than one accent color.
- **After:** Familjen Grotesk throughout, the cool neutral palette below, cobalt as the one accent, no numbered or mono labels, and sentence-case section names.
- **Rules:** banned stock styles, one accent per view, sentence case.

## Task dashboard, light mode

- **Before:** faint secondary text that failed contrast, a page gray so close to the card color that cards didn't separate, checkbox outlines too pale to see, and a heavy navy panel that dominated the light theme.
- **After:** secondary text darkened until it passed, the page gray deepened, checkbox outlines raised to 3.3:1, and the navy panel turned pale indigo in light mode only. Dark mode was left alone.
- **Rules:** APCA contrast (muted text has to pass), non-text controls at 3:1 or better, depth from surface shifts.

## Reading-list page

- **Before:** a cream "book paper" background.
- **After:** a faint warm neutral gray. It keeps a bookish feel without the stock cream look.
- **Rule:** no cream or off-white backgrounds.

## Long-form reading site

- **Before:** a blurred, translucent top bar over body text.
- **After:** a solid top bar. The site's two book serifs stayed, because neither is on the banned list and both suit long reading.
- **Rule:** translucent bars only on floating navigation, and opaque material behind dense text.

## Diagram page with an animated connector

- **Before:** a wire animation that looped on its own with no way to stop it.
- **After:** the animation no longer plays automatically.
- **Rule:** motion that plays on its own is non-essential, pauses off-screen, and gets a pause control past 5 seconds.

## Personal site

- **Before:** IBM Plex Mono for small labels and metadata.
- **After:** labels set in the site's serif at 15px in a soft ink color, and the mono font removed from the site. Alpha hairlines, a tinted paper background, a 14px minimum, and a dark mode came in the same pass. Choices I had marked as deliberate, like a background gradient and a grain texture, stayed as they were.
- **Rules:** no monospace labels, 14px minimum, theme toggle, and marked choices override the rules.

## Music production boards

- **Before:** DAW-style meter ticks and clip numbers below 14px, and a different color for each sound lane.
- **After:** the small ticks kept a written 12px exception, because they imitate hardware and aren't read as text. The lane colors stayed as data, not as extra accents.
- **Rules:** 14px minimum with written exceptions, one accent per view (data colors don't count).

## A palette that worked

The cool neutral set used on most of the refreshed pages, in OKLCH. Hue stays at 250 and chroma stays low, so the grays read as tinted rather than dead.

| Role | Light | Dark |
|---|---|---|
| Page | `oklch(97% 0.004 250)` | `oklch(17% 0.008 250)` |
| Strip or panel | `oklch(94.5% 0.005 250)` | `oklch(21% 0.009 250)` |
| Ink (headings) | `oklch(20% 0.01 250)` | `oklch(94% 0.005 250)` |
| Body text | `oklch(30% 0.01 250)` | `oklch(86% 0.006 250)` |
| Muted text | `oklch(47% 0.012 250)` | `oklch(74% 0.01 250)` |
| Accent (cobalt) | `#003B8E` | `oklch(78% 0.1 260)` |

A type scale that worked for dense app pages: 14px metadata, 16px body, 18px semibold panel titles, and 22px semibold view titles, all in Familjen Grotesk.
