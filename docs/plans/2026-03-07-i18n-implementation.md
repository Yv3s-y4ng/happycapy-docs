# i18n Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add Simplified Chinese (zh) and Traditional Chinese (zh-Hant) translations to the HappyCapy Mintlify documentation site.

**Architecture:** Mintlify's `navigation.languages` array wraps our existing `tabs` structure. English files stay at root (zero disruption). Chinese and Traditional Chinese files go in `zh/` and `zh-Hant/` folders, mirroring the English directory structure. Content is translated from Notion-exported HTML source files.

**Tech Stack:** Mintlify docs.json i18n, MDX components (Card, CardGroup, Accordion, Steps, Tip, Note, Warning, Columns)

---

## Source File Mapping

Base path: `/home/node/a0/workspace/245eba45-b9f7-4f6d-901c-2f4064bbfd44/workspace/happycapy 多语言/extracted/howtobestusai1-bilingual-docs-main/HappyCapy/`

| Target MDX | zh HTML source (no suffix) | zh-Hant HTML source (_tw suffix) |
|---|---|---|
| `index.mdx` | `欢迎使用Happycapy 3096ea04998680118520f6984c65445d.html` | `...65445d_tw.html` |
| `getting-started/quickstart.mdx` | `快速上手 3096ea0499868002bcddc67c919bd1d4.html` | `...91bd1d4_tw.html` |
| `getting-started/faq.mdx` | `常见问题 3096ea0499868067bff9e4ee0c97f315.html` | `...97f315_tw.html` |
| `guides/skills.mdx` | `Skills 指南 3096ea0499868071be29cad4ee14f954.html` | `...14f954_tw.html` |
| `guides/multi-agent.mdx` | `Multi-Agent Team 指南 3096ea04998680248c82fbf994d3b1a2.html` | `...d3b1a2_tw.html` |
| `guides/mcp.mdx` | `MCP使用指南（多会话记忆管理，其他平台全局集成） 30f6ea0499868072a5a4d10ecfdeb723.html` | `...deb723_tw.html` |
| `guides/automations.mdx` | `Automations （Beta）指南 3096ea049986806aa62afc6d8912db3f.html` | `...12db3f_tw.html` |
| `best-practices/index.mdx` | `HappyCapy 使用建议：真实团队的最佳实践 3126ea04998680ddb840dfae4e413585.html` | `...413585_tw.html` |
| `best-practices/general.mdx` | `HappyCapy 使用建议.../通用最佳实践 3126ea04998681299e9bc077058a06ad.html` | `...8a06ad_tw.html` |
| `best-practices/developers.mdx` | `HappyCapy 使用建议.../开发者如何高效使用 HappyCapy 3126ea04998681cbb396dc0c52183fd4.html` | `...183fd4_tw.html` |
| `best-practices/non-technical.mdx` | `HappyCapy 使用建议.../非技术人员如何使用 HappyCapy 3126ea04998681d1a08de5b1761523b8.html` | `...1523b8_tw.html` |
| `best-practices/product-design.mdx` | `HappyCapy 使用建议.../产品设计与原型制作 3126ea04998681179769cd8d49281e70.html` | `...281e70_tw.html` |
| `best-practices/marketing.mdx` | `HappyCapy 使用建议.../营销与内容创作 3126ea04998681e88974ffb9c760a324.html` | `...c760a324_tw.html` |
| `best-practices/data-analysis.mdx` | `HappyCapy 使用建议.../数据分析与可视化 3126ea04998681af86bdef3b6641f2ef.html` | `...6641f2ef_tw.html` |
| `best-practices/research.mdx` | `HappyCapy 使用建议.../研究与学习 3126ea049986815b963be80819503258.html` | `...19503258_tw.html` |
| `best-practices/team-collaboration.mdx` | `HappyCapy 使用建议.../团队协作与文档管理 3126ea04998681f9a765e394e6e6b04a.html` | `...e6e6b04a_tw.html` |
| `integrations/index.mdx` | `与其他平台的集成 3096ea04998680d3b4d2f992b732da62.html` | `...b732da62_tw.html` |
| `integrations/github.mdx` | `与其他平台的集成/GitHub 集成 3096ea04998681d095fece36eafa5146.html` | `...eafa5146_tw.html` |
| `integrations/notion.mdx` | `与其他平台的集成/Notion 集成 3096ea04998681c09d2efbf805bac461.html` | `...05bac461_tw.html` |
| `integrations/vscode.mdx` | `使用本地 IDE(以VS Code为例) 连接 HappyCapy沙箱 3146ea04998680a59c01f25071564452.html` | `...71564452_tw.html` |
| `integrations/contact.mdx` | `联系我们 3096ea04998680e88619c30a159342f9.html` | `...159342f9_tw.html` |

---

## Task 1: Update docs.json with i18n navigation

**Files:**
- Modify: `happycapy-docs/docs.json`

**Step 1: Rewrite navigation section**

Replace the current `navigation.tabs` with `navigation.languages` containing 3 language entries, each with their own `tabs` inside. Keep all other config (theme, colors, background, logo, navbar, footer) unchanged.

