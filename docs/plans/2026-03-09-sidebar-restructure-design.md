# Sidebar Restructure Design

**Date**: 2026-03-09
**Status**: Approved

## Problem

HappyCapy docs use 5 top tabs, each showing only 3-9 pages in the sidebar. This makes the site feel empty compared to reference sites like Trickle (help.trickle.so) which use a single sidebar with all content visible at once.

## Solution

Remove top tabs. Consolidate all 26 pages into a single sidebar with 5 logical groups. Remove 3 redundant index/overview pages. Move QQ Bot tutorial to Guides. Move Contact to Community. Rename "Use Cases" to "Community".

## New Sidebar Structure

### EN

```
Getting Started
  Welcome to HappyCapy          → index.mdx
  Quick Start                   → getting-started/quickstart.mdx
  FAQ                           → getting-started/faq.mdx

Guides
  Skills                        → guides/skills.mdx
  Multi-Agent                   → guides/multi-agent.mdx
  MCP                           → guides/mcp.mdx
  Automations                   → guides/automations.mdx
  Connect QQ Bot                → integrations/qq-bot.mdx

Best Practices
  General Tips                  → best-practices/general.mdx
  Developers                    → best-practices/developers.mdx
  Non-Technical Users           → best-practices/non-technical.mdx
  Product & Design              → best-practices/product-design.mdx
  Marketing                     → best-practices/marketing.mdx
  Data Analysis                 → best-practices/data-analysis.mdx
  Research                      → best-practices/research.mdx
  Team Collaboration            → best-practices/team-collaboration.mdx

Integrations
  GitHub                        → integrations/github.mdx
  Notion                        → integrations/notion.mdx
  VS Code                       → integrations/vscode.mdx

Community
  Skills Directory              → use-cases/skills-directory.mdx
  Discord Bot for Business      → use-cases/discord-bot-business.mdx
  Telegram Bot Skill            → use-cases/telegram-bot.mdx
  Contact Us                    → integrations/contact.mdx
```

### ZH

```
快速入门: Welcome / 快速开始 / FAQ
功能指南: Skills / Multi-Agent / MCP / 自动化 / 接入 QQ 机器人
最佳实践: (same 8 pages)
集成: GitHub / Notion / VS Code
社区: (same 3 cases + 联系我们)
```

### ZH-Hant

```
快速入門: Welcome / 快速開始 / FAQ
功能指南: Skills / Multi-Agent / MCP / 自動化 / 接入 QQ 機器人
最佳實踐: (same 8 pages)
整合: GitHub / Notion / VS Code
社群: (same 3 cases + 聯絡我們)
```

## Changes Summary

1. **docs.json**: Replace `tabs` with flat `groups` in each language
2. **Delete 3 index pages**: `best-practices/index.mdx`, `integrations/index.mdx`, `use-cases/index.mdx` (+ zh/ + zh-Hant/ = 9 files total)
3. **No file moves needed**: Files stay in their current paths; only navigation references change
4. Total: 23 pages visible in sidebar (down from 26, minus 3 index pages)
