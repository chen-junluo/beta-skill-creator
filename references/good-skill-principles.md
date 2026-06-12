---
## 1. 第一原则：不要一开始就堆很多 `prompt text`
1. 更好的方式是先分层：
   - `SKILL.md`
     - 只放：
       - trigger
       - default stance
       - workflow
       - output contract
       - “什么时候打开哪些 supporting files”
   - 细节规则下沉到 `references/`
2. 原因：
   - `SKILL.md` 太长会变成不可维护的大杂烩
   - 而 `references/` 能模块化复用
3. 如何落地：
   - 先写最小 `SKILL.md`
   - 再把 taxonomy、policy、tone、section logic 拆到 `references/`

---
## 2. 第二原则：skill 先定义“边界”，再定义“能力”
1. 一个好 skill 应该先说清楚：
   - 不要编造
   - 不要越界
   - 什么时候停下来问用户
   - 哪些情况只输出草稿
2. 所以下一个 AI 做 skill 时，先写：
   - `default stance`
   - `red lines`
   - `source hierarchy`
   - `missing-input policy`
3. 如何落地：
   - 不要一上来写花哨 workflow
   - 先把 `guardrails` 与 escalation policy 写稳

---
## 3. 第三原则：workflow 要写成 `deterministic pipeline`
1. 不要只说“帮用户做 X”。
2. 要写成：
   - `1. intake`
   - `2. classify`
   - `3. gather evidence`
   - `4. produce draft`
   - `5. run QA`
   - `6. return output`
3. 原因：
   - 这样 AI 更容易稳定执行，也更容易 debug
4. 如何落地：
   - 把 skill 的动作写成 `5–10` 步
   - 每一步写清楚输入、判断点、输出

---
## 4. 第四原则：把 output 当成 `contract`，而不是随意发挥
1. 例如最终产物可能是：
   - `paper.md`
   - `source_map.json`
   - `translation_notes.md`
   - `references.enw`
   - `qa_report.md`
2. 如果一个 skill 最终产物很重要，建议单独放：
   - `references/output-spec.md`
3. 原因：
   - 这样能明显提升 consistency
4. 如何落地：
   - 在 `SKILL.md` 中显式定义 output format
   - 对复杂产物额外写一份 output spec

---
## 5. 第五原则：有复杂判断时，一定要把知识拆到 `references/`
1. 比如：
   - taxonomy
   - policy
   - tone
   - search strategy
   - section architecture
2. 这样 AI 在运行时可以：
   - 先 routing
   - 再按需打开具体 reference
3. 这比把所有知识硬塞在 `SKILL.md` 更强。
4. 如何落地：
   - 把稳定、复杂、可复用的判断知识沉淀到 `references/`
   - 在主 skill 中只保留“什么时候去看哪个 reference”

---
## 6. 第六原则：如果 skill 涉及真实执行，尽量补 `scripts/` 或 `mcp-server/`
1. 纯 prompt 适合：
   - polishing
   - writing
   - response drafting
2. 但如果任务是：
   - citation export
   - format conversion
   - multi-source search
   - artifact generation
3. 最好补 execution layer：
   - `scripts/`
   - 或 `mcp-server/`
4. 原因：
   - 否则 skill 只能“会说”，不一定“会做”
5. 如何落地：
   - 识别那些 deterministic、重复、工具化强的步骤
   - 优先沉淀为 `scripts/` 或服务接口

---
## 7. 第七原则：`examples`、`tests`、`evals` 至少选一个
1. 最佳组合：
   - `examples/` 负责教模型“应该怎样处理”，本质是 few-shot demonstration
     - 它强调：
       - 代表性输入长什么样
       - 理想处理路径是什么
       - 回答风格、结构、颗粒度应该如何呈现
     - 它更像 teaching material，不是 pass/fail harness
   - `tests/` 负责覆盖“哪些场景必须处理对”，本质是 case coverage
     - 它强调：
       - 边界条件
       - 分支判断
       - 常见失败模式
       - 每个 case 的 expected behavior 与判定标准
     - 它更像 scenario-based spec，不是 few-shot，也不一定可自动运行
   - `evals/` 负责检查“这项能力有没有退化”，本质是 automated regression surface
     - 它强调：
       - 一组可重复运行的 prompt / input set
       - 可比较的 expected traits 或 scoring rules
       - 版本之间是否变好、变差、或出现回归
     - 它更像 benchmark / regression harness，不承载长篇上下文教学
2. 三者的边界：
   - `examples/` 解决的是：
     - “模型该怎么做”
     - 不解决：
       - 系统性覆盖 edge cases
       - 稳定回归比较
   - `tests/` 解决的是：
     - “哪些情形必须过关，失败会怎么失败”
     - 不解决：
       - 教模型形成统一文风
       - 大规模自动跑分
   - `evals/` 解决的是：
     - “改完之后整体表现有没有退化，哪些维度波动了”
     - 不解决：
       - 细致解释单个案例背后的处理思路
       - 替代完整的 few-shot example 或 test spec
3. 如果只能选一个：
   - reasoning-heavy skill 先选 `tests/`
     - 因为这类 skill 最怕 decision boundary 不稳，先把 case coverage 立住
   - output-style skill 先选 `examples/`
     - 因为这类 skill 最怕风格漂移、结构失真，先把 exemplar 写清楚
   - platform / product / workflow skill 先选 `evals/`
     - 因为这类 skill 最怕迭代后 regression，先建立可重复比较的检查面
4. 如何落地：
   - 不一定三个都做，但至少挑一种质量控制机制，不要完全裸奔
   - 一个简单顺序是：
     1. 先用 `examples/` 教会目标行为
     2. 再用 `tests/` 补关键 edge cases
     3. 最后用 `evals/` 把高频能力做成可回归检查
   - 当 repo 还很早期：
     - 先选最能解决当前主要风险的那一种，而不是为了“目录完整”三种都建空壳
