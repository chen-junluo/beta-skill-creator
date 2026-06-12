---
## 1. `skill folder system` 总览
1. 每个 skill 基本都有：
   - `SKILL.md`
     - 这是核心 instruction bundle，定义：
       - `name`
       - `description`
       - 触发场景 `when to use`
       - 默认工作原则 `default stance`
       - workflow
       - output contract
       - 相关支持文件如何调用
   - `README.md`
     - 给人看的说明书，解释 skill 做什么、怎么装、目录里每部分的用途
2. 这两个文件的分工应该保持清楚：
   - `SKILL.md` 面向运行时的 agent
   - `README.md` 面向维护者、安装者、复用者

---
## 2. 4 supporting folders components
1. 然后按职责分成四层；`supporting folders` 的意义不是把材料分类堆放，而是把 skill 的不同工作面拆开，避免所有内容都塞进 `SKILL.md`：
   - 配置层
     - `config/`
       - 存放这个 skill 运行时依赖的显式配置，而不是知识内容本身
       - 用于集中管理默认参数、路径约定、模型路由、外部资源映射等可复用配置
       - 里面应放：
         - `.json`、`.yaml`、`.toml` 一类 config files
         - preset definitions、routing tables、environment-specific mappings
   - 知识库
     - `references/`
       - 存放需要被反复引用的判断框架，而不是一次性的任务说明
       - 用于承载复杂但相对稳定的知识，例如 taxonomy、design principles、writing rules、decision criteria、domain theory
       - 里面应放：
         - conceptual guides
         - decision frameworks
         - reusable rubrics、checklists、glossaries
     - `assets/`
       - 存放不适合写进 `SKILL.md` 或 `references/` 的重型素材
       - 用于提供可被引用但不是每次执行都必须读取的 supporting materials
       - 里面可以放：
         - output screenshots、before/after samples、demo artifacts
         - large prompt examples、image resources、reference datasets
   - 执行层
     - `scripts/`
       - 存放需要稳定复用的可执行步骤，把 deterministic operations 从 prompt 里下沉出来
       - 用于处理格式转换、批处理、抽取、校验、生成中间文件等可脚本化任务
       - 里面应放：
         - shell / python / node scripts
         - parsing、transforming、validating、assembling 用的小工具
     - `mcp-server/`
       - 存放这个 skill 专属的 `MCP server`，把外部系统访问或多步工具操作封装成稳定接口
       - 只有当 skill 需要长期复用的 tool surface、外部服务接入、或结构化 capability 时才需要
       - 里面应放：
         - `MCP server` source code
         - tool schemas
         - service adapters、auth wiring、local launch instructions
   - 质量控制
     - `evals/`
       - 存放可批量运行的 evaluation cases，用来检查 skill 输出是否持续满足预期
       - 重点是 regression checking；不是完整叙事案例，而是可比较、可复跑的样本集
       - 里面可以放：
         - `json` / `yaml` eval sets
         - `prompt`、expected traits、scoring rules、failure notes
       - 可参考 exemplar：
         - [example-eval.md](example-eval.md)
     - `tests/`
       - 存放更完整的 case-level test materials，用来覆盖 edge cases、failure modes、workflow branching
       - 比 `evals/` 更重，因为它强调单个场景的上下文、步骤和判定标准
       - 里面应放：
         - one case per file 的 test docs
         - setup、input、expected behavior、pass/fail criteria
       - 可参考 exemplar：
         - [example-test.md](example-test.md)
     - `examples/`
       - 存放 few-shot examples，作用是教 skill 学会“怎么处理”，不是证明 skill “测过了”
       - 适合保存长输入、代表性任务、目标响应风格
       - 每个 example 至少应包含：
         - `input`
         - `expected handling`
         - `response style`
         - 如有必要，再补 `example context` 或 `target output`
       - 可参考 exemplar：
         - [example-example.md](example-example.md)

---
## 3. 固定流水线
1. 它们几乎都遵循一个固定流水线：
   - `SKILL.md`
     - `trigger`
       - 由 `SKILL.md` 的 `description` 和开头规则定义
     - `stance / guardrails`
       - 明确不能做什么、默认怎么做
     - `workflow`
       - 把复杂任务拆成 `5–10` 步
     - 连接知识库
       - `supporting knowledge`
         - 从 `references/` 或者 `assets/` 读取特定知识
     - 连接执行层
       - 如果需要，就调用 `scripts/` 或 `mcp-server/`
     - 质量控制
       - prompt 写清楚 `output contract`，明确最后返回什么格式
       - 用 `evals/`、`tests/`、`examples/` 保证稳定性
2. 这个流水线背后的意思不是“每个 skill 都要有所有文件夹”，而是：
   - 每个 skill 都应该知道自己的：
     - trigger 在哪定义
     - guardrails 在哪定义
     - workflow 在哪展开
     - knowledge 从哪读
     - execution 由谁承担
     - output 怎样被约束

---
## 4. 各层更适合在什么情况下出现
1. 不要把 `supporting folders` 当成固定模板；判断标准不是“目录是否完整”，而是这个 skill 是否真的出现了对应职责：
   - 只有 prompt 就能稳定完成的 skill
     - 通常只需要 `SKILL.md`，最多再加少量 `references/`
   - 出现可复用参数、跨 runtime 适配、外部资源映射
     - 再引入配置层，例如 `config/`、`agents/`
   - 出现大量稳定知识，已经不适合继续堆在主 prompt 里
     - 再引入知识库层，例如 `references/`，必要时补 `assets/`
   - 出现可脚本化、可工具化、需要稳定复用的操作
     - 再引入执行层，例如 `scripts/` 或 `mcp-server/`
   - 出现回归风险、边界场景增多、需要验证 skill 是否退化
     - 再引入质量控制层，例如 `evals/`、`tests/`、`examples/`
2. 一个简单判断法是看某段内容到底属于哪种职责：
   - 如果它定义的是行为总控、trigger、workflow、output contract
     - 放在 `SKILL.md`
   - 如果它提供的是长期稳定的判断依据
     - 放在 `references/`
   - 如果它提供的是运行参数或环境映射
     - 放在 `config/` 或 `agents/`
   - 如果它承担的是实际执行步骤
     - 放在 `scripts/` 或 `mcp-server/`
   - 如果它用来演示、覆盖或检验输出质量
     - 放在 `examples/`、`tests/`、`evals/`

---
## 5. 如何用这份 reference
1. 在做一个新 skill 时，可以先问四个问题：
   1. 最小必需文件是什么
   2. 哪些 supporting folders 是真正需要的
   3. 哪些知识适合下沉到 `references/`
   4. 有没有执行环节应该沉淀为 `scripts/` 或 `mcp-server/`
2. 在改一个旧 skill 时，也可以用这份 reference 检查：
   - 它是不是把太多内容硬塞进 `SKILL.md`
   - 它是不是缺少 execution layer
   - 它是不是没有清楚区分 examples / tests / evals
3. 这份文档更像 `taxonomy + routing map`，不是模板本身。
