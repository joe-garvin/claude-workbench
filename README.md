# Claude workbench

Skills, guides, and small projects I've built while working with Claude as a writer. I use all of them.

I'm Joe Garvin, a writer and content strategist. My work is at [joegarvin.com](https://joegarvin.com).

## Skills

Each skill is a folder with a `SKILL.md` that tells Claude when to use it and how. Some carry reference files, templates, and worked examples.

| Skill | What it does |
|---|---|
| [zinsser-writing](skills/zinsser-writing) | Reads a draft against the craft principles in William Zinsser's *On Writing Well* and reports what to cut, tighten, and restructure. |
| [style-comparison](skills/style-comparison) | Compares Claude's first draft with my finished version, works out what I changed and why, and logs the principles for next time. |
| [client-writing-outline](skills/client-writing-outline) | Builds a structured outline for a client deliverable, so the content plan can be reviewed before any drafting. |
| [prompt-optimizer](skills/prompt-optimizer) | Compresses a long, wandering brain-dump into a short prompt that's ready to run. |
| [skill-refiner](skills/skill-refiner) | Audits a skill that has outgrown one file and restructures it into references, templates, and examples. |
| [conversation-handoff](skills/conversation-handoff) | Writes a handoff note at the end of a session, so the work can continue in a new chat. |
| [meeting-debrief](skills/meeting-debrief) | Turns a raw meeting transcript into a debrief: what was decided, what's open, and what I need to do. |
| [task-triage](skills/task-triage) | Sorts the inbox of an Obsidian task list into the right sections with priorities, and waits for approval before moving anything. |
| [github-push](skills/github-push) | Saves a summary of the current conversation to a private notes repo, filed by project, area, resource, or archive. |
| [music-discovery-digest](skills/music-discovery-digest) | Runs a weekly new-music digest: pulls from several sources, scores releases against a taste profile, and publishes a page. |

Several are written around my own setup (an Obsidian vault, a notes repo, my name). To use one, add the folder to Claude as a skill, then read the file and change the names and paths to yours.

## Guides

- [Avoiding AI writing](https://joe-garvin.github.io/claude-workbench/avoid-ai-writing.html). A reference on what makes writing sound machine-made, how detection works, and how to edit it out. The source notes are in [guides/avoiding-ai-writing](guides/avoiding-ai-writing).
- [Knowledge base agent guide](guides/knowledge-base-agent-guide.md). How to build a Claude Code agent that researches a topic, judges its sources, and builds a body of notes over time.
- [Automated book notes](https://gist.github.com/joe-garvin/81b9332bdbf1adce95bf23dc1f90147f). A tutorial for turning a book file into structured notes with Claude, NotebookLM, and Obsidian.
- [Weekly music digest](https://gist.github.com/joe-garvin/1b57111a07c22b42a71ecb81473d7852). The design behind the music-discovery-digest skill.

The AI writing guide leans on other people's work, credited in the guide. One skill I use every day and didn't write is Conor Bronsdon's [avoid-ai-writing](https://github.com/conorbronsdon/avoid-ai-writing).

## Projects

- [Listening notes](https://joe-garvin.github.io/claude-workbench/listening-notes/). The pages the music digest skill publishes each week.
- [Tour de France 2026 tracker](https://joe-garvin.github.io/claude-workbench/tdf-2026/). A dashboard of standings, stage results, and watch times that refreshed itself during the race. The scraper and its tests are in [docs/tdf-2026/scraper](docs/tdf-2026/scraper).
