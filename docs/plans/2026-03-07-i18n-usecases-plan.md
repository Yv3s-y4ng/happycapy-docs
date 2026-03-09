# i18n + User Cases Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add zh/zh-Hant translations to all 21 existing English pages, add a Use Cases tab with overview page, and update docs.json to use Mintlify's i18n navigation.

**Architecture:** Mintlify's `navigation.languages` array wraps our existing `tabs` structure. English files stay at root. Chinese files in `zh/`, Traditional Chinese in `zh-Hant/`. Each language gets a full `tabs` definition with translated labels. Use Cases tab added as 5th tab with a single overview page per language. Content translated from Notion-exported HTML sources.

**Tech Stack:** Mintlify docs.json, MDX with Mintlify components (Card, CardGroup, Accordion, AccordionGroup, Steps, Step, Tip, Note, Warning, Columns)

---

## Reference Paths

- **Docs repo**: `/home/node/a0/workspace/245eba45-b9f7-4f6d-901c-2f4064bbfd44/workspace/happycapy-docs/`
- **Notion sources**: `/home/node/a0/workspace/245eba45-b9f7-4f6d-901c-2f4064bbfd44/workspace/happycapy 多语言/extracted/howtobestusai1-bilingual-docs-main/HappyCapy/`
- **Design doc**: `docs/plans/2026-03-07-i18n-design.md`

---

### Task 1: Update docs.json with i18n navigation + Use Cases tab

**Files:**
- Modify: `docs.json`

**Step 1: Rewrite docs.json navigation**

