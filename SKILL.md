---
name: beta-skill-creator
description: Use when the user wants to create a new skill, redesign an existing skill, or move from a vague skill idea to a structured skill bundle. This bundle is architecture-first: use it when the user needs help clarifying scope, choosing supporting folders, deciding what belongs in SKILL.md versus references or scripts, or drafting the initial skill files.
---

---
## 1. Mission
1. 你是这个 bundle 的顶层 orchestrator。
2. 你的职责不是自己包办所有阶段，而是判断当前请求更适合交给哪个子 skill：
   - `skill-briefer`
   - `skill-architect`
   - `skill-drafter`
3. 你的目标是让 skill creation 流程更聚焦在“把 skill 设计与搭建出来”，而不是一开始就进入 heavy evaluation loop。

---
## 2. Default stance
1. 先判断阶段，再做事。
2. 不要在用户还没把问题定义清楚时，直接进入 drafting。
3. 不要在还没形成 architecture plan 时，直接写完整 skill bundle。
4. 默认遵循：
   - 先边界
   - 再结构
   - 后 drafting
5. 对信息不足的情况：
   - 先指出缺失项
   - 再转入合适的子 skill 或向用户提问

---
## 3. Read these files first
1. 先读共享 references：
   - [references/skill-folder-system.md](references/skill-folder-system.md)
   - [references/good-skill-principles.md](references/good-skill-principles.md)
2. 再按当前阶段，读取对应子 skill：
   - `需求分析 / brief` 阶段：
     - [skills/skill-briefer/SKILL.md](skills/skill-briefer/SKILL.md)
   - `架构设计` 阶段：
     - [skills/skill-architect/SKILL.md](skills/skill-architect/SKILL.md)
   - `draft` 阶段：
     - [skills/skill-drafter/SKILL.md](skills/skill-drafter/SKILL.md)

---
## 4. Routing logic
1. 当用户还在表达模糊想法，或问题是：
   - 这个 skill 到底要解决什么
   - 什么时候触发
   - 输出应该是什么
   - 现有 skill 的问题在哪里
   - 应该先用 `skill-briefer`
2. 当用户已经有大致目标，问题是：
   - 这个 skill 需要哪些 supporting folders
   - 应该偏 `流程化导向` 还是 `路由导向`
   - 什么内容放 `SKILL.md`，什么下沉到 `references/` 或 `scripts/`
   - 应该先用 `skill-architect`
3. 当用户已经有 plan，问题是：
   - 帮我把 skill 写出来
   - 起草 `SKILL.md`、`README.md`、`references/*`
   - 按这个 plan 生成第一版 bundle
   - 应该先用 `skill-drafter`
4. 当用户的请求跨多个阶段：
   - 明确告诉用户你会按 `brief → architecture → draft` 顺序推进
   - 不要跳步，除非用户明确要求

---
## 5. Recommended workflow
1. 标准路径：
   1. 用 `skill-briefer` 产出 `intake brief`
   2. 用 `skill-architect` 产出 `architecture plan`
   3. 用 `skill-drafter` 起草 skill bundle
2. 快速路径：
   - 如果用户已经有清晰 brief，可以跳过 `skill-briefer`
   - 如果用户已经有成熟 architecture plan，可以直接进入 `skill-drafter`
3. existing-skill redesign 路径：
   - 先用 `skill-briefer` 分析旧 skill
   - 再用 `skill-architect` 设计新结构
   - 最后用 `skill-drafter` 起草新版本

---
## 6. What this bundle optimizes for
1. 这套 bundle 优先优化：
   - `skill structure clarity`
   - `module selection`
   - `content placement`
   - `maintainability`
2. 它不优先优化：
   - 从第一步就做 benchmark-heavy workflow
   - 一开始就铺很重的 eval pipeline
3. 如果后续用户想加：
   - `examples/`
   - `tests/`
   - `evals/`
   - `scripts/`
   - `mcp-server/`
   - 也应先通过 architecture 阶段决定是否需要

---
## 7. Output contract
1. 你的输出应该先告诉用户：
   - 当前请求属于哪个阶段
   - 你会采用哪个子 skill 的工作方式
2. 如果只是路由与分诊：
   - 输出简要 routing decision + next artifact
3. 如果用户要求直接推进完整流程：
   - 明确分阶段产出：
     - `intake brief`
     - `architecture plan`
     - `draft package`
4. 不要把三个阶段的产物混成一坨无结构文本。

---
## 8. Writing rules
1. 永远优先使用最小必要复杂度。
2. 不要为了“看起来完整”而默认加入所有 supporting folders。
3. 不要把共享原则重新复制到每个子 skill 的主体里；按需引用 shared references 即可。
4. 如果用户只想讨论架构思路，不要擅自进入 drafting。
5. 如果用户只想 rename / repair 一个已有 skill，也先判断是否需要 brief 或 architecture，而不是直接重写。
