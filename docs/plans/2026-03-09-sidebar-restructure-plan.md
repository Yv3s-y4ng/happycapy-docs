# Sidebar Restructure Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Remove top tabs from HappyCapy docs and consolidate all pages into a single sidebar with 5 groups.

**Architecture:** Replace `navigation.languages[].tabs` with `navigation.languages[].groups` in docs.json. Delete 9 redundant index files. No file moves needed.

**Tech Stack:** Mintlify docs.json config, MDX files

---

### Task 1: Rewrite docs.json navigation

**Files:**
- Modify: `docs.json`

**Step 1: Replace the entire `navigation` object**

Replace the `navigation` key in docs.json with this structure (tabs removed, flat groups):

```json
"navigation": {
  "languages": [
    {
      "language": "en",
      "groups": [
        {
          "group": "Getting Started",
          "pages": ["index", "getting-started/quickstart", "getting-started/faq"]
        },
        {
          "group": "Guides",
          "pages": ["guides/skills", "guides/multi-agent", "guides/mcp", "guides/automations", "integrations/qq-bot"]
        },
        {
          "group": "Best Practices",
          "pages": [
            "best-practices/general",
            "best-practices/developers",
            "best-practices/non-technical",
            "best-practices/product-design",
            "best-practices/marketing",
            "best-practices/data-analysis",
            "best-practices/research",
            "best-practices/team-collaboration"
          ]
        },
        {
          "group": "Integrations",
          "pages": ["integrations/github", "integrations/notion", "integrations/vscode"]
        },
        {
          "group": "Community",
          "pages": ["use-cases/skills-directory", "use-cases/discord-bot-business", "use-cases/telegram-bot", "integrations/contact"]
        }
      ]
    },
    {
      "language": "zh",
      "groups": [
        {
          "group": "快速入门",
          "pages": ["zh/index", "zh/getting-started/quickstart", "zh/getting-started/faq"]
        },
        {
          "group": "功能指南",
          "pages": ["zh/guides/skills", "zh/guides/multi-agent", "zh/guides/mcp", "zh/guides/automations", "zh/integrations/qq-bot"]
        },
        {
          "group": "最佳实践",
          "pages": [
            "zh/best-practices/general",
            "zh/best-practices/developers",
            "zh/best-practices/non-technical",
            "zh/best-practices/product-design",
            "zh/best-practices/marketing",
            "zh/best-practices/data-analysis",
            "zh/best-practices/research",
            "zh/best-practices/team-collaboration"
          ]
        },
        {
          "group": "集成",
          "pages": ["zh/integrations/github", "zh/integrations/notion", "zh/integrations/vscode"]
        },
        {
          "group": "社区",
          "pages": ["zh/use-cases/skills-directory", "zh/use-cases/discord-bot-business", "zh/use-cases/telegram-bot", "zh/integrations/contact"]
        }
      ]
    },
    {
      "language": "zh-Hant",
      "groups": [
        {
          "group": "快速入門",
          "pages": ["zh-Hant/index", "zh-Hant/getting-started/quickstart", "zh-Hant/getting-started/faq"]
        },
        {
          "group": "功能指南",
          "pages": ["zh-Hant/guides/skills", "zh-Hant/guides/multi-agent", "zh-Hant/guides/mcp", "zh-Hant/guides/automations", "zh-Hant/integrations/qq-bot"]
        },
        {
          "group": "最佳實踐",
          "pages": [
            "zh-Hant/best-practices/general",
            "zh-Hant/best-practices/developers",
            "zh-Hant/best-practices/non-technical",
            "zh-Hant/best-practices/product-design",
            "zh-Hant/best-practices/marketing",
            "zh-Hant/best-practices/data-analysis",
            "zh-Hant/best-practices/research",
            "zh-Hant/best-practices/team-collaboration"
          ]
        },
        {
          "group": "整合",
          "pages": ["zh-Hant/integrations/github", "zh-Hant/integrations/notion", "zh-Hant/integrations/vscode"]
        },
        {
          "group": "社群",
          "pages": ["zh-Hant/use-cases/skills-directory", "zh-Hant/use-cases/discord-bot-business", "zh-Hant/use-cases/telegram-bot", "zh-Hant/integrations/contact"]
        }
      ]
    }
  ]
}
```

**Step 2: Verify JSON is valid**

Run: `cd /home/node/a0/workspace/245eba45-b9f7-4f6d-901c-2f4064bbfd44/workspace/happycapy-docs && node -e "JSON.parse(require('fs').readFileSync('docs.json','utf8')); console.log('Valid JSON')"`
Expected: `Valid JSON`

**Step 3: Commit**

```bash
git add docs.json
git commit -m "refactor: replace tab navigation with flat sidebar groups"
```

---

### Task 2: Delete redundant index pages

**Files:**
- Delete: `best-practices/index.mdx`
- Delete: `integrations/index.mdx`
- Delete: `use-cases/index.mdx`
- Delete: `zh/best-practices/index.mdx`
- Delete: `zh/integrations/index.mdx`
- Delete: `zh/use-cases/index.mdx`
- Delete: `zh-Hant/best-practices/index.mdx`
- Delete: `zh-Hant/integrations/index.mdx`
- Delete: `zh-Hant/use-cases/index.mdx`

**Step 1: Delete all 9 index files**

```bash
rm best-practices/index.mdx integrations/index.mdx use-cases/index.mdx
rm zh/best-practices/index.mdx zh/integrations/index.mdx zh/use-cases/index.mdx
rm zh-Hant/best-practices/index.mdx zh-Hant/integrations/index.mdx zh-Hant/use-cases/index.mdx
```

**Step 2: Commit**

```bash
git add -u
git commit -m "chore: remove redundant index pages no longer in navigation"
```

---

### Task 3: Push and verify

**Step 1: Push to remote**

```bash
git push origin main
```

**Step 2: Verify site loads at https://happycapy.mintlify.app/**

Open site and confirm sidebar shows 5 groups with all 23 pages visible.
