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
   - `examples/` 给 few-shot
   - `tests/` 给 case coverage
   - `evals/` 给自动回归
2. 如果只能选一个：
   - reasoning-heavy skill 先选 `tests/`
   - output-style skill 先选 `examples/`
   - platform/product skill 先选 `evals/`
3. 如何落地：
   - 不一定三个都做
   - 但至少挑一种质量控制机制，不要完全裸奔

---
## 8. 第八原则：`README` 不是可有可无
1. 这里做得好的 skill 基本都有 `README.md`。
2. `README.md` 的作用不是重复 `SKILL.md`，而是：
   - 给人类维护者看
   - 解释 file structure
   - 说明 design intent
   - 说明安装和适配方法
3. 如何落地：
   - 把 `README.md` 当作维护文档，而不是 prompt 的副本
   - 写清楚目录作用、依赖关系、适配方式
