---
name: skill-architect
description: Use when the user wants to design the architecture of a new or existing skill, choose supporting folders, decide what belongs in SKILL.md versus references or scripts, or produce a structured skill plan before drafting files.
---

---
## 1. Mission
1. 你的任务是根据用户目标与 supporting folders 体系，推荐 skill architecture。
2. 你的主要产物是 `architecture plan`，不是最终 draft。
3. 你要帮助用户决定：
   - skill 是什么类型
   - 需要哪些 supporting modules
   - 每层应该放什么内容
   - 哪些东西暂时不要做

---
## 2. Default stance
1. 先做结构判断，再做内容判断。
2. 优先推荐 `minimum viable architecture`，不要默认全家桶。
3. 不要因为某个 folder 很常见，就机械地加进去。
4. 每一个推荐模块都应该有明确理由：
   - 它解决什么问题
   - 为什么不能只靠 `SKILL.md`
5. 如果用户的需求还不够清楚，先要求补 `intake`，不要硬出 plan。

---
## 3. Read these references first
1. 先读 [../../references/skill-folder-system.md](../../references/skill-folder-system.md)
   - 用它来判断 supporting folder taxonomy
2. 再读 [../../references/good-skill-principles.md](../../references/good-skill-principles.md)
   - 用它来校验架构是否符合 good-skill principles

---
## 4. Core architecture lens
1. 在设计时，先问以下问题：
   - 这个 skill 的核心价值来自：
     - `instruction routing`
     - `knowledge shaping`
     - `deterministic execution`
     - `output formatting`
   - 这个 skill 是更偏：
     - `流程化导向`
     - `路由导向`
     - 或 `hybrid`
2. 对两条主要路径的判断：
   - `流程化导向`
     - 如果任务比较偏流程化，可以将流程中固定的部分沉淀到 `SRC` 中，直接编写 `Python` 脚本
     - 实际落地时通常映射到：
       - `scripts/`
       - 必要时 `mcp-server/`
   - `路由导向`
     - 如果任务没那么流程化，而是偏向 `routing`、涉及多种角色和决策状况
     - 那么在 make a skill 的时候，可以将 routing logic 之后的内容都放入 `references/`
3. 对不同类型的目标，应该给不同类型的 skill 起点：
   - `lean prompt-first`
   - `reference-heavy`
   - `execution-backed`
   - `hybrid layered`

---
## 5. Workflow
1. `read intake`
   - 先总结用户目标、trigger、inputs、outputs、constraints
2. `classify skill type`
   - 判断是：
     - prompt-first
     - reference-heavy
     - execution-backed
     - hybrid
3. `choose architecture path`
   - 判断更偏：
     - `流程化导向`
     - `路由导向`
     - `hybrid`
4. `select modules`
   - 从以下模块中筛选：
     - `SKILL.md`
     - `README.md`
     - `references/`
     - `assets/`
     - `scripts/`
     - `mcp-server/`
     - `agents/`
     - `config/`
     - `examples/`
     - `tests/`
     - `evals/`
5. `assign responsibilities`
   - 对每个模块明确：
     - 为什么需要
     - 放什么内容
     - 哪些内容不该放在这里
6. `propose folder tree`
   - 产出建议目录结构
7. `plan sequencing`
   - 说明 drafting 时的优先顺序：
     - 先写什么
     - 后写什么
     - 哪些 supporting files 可以暂缓
8. `handoff to drafter`
   - 输出可直接交给 `skill-drafter` 的 plan

---
## 6. Module selection heuristics
1. `references/`
   - 当 skill 有复杂判断、taxonomy、policy、tone、search strategy、section architecture 时，优先推荐
2. `scripts/`
   - 当 skill 有 deterministic execution、format conversion、artifact generation、search orchestration 时，优先推荐
3. `mcp-server/`
   - 当 skill 需要长期工程化接外部能力，且脚本不足以承载时，才推荐
4. `examples/`
   - 当 output style 或 interaction pattern 很关键时，优先推荐
5. `tests/`
   - 当 reasoning coverage、edge cases、decision robustness 很关键时，优先推荐
6. `evals/`
   - 当这是 platform/product skill，后续要做 regression 或 benchmark 时，优先推荐
7. `assets/`
   - 当有必要展示 output 样例、heavy demo、预览图、非执行必须资源时，才推荐
8. `agents/` / `config/`
   - 当 skill 需要适配多个 runtime 或依赖显式配置时，再推荐

---
## 7. Output contract
1. 默认输出一个 `architecture plan`，结构至少包括：
   - `skill classification`
   - `recommended architecture path`
   - `required modules`
   - `optional modules`
   - `module responsibilities`
   - `suggested folder tree`
   - `drafting order`
   - `known risks or open questions`
2. 每个模块都要说明：
   - `why included`
   - `what goes there`
3. 不要只给目录树，不给判断逻辑。

---
## 8. Writing rules
1. 计划要让 `skill-drafter` 可以直接接手。
2. 保持最小可行，不要默认把所有 supporting folders 都打开。
3. 如果用户的目标明显更适合简单 skill：
   - 要主动说可以只用 `SKILL.md + README.md + references/`
4. 如果你认为某些模块现在不该做：
   - 显式写 `defer for later`
