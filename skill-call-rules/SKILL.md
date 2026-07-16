---
name: skill-call-rules
description: Skill 调用决策规则 — 双轨制：开发任务由 using-superpowers 激进调度，非开发任务保守匹配。防止误匹配和无效调用。
---

# ⚙️ Skill 调用决策规则

> **双轨制：开发任务走 Superpowers 调度（1%可能就查），非开发任务走保守匹配（不确定不调）。两套规则互补，不冲突。**

---

## 🎯 双轨制总览

| | 🛠️ 开发轨道 | 💬 通用轨道 |
|---|---|---|
| **调度者** | using-superpowers | 本规则（skill-call-rules） |
| **适用场景** | 写代码、调试、审查、部署、重构 | 闲聊、文档、元任务、非代码操作 |
| **调用门槛** | 1% 可能就查 skill | 精确匹配才调 |
| **核心原则** | IF A SKILL APPLIES, YOU MUST USE IT | 不确定时走不调用方向 |

---

## 🛠️ 开发轨道（using-superpowers 调度）

当任务涉及以下任一类别时，由 using-superpowers 接管调度：

- 写/改代码、修 bug、加功能
- 调试、测试、代码审查
- 部署、Git 操作
- 需求分析、技术方案设计

**Superpowers 技能链（调用优先级从高到低）：**

1. `brainstorming` → 需求不明确时先追问，不跳步
2. `writing-plans` → 复杂任务先写计划
3. `test-driven-development` → 写代码前先写测试
4. `subagent-driven-development` → 可并行任务分派子代理
5. `systematic-debugging` → 调试时系统化排查，不乱猜
6. `verification-before-completion` → 完工前验证
7. `requesting-code-review` / `receiving-code-review` → 提交前审查
8. `using-git-worktrees` / `finishing-a-development-branch` → 分支管理

**这些 skill 之间不冲突** — using-superpowers 按流程阶段自动选择，不会同时调多个同阶段 skill。

---

## 💬 通用轨道（本规则调度）

以下场景**不走** Superpowers，用保守策略：

1. **简单闲聊** — "今天天气怎么样" → 直接回答
2. **纯元任务** — 写记忆文件、写 Obsidian 笔记 → 直接处理
3. **常识性问题** — "git clone 命令是什么" → 直接回答
4. **非开发类 skill** — frontend-design、brand-guidelines 等 UI skill，按精确匹配原则调用

**判断标准：**
```
收到任务
  ↓
是不是开发任务？（写代码/调试/审查/部署）
  ↓ 是                    ↓ 否
using-superpowers 接管    扫描 skills 列表
                          ↓
                    有精确匹配？→ 调
                          ↓ 否
                    不确定时走"不调用"方向
```

---

## ⚠️ 常见误用陷阱

| 场景 | 错误做法 | 正确做法 |
|------|----------|----------|
| 开发任务 | 凭经验手动查、跳过 skill | using-superpowers 调度，1%可能就查 |
| 非开发任务 | 强行找 skill 套上去 | 精确匹配才调，不确定不调 |
| 用户问简单问题 | 调用 skill "以防万一" | 直接回答 |
| 任务标题沾边但描述不符 | 强行调用 | 不调用，直接处理 |

---

> 📝 创建时间：2026-07-14
> 🔄 更新时间：2026-07-16 — 整合 using-superpowers 双轨制
