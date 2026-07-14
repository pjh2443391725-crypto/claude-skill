# 前端 / 产品 / UI 方向 Agent Skills 推荐清单

> 面向 Claude Code / Codex 等 AI 编码代理，覆盖设计落地、UI 质量、交互验证三大维度。

## 技能总览

| # | 技能名 | 来源 | 🔒 安全 | ⭐ 实用 | 核心用途 | 依赖 |
|---|--------|------|---------|---------|----------|------|
| 1 | **frontend-design** | Anthropic 官方 | ✅ 官方 | ⭐⭐⭐⭐⭐ | 高完成度、强风格的前端界面，拒绝 AI 审美 | 无 |
| 2 | **figma-implement-design** | OpenAI 官方 | ✅ 官方 | ⭐⭐⭐⭐⭐ | Figma 设计稿 → 生产级代码，像素级还原 | Figma MCP |
| 3 | **web-design-guidelines** | Vercel 官方 | ✅ 官方 | ⭐⭐⭐⭐⭐ | UI 审查：可访问性/表单/动效/排版/暗黑模式 100+ 规则 | 无 |
| 4 | **react-best-practices** | Vercel 官方 | ✅ 官方 | ⭐⭐⭐⭐⭐ | React/Next.js 性能优化，40+ 规则（瀑布请求/打包/重渲染） | 无 |
| 5 | **playwright** | OpenAI 官方 | ✅ 官方 | ⭐⭐⭐⭐ | 浏览器自动化：导航/填表/截图/数据提取/UI 流程调试 | Playwright |
| 6 | **webapp-testing** | Anthropic 官方 | ✅ 官方 | ⭐⭐⭐⭐ | 本地 Web 应用验证：页面行为/截图/日志/交互回归 | Playwright |
| 7 | **frontend-slides** | 社区（zarazhangrui） | ⚠️ 社区 | ⭐⭐⭐ | HTML 演示文稿/PPT 生成，24K+ star，零依赖单文件输出 | 无 |
| 8 | **canvas-design** | Anthropic 官方 | ✅ 官方 | ⭐⭐⭐ | 创意视觉设计：海报/封面/信息图，PDF/PNG 画布输出 | 字体文件 |
| 9 | **brand-guidelines** | Anthropic 官方 | ✅ 官方 | ⭐⭐⭐ | 品牌色/字体规范应用到所有产物，可定制为自有品牌模板 | 无 |

## 详情与安装

### 1. frontend-design
- **仓库**: [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design)
- **擅长**: 字体选择、配色体系、动效、空间构图、背景纹理 —— 避免千篇一律的「AI 风格」
- **安装**: `npx skills add anthropics/skills --skill frontend-design`

### 2. figma-implement-design
- **仓库**: [openai/skills](https://github.com/openai/skills/tree/main/skills/.curated/figma-implement-design)
- **擅长**: 7 步工作流（获取节点 → 设计上下文 → 截图对照 → 下载资源 → 设计 Token 映射 → 像素对齐 → 验证）
- **安装**: `npx skills add https://github.com/openai/skills --skill figma-implement-design`
- ⚠️ 需要配置 Figma MCP Server

### 3. web-design-guidelines
- **仓库**: [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines)
- **擅长**: 11 个维度的 UI 审查（可访问性 / 焦点状态 / 表单 / 动效 / 排版 / 图片 / 性能 / 导航 / 暗黑模式 / 触控 / 国际化）
- **安装**: `npx add-skill vercel-labs/agent-skills`

### 4. react-best-practices
- **仓库**: [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills/tree/main/skills/react-best-practices)
- **擅长**: 消除请求瀑布流 / 打包体积 / 服务端性能 / 客户端数据获取 / 重渲染优化
- **安装**: `npx add-skill vercel-labs/agent-skills`

### 5. playwright
- **仓库**: [openai/skills](https://github.com/openai/skills/tree/main/skills/.curated/playwright)
- **擅长**: 通过 `playwright-cli` 在真实浏览器中导航、交互、截图、提取数据
- **安装**: `npx skills add https://github.com/openai/skills --skill playwright`

### 6. webapp-testing
- **仓库**: [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/webapp-testing)
- **擅长**: 「侦察-行动」模式：等待 networkidle → 截图/检查 DOM → 通过发现的选择器交互
- **安装**: `npx skills add anthropics/skills --skill webapp-testing`

### 7. frontend-slides
- **仓库**: [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides)
- **擅长**: 文字描述 → 3 种视觉风格预览 → 完整 HTML 演示文稿；支持 .pptx 导入
- **安装**: `git clone https://github.com/zarazhangrui/frontend-slides.git ~/.claude/skills/frontend-slides`
- ⚠️ 社区维护项目，非 OpenAI 官方

### 8. canvas-design
- **仓库**: [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/canvas-design)
- **擅长**: 先输出设计哲学文档，再在画布上实现；内置 50+ 专业字体（OFL/CC 许可）
- **安装**: `npx skills add anthropics/skills --skill canvas-design`

### 9. brand-guidelines
- **仓库**: [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/brand-guidelines)
- **擅长**: 默认内置 Anthropic 品牌规范，可替换为自有品牌色板/字体体系
- **安装**: `npx skills add anthropics/skills --skill brand-guidelines`

---

## 怎么选？

| 你的场景 | 优先装 |
|----------|--------|
| 🎨 品牌官网 / 营销页 | frontend-design · brand-guidelines · frontend-slides |
| 🖼️ Figma 设计稿 → 代码 | figma-implement-design · react-best-practices · web-design-guidelines |
| 🧪 UI 交互验证 / 回归测试 | playwright · webapp-testing |
| ✨ 创意视觉 / 海报 / 封面 | canvas-design · frontend-design |

---

## ⚠️ 安全备注

- 所有标注「✅ 官方」的技能均来自 **Anthropic / OpenAI / Vercel** 官方 GitHub 组织，经过审核，可放心安装
- **frontend-slides** 是社区项目（zarazhangrui），虽热门（24K+ star）但非官方，安装前建议自行审查 `SKILL.md` 内容
- 技能本身为声明式 Markdown 指令文件，不包含可执行代码，风险主要在于：指令是否会让代理执行危险操作（如 `rm -rf`、泄露文件等），安装前可快速浏览 SKILL.md