Replace `navigation.tabs` with `navigation.languages`. Keep all other config unchanged (theme, colors, background, logo, navbar, footer).

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "maple",
  "name": "HappyCapy",
  "colors": {
    "primary": "#F8A963",
    "light": "#fcfbf8",
    "dark": "#2e2929"
  },
  "background": {
    "color": {
      "light": "#fcfbf8",
      "dark": "#1a1a1a"
    }
  },
  "favicon": "/favicon.svg",
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "navigation": {
    "languages": [
      {
        "language": "en",
        "tabs": [
          {
            "tab": "Getting Started",
            "groups": [
              {
                "group": "Getting Started",
                "pages": ["index", "getting-started/quickstart", "getting-started/faq"]
              }
            ]
          },
          {
            "tab": "Feature Guides",
            "groups": [
              {
                "group": "Feature Guides",
                "pages": ["guides/skills", "guides/multi-agent", "guides/mcp", "guides/automations"]
              }
            ]
          },
          {
            "tab": "Best Practices",
            "groups": [
              {
                "group": "Overview",
                "pages": ["best-practices/index", "best-practices/general"]
              },
              {
                "group": "By Role",
                "pages": [
                  "best-practices/developers",
                  "best-practices/non-technical",
                  "best-practices/product-design",
                  "best-practices/marketing",
                  "best-practices/data-analysis",
                  "best-practices/research",
                  "best-practices/team-collaboration"
                ]
              }
            ]
          },
          {
            "tab": "Integrations",
            "groups": [
              {
                "group": "Platform Integrations",
                "pages": ["integrations/index", "integrations/github", "integrations/notion"]
              },
              {
                "group": "Advanced",
                "pages": ["integrations/vscode", "integrations/contact"]
              }
            ]
          },
          {
            "tab": "Use Cases",
            "groups": [
              {
                "group": "Use Cases",
                "pages": ["use-cases/index"]
              }
            ]
          }
        ]
      },
      {
        "language": "zh",
        "tabs": [
          {
            "tab": "快速入门",
            "groups": [
              {
                "group": "快速入门",
                "pages": ["zh/index", "zh/getting-started/quickstart", "zh/getting-started/faq"]
              }
            ]
          },
          {
            "tab": "功能指南",
            "groups": [
              {
                "group": "功能指南",
                "pages": ["zh/guides/skills", "zh/guides/multi-agent", "zh/guides/mcp", "zh/guides/automations"]
              }
            ]
          },
          {
            "tab": "最佳实践",
            "groups": [
              {
                "group": "概览",
                "pages": ["zh/best-practices/index", "zh/best-practices/general"]
              },
              {
                "group": "按角色",
                "pages": [
                  "zh/best-practices/developers",
                  "zh/best-practices/non-technical",
                  "zh/best-practices/product-design",
                  "zh/best-practices/marketing",
                  "zh/best-practices/data-analysis",
                  "zh/best-practices/research",
                  "zh/best-practices/team-collaboration"
                ]
              }
            ]
          },
          {
            "tab": "集成",
            "groups": [
              {
                "group": "平台集成",
                "pages": ["zh/integrations/index", "zh/integrations/github", "zh/integrations/notion"]
              },
              {
                "group": "高级",
                "pages": ["zh/integrations/vscode", "zh/integrations/contact"]
              }
            ]
          },
          {
            "tab": "用户案例",
            "groups": [
              {
                "group": "用户案例",
                "pages": ["zh/use-cases/index"]
              }
            ]
          }
        ]
      },
      {
        "language": "zh-Hant",
        "tabs": [
          {
            "tab": "快速入門",
            "groups": [
              {
                "group": "快速入門",
                "pages": ["zh-Hant/index", "zh-Hant/getting-started/quickstart", "zh-Hant/getting-started/faq"]
              }
            ]
          },
          {
            "tab": "功能指南",
            "groups": [
              {
                "group": "功能指南",
                "pages": ["zh-Hant/guides/skills", "zh-Hant/guides/multi-agent", "zh-Hant/guides/mcp", "zh-Hant/guides/automations"]
              }
            ]
          },
          {
            "tab": "最佳實踐",
            "groups": [
              {
                "group": "概覽",
                "pages": ["zh-Hant/best-practices/index", "zh-Hant/best-practices/general"]
              },
              {
                "group": "按角色",
                "pages": [
                  "zh-Hant/best-practices/developers",
                  "zh-Hant/best-practices/non-technical",
                  "zh-Hant/best-practices/product-design",
                  "zh-Hant/best-practices/marketing",
                  "zh-Hant/best-practices/data-analysis",
                  "zh-Hant/best-practices/research",
                  "zh-Hant/best-practices/team-collaboration"
                ]
              }
            ]
          },
          {
            "tab": "整合",
            "groups": [
              {
                "group": "平台整合",
                "pages": ["zh-Hant/integrations/index", "zh-Hant/integrations/github", "zh-Hant/integrations/notion"]
              },
              {
                "group": "進階",
                "pages": ["zh-Hant/integrations/vscode", "zh-Hant/integrations/contact"]
              }
            ]
          },
          {
            "tab": "使用案例",
            "groups": [
              {
                "group": "使用案例",
                "pages": ["zh-Hant/use-cases/index"]
              }
            ]
          }
        ]
      }
    ]
  },
  "navbar": {
    "primary": {
      "type": "button",
      "label": "Get Started",
      "href": "https://happycapy.ai"
    }
  },
  "footer": {
    "socials": {
      "x": "https://x.com/happycapy",
      "github": "https://github.com/Yv3s-y4ng"
    }
  }
}
```

**Step 2: Commit**

```bash
cd /home/node/a0/workspace/245eba45-b9f7-4f6d-901c-2f4064bbfd44/workspace/happycapy-docs
git add docs.json
git commit -m "feat: add i18n navigation for en/zh/zh-Hant with Use Cases tab"
```

---

### Task 2: Create Use Cases overview pages (3 languages)

**Files:**
- Create: `use-cases/index.mdx` (EN)
- Create: `zh/use-cases/index.mdx` (zh)
- Create: `zh-Hant/use-cases/index.mdx` (zh-Hant)

**Step 1: Create directories**

```bash
mkdir -p use-cases zh/use-cases zh-Hant/use-cases
```

**Step 2: Create EN use-cases/index.mdx**

Content: Overview of the User Stories section. Explains that this is a community showcase. Describes how users can submit their stories. Lists the scenario categories (Coding, Design, Content Creation, Data & Analysis, Other). Uses Mintlify CardGroup components for categories and a Note component for submission instructions.

**Step 3: Create zh/use-cases/index.mdx**

Same structure, content in Simplified Chinese.

**Step 4: Create zh-Hant/use-cases/index.mdx**

Same structure, content in Traditional Chinese.

**Step 5: Commit**

```bash
git add use-cases/ zh/use-cases/ zh-Hant/use-cases/
git commit -m "feat: add Use Cases overview pages in en/zh/zh-Hant"
```

---

### Task 3: Create zh/ translated pages (21 files, 4 parallel batches)

**Files:**
- Create all 21 files under `zh/`

**Source**: Notion HTML files (no suffix = Simplified Chinese)
**Reference**: Corresponding English MDX file for structure/components

Each subagent:
1. Reads the zh HTML source file
2. Reads the corresponding English MDX for component structure
3. Creates the zh MDX file matching the English structure but with Chinese content
4. Translates frontmatter title/description to Chinese
5. Keeps image paths identical (/images/...)
6. Keeps external URLs identical

**Batch A — Getting Started (3 files):**

| Target | zh HTML Source |
|--------|---------------|
| `zh/index.mdx` | `欢迎使用Happycapy 3096ea04998680118520f6984c65445d.html` |
| `zh/getting-started/quickstart.mdx` | `快速上手 3096ea0499868002bcddc67c919bd1d4.html` |
| `zh/getting-started/faq.mdx` | `常见问题 3096ea0499868067bff9e4ee0c97f315.html` |

**Batch B — Feature Guides (4 files):**

| Target | zh HTML Source |
|--------|---------------|
| `zh/guides/skills.mdx` | `Skills 指南 3096ea0499868071be29cad4ee14f954.html` |
| `zh/guides/multi-agent.mdx` | `Multi-Agent Team 指南 3096ea04998680248c82fbf994d3b1a2.html` |
| `zh/guides/mcp.mdx` | `MCP使用指南（多会话记忆管理，其他平台全局集成） 30f6ea0499868072a5a4d10ecfdeb723.html` |
| `zh/guides/automations.mdx` | `Automations （Beta）指南 3096ea049986806aa62afc6d8912db3f.html` |

**Batch C — Best Practices (9 files):**

| Target | zh HTML Source (under `HappyCapy 使用建议：真实团队的最佳实践/`) |
|--------|---------------|
| `zh/best-practices/index.mdx` | `HappyCapy 使用建议：真实团队的最佳实践 3126ea04998680ddb840dfae4e413585.html` |
| `zh/best-practices/general.mdx` | `通用最佳实践 3126ea04998681299e9bc077058a06ad.html` |
| `zh/best-practices/developers.mdx` | `开发者如何高效使用 HappyCapy 3126ea04998681cbb396dc0c52183fd4.html` |
| `zh/best-practices/non-technical.mdx` | `非技术人员如何使用 HappyCapy 3126ea04998681d1a08de5b1761523b8.html` |
| `zh/best-practices/product-design.mdx` | `产品设计与原型制作 3126ea04998681179769cd8d49281e70.html` |
| `zh/best-practices/marketing.mdx` | `营销与内容创作 3126ea04998681e88974ffb9c760a324.html` |
| `zh/best-practices/data-analysis.mdx` | `数据分析与可视化 3126ea04998681af86bdef3b6641f2ef.html` |
| `zh/best-practices/research.mdx` | `研究与学习 3126ea049986815b963be80819503258.html` |
| `zh/best-practices/team-collaboration.mdx` | `团队协作与文档管理 3126ea04998681f9a765e394e6e6b04a.html` |

**Batch D — Integrations (5 files):**

| Target | zh HTML Source |
|--------|---------------|
| `zh/integrations/index.mdx` | `与其他平台的集成 3096ea04998680d3b4d2f992b732da62.html` |
| `zh/integrations/github.mdx` | `与其他平台的集成/GitHub 集成 3096ea04998681d095fece36eafa5146.html` |
| `zh/integrations/notion.mdx` | `与其他平台的集成/Notion 集成 3096ea04998681c09d2efbf805bac461.html` |
| `zh/integrations/vscode.mdx` | `使用本地 IDE(以VS Code为例) 连接 HappyCapy沙箱 3146ea04998680a59c01f25071564452.html` |
| `zh/integrations/contact.mdx` | `联系我们 3096ea04998680e88619c30a159342f9.html` |

**Step: Commit after all zh/ files created**

```bash
git add zh/
git commit -m "feat: add Simplified Chinese (zh) documentation — 21 pages"
```

---

### Task 4: Create zh-Hant/ translated pages (21 files, 4 parallel batches)

**Files:**
- Create all 21 files under `zh-Hant/`

**Source**: Notion HTML files (_tw suffix = Traditional Chinese)
**Reference**: Corresponding English MDX file for structure/components

Same batch structure as Task 3 but using `_tw.html` source files. Same rules apply.

**Verify**: No Simplified Chinese characters leak into zh-Hant files.

**Step: Commit after all zh-Hant/ files created**

```bash
git add zh-Hant/
git commit -m "feat: add Traditional Chinese (zh-Hant) documentation — 21 pages"
```

---

### Task 5: Push and verify deployment

**Step 1: Push**

```bash
git push
```

**Step 2: Verify at https://happycapy.mintlify.app/**

Check:
- Language switcher visible in header
- EN loads by default with all 5 tabs
- zh shows Chinese content with Chinese nav labels
- zh-Hant shows Traditional Chinese with Traditional Chinese nav labels
- Use Cases tab shows overview page in all 3 languages
- Images load across all languages
- Internal links work

---

## Parallelization Strategy

- Task 1 must go first (docs.json)
- Task 2 can go after Task 1
- Tasks 3 and 4 are independent and can run in parallel
- Within Task 3: Batches A/B/C/D can run as 4 parallel subagents
- Within Task 4: Batches A/B/C/D can run as 4 parallel subagents
- Maximum parallelism: 8 subagents (4 batches x 2 languages)
- Task 5 goes last after all files are committed
