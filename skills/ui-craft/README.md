# ui-craft

A Claude skill that applies a set of design rules whenever Claude builds or restyles a web page, HTML artifact, dashboard, or small site. The rules keep the result from looking machine-made: no stock AI styles, and a list of small, checkable craft details drawn from Vercel, Apple, Butterick, Refactoring UI, Emil Kowalski, Charles Liu, and others.

For a readable version of the same rules, see the [UI craft guide](../../guides/ui-craft.md).

## Usage

Add the `ui-craft/` folder to Claude as a skill. It applies to any page Claude writes. Two habits make it work well:

- Mark choices you want kept with a comment in the page's code, such as "my pick." Claude flags conflicts with those instead of changing them.
- When refreshing an existing page, Claude audits it first and lists each problem with a fix, then waits for your OK before editing.

The fonts default to three Google Fonts (Familjen Grotesk, EB Garamond, IBM Plex Mono), because Claude artifacts can only load fonts from Google Fonts or from files shipped with the page. Swap in your own if you host them.

## Contents

```
ui-craft/
├── SKILL.md                      the rules Claude loads
├── references/
│   └── research-rules.md         every rule with its source, a reading list, and a log
└── examples/
    └── before-and-after.md       refreshes of real pages, and a palette that worked
```
