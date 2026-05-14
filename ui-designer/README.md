# ui-designer

> OpenClaw Skill — AI 驱动的 UI 设计与集成工作流

## 简介

`ui-designer` 是一个为 OpenClaw 设计的 Skill，能够根据你的需求和项目代码，自动生成结构化的 UI 设计方案，并将最终 UI 代码无缝融合到现有项目中。

整个流程完全由 AI 驱动，你只需用自然语言描述需求，其余交给 AI 完成。

---

## 安装

### 方法一：使用 OpenClaw CLI 一键安装（推荐）

```bash
openclaw skills install https://github.com/Team-Nexus-AI/openclaw-skills/tree/main/ui-designer
```

### 方法二：手动安装

1. 克隆或下载本仓库：

```bash
git clone https://github.com/Team-Nexus-AI/openclaw-skills.git
```

2. 将 `ui-designer` 目录复制到 OpenClaw 的 skills 目录：

```bash
cp -r openclaw-skills/ui-designer ~/.openclaw/projects/.openclaw/skills/
# 或者（取决于你的 OpenClaw 安装路径）
cp -r openclaw-skills/ui-designer /projects/.openclaw/skills/
```

3. 重启 OpenClaw 或重新开始对话，skill 即生效。

### 验证安装

在 OpenClaw 对话中输入：

```
帮我设计UI
```

如果 AI 开始询问 UI 需求，说明安装成功 ✅

---

## 工作流

```
Step 1  收集 UI 需求（风格、页面、平台、功能）
   ↓
Step 2  阅读项目代码（技术栈、组件库、路由结构）
   ↓
Step 3  合成结构化设计规格，与用户确认
   ↓
Step 4  输出高质量 Google Stitch Prompt + 操作指引
        → 用户在 Stitch 上自由预览和调整
        → 满意后下载代码
   ↓
Step 5  将 UI 代码融合到项目中（React / Vue / 原生 HTML 等）
```

---

## 触发方式

在 OpenClaw 对话中说以下任意一句话即可触发：

- `帮我设计UI`
- `给这个项目做个界面`
- `生成UI`
- `UI设计`
- `页面设计`

---

## 功能特点

- **零门槛上手**：无需懂 Figma 或 CSS，用自然语言描述即可
- **技术栈感知**：自动分析项目代码，确保生成的 UI 与现有技术栈兼容
- **人在回路**：UI 效果由用户在 Google Stitch 上亲自预览和调整，满意后再融合
- **多框架支持**：React / Next.js、Vue 3 / Nuxt、原生 HTML，以及 Tailwind、Ant Design、MUI 等组件库
- **渐进式集成**：融合时保留已有设计 token，不破坏现有页面

---

## 依赖

- **OpenClaw** — Skill 运行环境
- **Google Stitch** — UI 生成工具（免费，需 Google 账号）
  - 访问地址：https://stitch.withgoogle.com
  - 每月免费配额：标准模式 350 次

---

## 文件结构

```
ui-designer/
├── README.md                         # 本文档
├── SKILL.md                          # 主流程与工作流定义
└── references/
    ├── stitch-prompt-guide.md        # Google Stitch 高质量 Prompt 构建指南
    └── integration-guide.md          # 各技术栈 UI 代码融合方案
```

---

## 参考资料

- [Google Stitch 官网](https://stitch.withgoogle.com)
- [OpenClaw 文档](https://docs.openclaw.ai)

---

## 注意事项

- Stitch 生成的是**静态 UI 壳**，不含业务逻辑（无数据库、无用户认证）
- 复杂 B 端页面（多层级数据表格）生成质量一般，建议拆分为多个简单页面分别生成
- 多页面项目需在 Prompt 中明确指定设计系统（颜色、字体、圆角），保持跨页面一致性
