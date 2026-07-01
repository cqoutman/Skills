# Skills

Reusable Codex skills maintained by cqoutman.

可复用的 Codex Skills 集合，用于沉淀可迁移、可复用的智能体工作流。

## figma-ui-export

**figma-ui-export: 补上 AI 出图后“无法交付”的最后一公里**

如今 AI 已经能快速生成 UI 设计稿，但问题也随之而来：AI 产出的往往是一张完整位图，没有矢量图层、没有可编辑文字、没有可切片的资源结构。设计师过去用 Sketch、Figma、Photoshop 一笔一画手搓出的稿子，天然带分层、可编辑、可切片，开发拿到手就能用；而 AI 生成的图看似精致，下游却动不了：文字改不了、图标切不出、模块调不动，真正进入交付环节时反而卡壳。

`figma-ui-export` 正是为补上这一环而生。它运行于 Codex 智能体之上，解决的是“AI 能出图，但生成的图无法像手搓稿那样切片、还原、交付”的核心难题。借助 Codex 的多模态识图、坐标推理、代码生成与自验证能力，一条指令即可把一张 AI 生成的整图，反向重建为结构化、可编辑、可切片的设计资产，让 AI 设计真正具备工程可交付性。

它内置三条工作模式，覆盖从还原到交付的完整链路：

- `screenshot-to-figma`: 将 AI 生成的图还原为带可编辑文字、矢量图标与原子资产的 Figma 文件。导航、卡片、表单、文案等保持可编辑，主视觉与富媒体则保留为高质量原子资产。
- `figma-export-html`: 由设计源帧导出独立的 HTML/CSS/资源，直接对接前端开发。
- `figma-export-file`: 生成真实 `.fig` 文件，可导入蓝湖 / Lanhu / Blue Lake 等交付工具。

最终交付质量同样由 Codex 自动把关：它对照原稿核验布局、间距、字体、颜色、圆角、阴影等关键维度，并清理残留的旧路径与外部依赖，确保输出具备可交付性。原本需要设计师照着 AI 图在 Figma 里逐层重画、一一拆图命名、反复对照验收的小时级工作，被压缩为分钟级的自动交付。

应用上它不绑定具体行业或产品，从 App 页面、SaaS dashboard、落地页、活动页到老系统界面迁移都能覆盖。它的真正价值，是把 AI 生成设计与工程交付之间断裂的那一环重新接上：让 AI 出图不再是终点，而是一个可切片、可还原、可二次编辑的交付起点。

### English

**figma-ui-export: the last mile that makes AI-generated UI deliverable**

AI can now generate polished UI mockups quickly, but a new delivery gap appears immediately: the output is often a single bitmap, without vector layers, editable text, or a sliceable asset structure. Traditional Sketch, Figma, or Photoshop files are naturally layered, editable, and ready for handoff. AI-generated images may look refined, yet downstream teams cannot change the text, extract icons, adjust modules, or reliably prepare assets for implementation.

`figma-ui-export` exists to close that gap. Built for Codex agents, it addresses the core problem that AI can create an image, but that image cannot be handed off like a manually crafted design file. With Codex's multimodal vision, coordinate reasoning, code generation, and self-verification, a single instruction can reverse-rebuild an AI-generated full-page image into structured, editable, and sliceable design assets.

The skill includes three workflow modes:

- `screenshot-to-figma`: Recreates an AI-generated screenshot as an editable Figma file with editable text, vector icons, and atomic assets. Navigation, cards, forms, and copy remain editable, while complex hero visuals and rich media are preserved as high-quality atomic assets.
- `figma-export-html`: Exports a source Figma frame into standalone HTML, CSS, and assets for frontend implementation.
- `figma-export-file`: Produces a real `.fig` file for import into handoff tools such as Lanhu / Blue Lake.

Codex also verifies delivery quality by comparing layout, spacing, typography, colors, radii, shadows, and other key visual details against the source, while cleaning stale paths and external dependencies. Work that previously required designers to manually redraw layers, slice assets, name files, and repeat visual QA can be compressed from hours into minutes.

The skill is product- and industry-agnostic. It can support app screens, SaaS dashboards, landing pages, campaign pages, and legacy interface migration. Its real value is reconnecting the broken link between AI-generated visuals and engineering delivery: AI output becomes not the endpoint, but a sliceable, restorable, and editable starting point.

## Repository Layout

```text
figma-ui-export/
  SKILL.md
  agents/
    openai.yaml
```
