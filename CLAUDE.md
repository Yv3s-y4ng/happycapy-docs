# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

The official documentation site for [Happycapy](https://happycapy.ai) — an agent-native browser computer powered by Claude Code. Built with [Mintlify](https://mintlify.com).

## Local development

```bash
# Install Mintlify CLI (once)
npm install -g mintlify

# Preview the docs locally
mintlify dev
```

The site runs at `http://localhost:3000` by default.

## Site configuration

All navigation, theme, colors, and language settings live in `docs.json`. This is the single source of truth for the site structure. A PostToolUse hook validates that `docs.json` remains valid JSON after every edit — if you break the JSON, the hook will block the change.

When adding a new page to `docs.json`, use forward slashes and omit the `.mdx` extension (e.g., `"features/desktops"`, `"locales/zh/features/desktops"`).

## Interacting with happycapy.ai via Chrome DevTools

The Happycapy app uses React. Standard `fill()` or `value =` won't trigger React state updates. Use this pattern:

```js
// 1. Inject text into the textarea
const textarea = document.querySelector('textarea[placeholder="Ask Happycapy"]');
const setter = Object.getOwnPropertyDescriptor(window.HTMLTextAreaElement.prototype, 'value').set;
setter.call(textarea, 'your message here');
textarea.dispatchEvent(new Event('input', { bubbles: true }));
textarea.dispatchEvent(new Event('change', { bubbles: true }));

// 2. Send — take a snapshot first, find the "Send message" button uid, then click it
```

This works via the `chrome-devtools-mcp` plugin's `evaluate_script` tool. After injecting, take a snapshot to get the send button's uid (it changes from "Enter a message" (disabled) to "Send message" once text is present), then click it.

## Content structure

Pages are `.mdx` files with YAML frontmatter (`title` and `description` required) using Mintlify components (`<Card>`, `<CardGroup>`, `<Frame>`, `<Columns>`, `<Accordion>`, `<Note>`, `<Tip>`, etc.).

Top-level content directories (English):
- `getting-started/` — quickstart, credits, FAQ
- `features/` — Desktops, Files, Skills, CLI, MCP, Automations, Agents, Multi-agent, Connect Mac, Capy Mail
- `best-practices/` — audience-specific best practices (developers, marketing, etc.)
- `integrations/` — GitHub, Notion (not currently in docs.json nav)
- `use-cases/` — community use cases (not currently in docs.json nav)

Images go in `/images/<section>/` (e.g., `/images/features/desktop-sessions.png`) and are referenced with absolute paths from the site root.

## Localization

The site supports three languages, each mirroring the same directory structure:
- English: root level (`index.mdx`, `features/`, `best-practices/`, etc.)
- Simplified Chinese: `locales/zh/`
- Traditional Chinese: `locales/zh-Hant/`

English is the source of truth. Chinese translations follow after English is finalized. Navigation entries for each language are defined separately in `docs.json` under `navigation.languages`.

**Every edit must touch all three languages in the same pass.** Chinese content lives under `locales/zh/` and `locales/zh-Hant/`, mirroring the English root structure. Never commit a change to one language without applying it to the other two.

## Workflow

### When to use plan mode

For any non-trivial change — new pages, navigation restructuring, multi-file updates — enter plan mode first. For single-sentence edits or typo fixes, skip planning and edit directly.

**Plan phase**: Define which files to create or modify, the content outline for each page, and what "done" looks like (e.g., registered in `docs.json`, all three languages updated).

**Execute phase**: Implement in focused chunks. Prefer smaller, coherent sprints over one giant pass.

**Evaluate phase**: Before finishing, check output against the writing style rules below. Self-evaluation is unreliable — treat the style rules as an external checklist, not a vibe check.

### Git commits

Do not add `Co-Authored-By: Claude` to commit messages.

### Multi-file changes

When a change touches multiple files (e.g., a new guide that needs English + zh + zh-Hant versions plus a `docs.json` entry), list all affected files in the plan before touching any of them. Don't start writing until the full scope is clear.

## Writing style

### English — [humanizer](https://github.com/blader/humanizer/tree/main)

- No AI vocabulary: "additionally", "testament", "serves as", "delve", "it's worth noting"
- No chatbot pleasantries or disclaimer hedging
- No unnecessary bold, emojis, or formatting flourishes
- Use Title Case for all headings: capitalize every word except articles (a, an, the), coordinating conjunctions (and, but, or, nor), and short prepositions (in, on, at, to, for, of, from, with) — unless first or last word. Verbs like "is", "are", "do" are always capitalized. Hyphenated words: capitalize both parts (e.g., "Real-World").
- Be direct and specific. If you can say it in one sentence, don't use three.
- Two-pass revision: humanize first, then audit for anything that still sounds AI-generated

### Chinese — [Humanizer-zh](https://github.com/op7418/Humanizer-zh)

Banned phrases: "此外" "至关重要" "持久的" "深入探讨" "强调" "复杂性" "标志着...关键时刻" "是...的体现" "专家认为" "观察者指出"

Banned structures:
- Forced three-part lists to appear thorough
- Excessive "不仅...而且..." parallel negation
- Formulaic "尽管...面临若干挑战" closings
- Synonym cycling to avoid repetition

Core rules:
- Delete filler phrases and preamble
- Mix sentence lengths — avoid monotonous rhythm
- State facts directly, don't over-explain
- No quotable "golden sentence" aphorisms
- Trust the reader
