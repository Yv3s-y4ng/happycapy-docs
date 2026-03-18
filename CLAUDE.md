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

All navigation, theme, colors, and language settings live in `docs.json`. This is the single source of truth for the site structure. When adding new pages, register them in `docs.json` under the appropriate group for each language.

## Content structure

Pages are `.mdx` files using Mintlify components (`<Card>`, `<CardGroup>`, `<Columns>`, `<Accordion>`, `<Note>`, `<Tip>`, etc.).

Top-level content directories (English):
- `getting-started/` — quickstart and FAQ
- `guides/` — Skills, Multi-agent, MCP, Automations
- `best-practices/` — audience-specific best practices (developers, marketing, etc.)
- `integrations/` — GitHub, Notion, VSCode
- `use-cases/` — community use cases (QQ bot, Discord bot, etc.)

## Localization

The site supports three languages, each mirroring the same directory structure:
- English: root level (`index.mdx`, `guides/`, etc.)
- Simplified Chinese: `zh/`
- Traditional Chinese: `zh-Hant/`

English is the source of truth. Chinese translations follow after English is finalized. Navigation entries for each language are defined separately in `docs.json` under `navigation.languages`.

## Writing style

### English — [humanizer](https://github.com/blader/humanizer/tree/main)

- No AI vocabulary: "additionally", "testament", "serves as", "delve", "it's worth noting"
- No chatbot pleasantries or disclaimer hedging
- No unnecessary bold, emojis, or formatting flourishes
- Use standard sentence-case headings
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