English (en): Keep exact same tab/group/page structure, no path prefix.
Chinese (zh): Mirror structure with `zh/` prefix on all page paths, Chinese nav labels.
Traditional Chinese (zh-Hant): Mirror structure with `zh-Hant/` prefix, Traditional Chinese nav labels.

See design doc `docs/plans/2026-03-07-i18n-design.md` for exact nav label translations.

**Step 2: Commit**

```bash
git add docs.json
git commit -m "feat: add i18n navigation for zh and zh-Hant"
```

---

## Task 2: Create zh/ directory structure

**Step 1: Create directories**

```bash
mkdir -p happycapy-docs/zh/getting-started
mkdir -p happycapy-docs/zh/guides
mkdir -p happycapy-docs/zh/best-practices
mkdir -p happycapy-docs/zh/integrations
```

---

## Task 3: Create all 21 zh/ MDX files (parallel subagents)

For each file: Read the corresponding zh HTML source, read the English MDX file for structure reference, convert the Chinese HTML content into MDX format matching the English file's Mintlify component structure (Card, CardGroup, Accordion, Steps, etc.).

**Important rules:**
- Keep the same frontmatter structure but translate title/description to Chinese
- Use the same Mintlify components as the English version
- Keep all image paths identical (shared /images/ directory)
- Keep all external URLs identical
- Translate ALL content including code block comments and prompt examples

Split into 4 parallel batches by tab:

### Batch A: Getting Started (3 files)
- `zh/index.mdx` ← from `欢迎使用Happycapy...html`
- `zh/getting-started/quickstart.mdx` ← from `快速上手...html`
- `zh/getting-started/faq.mdx` ← from `常见问题...html`

### Batch B: Feature Guides (4 files)
- `zh/guides/skills.mdx` ← from `Skills 指南...html`
- `zh/guides/multi-agent.mdx` ← from `Multi-Agent Team 指南...html`
- `zh/guides/mcp.mdx` ← from `MCP使用指南...html`
- `zh/guides/automations.mdx` ← from `Automations（Beta）指南...html`

### Batch C: Best Practices (9 files)
- `zh/best-practices/index.mdx` ← from `HappyCapy 使用建议...html`
- `zh/best-practices/general.mdx` ← from `通用最佳实践...html`
- `zh/best-practices/developers.mdx` ← from `开发者如何高效使用...html`
- `zh/best-practices/non-technical.mdx` ← from `非技术人员如何使用...html`
- `zh/best-practices/product-design.mdx` ← from `产品设计与原型制作...html`
- `zh/best-practices/marketing.mdx` ← from `营销与内容创作...html`
- `zh/best-practices/data-analysis.mdx` ← from `数据分析与可视化...html`
- `zh/best-practices/research.mdx` ← from `研究与学习...html`
- `zh/best-practices/team-collaboration.mdx` ← from `团队协作与文档管理...html`

### Batch D: Integrations (5 files)
- `zh/integrations/index.mdx` ← from `与其他平台的集成...html`
- `zh/integrations/github.mdx` ← from `与其他平台的集成/GitHub 集成...html`
- `zh/integrations/notion.mdx` ← from `与其他平台的集成/Notion 集成...html`
- `zh/integrations/vscode.mdx` ← from `使用本地 IDE...html`
- `zh/integrations/contact.mdx` ← from `联系我们...html`

**Step: Commit after all zh/ files created**

```bash
git add zh/
git commit -m "feat: add Simplified Chinese (zh) documentation"
```

---

## Task 4: Create zh-Hant/ directory structure

**Step 1: Create directories**

```bash
mkdir -p happycapy-docs/zh-Hant/getting-started
mkdir -p happycapy-docs/zh-Hant/guides
mkdir -p happycapy-docs/zh-Hant/best-practices
mkdir -p happycapy-docs/zh-Hant/integrations
```

---

## Task 5: Create all 21 zh-Hant/ MDX files (parallel subagents)

Same approach as Task 3 but using `_tw.html` source files. Same 4 parallel batches.

**Important:** zh-Hant content uses Traditional Chinese characters. Verify no Simplified Chinese leaks into zh-Hant files.

**Step: Commit after all zh-Hant/ files created**

```bash
git add zh-Hant/
git commit -m "feat: add Traditional Chinese (zh-Hant) documentation"
```

---

## Task 6: Push and verify deployment

**Step 1: Push all commits**

```bash
git push
```

**Step 2: Verify deployment**

Check https://happycapy.mintlify.app/ for:
- Language switcher appears in header
- English content loads by default
- Switching to zh shows Simplified Chinese with Chinese nav labels
- Switching to zh-Hant shows Traditional Chinese
- All images load correctly across all languages
- All internal links work

---

## Execution Notes

- Tasks 3 and 5 are the bulk of the work (42 MDX files total)
- Each can be parallelized with 4 subagents (one per batch)
- Tasks 3 and 5 can also run in parallel with each other (zh and zh-Hant simultaneously)
- Maximum parallelism: 8 subagents (4 batches x 2 languages)
- Each subagent reads HTML source + English MDX reference, writes translated MDX
