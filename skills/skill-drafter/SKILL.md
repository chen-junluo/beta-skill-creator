---
name: skill-drafter
description: Use when the user already has a skill architecture plan and wants to draft the actual skill files, including SKILL.md, README.md, and any initial supporting references or quality-control files. Trigger when the user wants to turn a plan into a first working skill bundle.
---

---
## 1. Mission
1. 你的任务是根据 plan 起草 skill bundle。
2. 你的目标不是重新发明架构，而是把 plan 变成第一版文件。
3. 你应该优先起草：
   - `SKILL.md`
   - `README.md`
   - 必要的 `references/*`
4. 如果 plan 明确要求，也可以继续起草：
   - `examples/`
   - `tests/`
   - `evals/`
   - `config/`
   - `agents/`
5. 如果 plan 提到 `scripts/` 或 `mcp-server/`，你可以为它们写 skeleton / placeholder spec；但当关键执行细节不明确时，要先问用户。

---
## 2. Default stance
1. 先忠实执行 plan，再做小范围补全。
2. 不要擅自升级 scope。
3. 对关键不确定项：
   - 不要硬编
   - 先问用户
4. 默认产出 `minimum viable draft`：
   - 让 skill 可读、可维护、可继续迭代
   - 而不是一次写成最终完美版

---
## 3. Read these references when needed
1. 读 [../../references/skill-folder-system.md](../../references/skill-folder-system.md)
   - 用于校验 folder placement 是否合理
2. 读 [../../references/good-skill-principles.md](../../references/good-skill-principles.md)
   - 用于校验 draft 是否遵循：
     - 先边界后能力
     - deterministic workflow
     - output contract
     - knowledge 下沉

---
## 4. Workflow
1. `read the plan`
   - 提炼：
     - 目标
     - trigger
     - output contract
     - required modules
     - optional modules
2. `identify drafting scope`
   - 明确本轮需要起草哪些文件
   - 不要默认把所有可选模块都写出来
3. `check for blockers`
   - 如果缺：
     - skill name
     - trigger definition
     - output format
     - source hierarchy
     - missing-input policy
   - 先问用户，不要跳过
4. `draft core files`
   - 先写：
     - `SKILL.md`
     - `README.md`
   - 再写必要 supporting references
5. `draft supporting files`
   - 仅在 plan 需要时补：
     - `examples/`
     - `tests/`
     - `evals/`
     - `config/`
     - `agents/`
     - `scripts/` / `mcp-server/` skeleton
6. `run internal QA`
   - 检查：
     - `SKILL.md` 是否太臃肿
     - 复杂知识是否已下沉到 `references/`
     - output contract 是否明确
     - workflow 是否可执行
7. `return draft package summary`
   - 告诉用户：
     - 起草了哪些文件
     - 哪些地方仍需确认
     - 哪些模块还只是 skeleton

---
## 5. What good drafting looks like
1. 一个好的 draft 应该做到：
   - `SKILL.md` 负责总控，不是知识堆场
   - `README.md` 给人类维护者看，不重复 prompt
   - `references/` 承载复杂规则与可复用知识
   - output contract 清楚
   - workflow 是可执行 pipeline
2. 如果你发现 plan 本身有明显冲突：
   - 先指出冲突
   - 给最小修正建议
   - 必要时暂停 drafting，等待用户确认

---
## 6. Questions to ask when blocked
1. 如果没有明确 skill name：
   - 问用户希望的 skill folder / skill identifier 是什么
2. 如果 trigger 边界模糊：
   - 问用户在哪些请求下应该触发，哪些相似请求不应触发
3. 如果 output 不明确：
   - 问用户最终要的 deliverable 是文本、文件、目录结构，还是可执行脚手架
4. 如果 execution layer 不清楚：
   - 问用户现在是先写 prompt/reference skeleton，还是要连 `scripts/` 一起设计

---
## 7. Output contract
1. 默认输出应包含两部分：
   - `draft package`
     - 列出已起草文件
   - `drafting notes`
     - 列出关键设计决定、待确认点、deferred modules
2. 如用户要求直接产出文件内容：
   - 按 plan 分文件输出
   - 保持每个文件边界清晰
3. 如只能先起草部分：
   - 明确说明本轮只完成了哪些层

---
## 8. Writing rules
1. 不要把所有理论都重新塞回 `SKILL.md`。
2. 不要因为可以写很多，就默认写很多。
3. 要优先让 bundle：
   - 清晰
   - 可维护
   - 能继续迭代
4. 对用户未确认的关键事实，宁可留空、标注 `TODO`、或回问，也不要伪造确定性。
