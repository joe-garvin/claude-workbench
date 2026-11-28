---
name: writing-gists
description: Use when someone wants to turn what happened across a Claude Code project or session into public write-ups, such as GitHub gists or blog posts. Mines the work for reusable methods, proposes a list, drafts each one for an outsider, and publishes only on the user's OK.
---

# Writing gists

This starts when the user wants to capture what happened across a whole Claude Code project, or a single session, and share it publicly as a GitHub gist (or a blog post, or a page in a repo). The job is to find the reusable methods buried in that work and write each one up so a stranger can follow it.

## What a gist is

A gist is a reusable method written for an outsider who starts with no context. It teaches the reader how to do something they could do in their own setup.

A project log is not a gist. A record of rounds on one specific thing (a 3D model, a video edit, a single report) stays in the project. If the only thing a reader could learn is "here is what this person made," it isn't a gist.

## Step 1: The user's earlier write-ups

If the user has published gists or posts before, read the most recent two or three in full for tone and level of detail. Ask for the link if you don't have it. Treat them as examples of quality, not as a template. If they all share a rigid skeleton (a "Phase 1, Phase 2, Phase 3" outline, say), don't copy it unless the user wants it.

If there's nothing earlier to read, ask whether they have a style guide or writing rules, and use those.

## Step 2: Mining the work

Read what the project or session produced. Depending on the setup, that can mean a brief or README, CLAUDE.md, logs and changelogs, prompt files, style or taste files, notes the project keeps for itself, and the transcript when it's a single session. Look for three things:

- Methods that worked and could be repeated somewhere else.
- The artifacts that made them work, such as a prompt, a file layout, an instruction block or a table.
- Things that failed, and what replaced them.

## Step 3: A list before any drafting

Propose a short list of candidate gists in the conversation, each with a working title and a two- or three-sentence scope. Say which candidates you'd fold into another one as a section, and which look like project logs that shouldn't be gists. Let the user pick, merge or cut before you draft anything.

## Step 4: Drafting

Draft each chosen gist somewhere the user can read and edit comfortably: a shared document, a markdown file, or a doc or artifact pane if your environment has one. If the user edits the draft directly, read the current version before changing anything and keep their edits. If they leave comments, answer each one where it was left.

### Writing rules

- Write for an outsider. Keep internal project names, codenames and in-jokes out of the title and headings, and explain anything a newcomer wouldn't know.
- Keep the reader's situation and the author's apart. Use "you" for advice that applies to anyone, and first person for what happened in this particular project. Don't frame a detail that only fits the author as the reader's ("your 78 saved artists"). Check the whole draft for this.
- Open with a plain, descriptive H1 that says what the reader will build or learn, such as "Building a visual taste profile with Claude." Follow it with an intro paragraph, no heading.
- Use headings that are descriptive and spelled out, specific enough to understand on their own. "Reactions to the artists behind your saved images" works; "The artist round" or "The first draft" doesn't.
- Shape the sections to the content. No fixed outline, no phase scaffold.
- Show real artifacts in full where they carry the method: the instruction text, a prompt, a file's layout, a sample entry. Put anything the reader would paste in a code block.
- Include a section on mistakes and approaches that failed. Readers learn as much from these as from the parts that worked.
- Include a table of files only when the reader makes files. Skip it otherwise.
- Aim for about 1,500 to 2,000 words.
- Follow the user's own prose rules if they have them (banned words, punctuation habits, sign-offs). If they don't, write plainly and skip filler openings and summary endings.

### Privacy

Gists are public, and a secret gist is still readable by anyone with the link. Leave out the following unless the user explicitly OKs a specific item:

- Private notes, journals and personal writing.
- Contents of private repositories, internal hostnames, file paths and account names.
- Photos or likenesses of real people.
- Health, family and other personal matters, and anything from support or recovery groups.
- Client work and projects with coworkers or employers.
- API keys, tokens and anything else that grants access.

When a method came from private material, describe the method without the material.

## Step 5: Publishing on the user's OK

Never publish without the user's explicit OK, given after they've seen the final text. Then publish whichever way fits their setup:

- In a browser where the user is already signed in to GitHub, create a new public gist at gist.github.com. The user signs in themselves; never type a password or token.
- With the GitHub CLI, if it's installed and authenticated: `gh gist create --public --desc "<one line>" <filename>.md`.
- Anywhere else they publish, such as a blog or a repo's guides folder, following that place's usual process.

For a gist, use a one-line description of what the guide teaches and a lowercase, hyphenated filename ending in `.md`. Afterward, reload the page and check that the H1 and the first section render, then give the user the link.

If the project keeps finished outputs somewhere, save a copy of the final markdown there and note the link alongside it.
