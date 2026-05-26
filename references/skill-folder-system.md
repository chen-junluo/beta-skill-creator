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
## 2. supporting folders 的层级
1. 然后按复杂度再挂不同的 supporting folders：
   - 配置层
     - `agents/`
       - 考虑了把 skill 适配到其他 agent/runtime
     - `config/`
       - 存放配置层
   - 知识库
     - `references/`
       - 知识库、整套设计理论
     - `assets/`
       - 不是执行必须。heavy 的资产
       - 用来：
         - 绘图结果示例、绘图结果代码（都可以分类）
         - 展示装配之后的输出效果图
   - 执行层
     - `scripts/`
     - `mcp-server/`
       - 工程化的体现
   - 质量控制
     - `evals/`
       - 测试 skill 表现是否符合预期
       - 可以是一个 `json` 文件里面放 `prompt` 和预期输出
     - `tests/`
       - 比 `evals` 要 heavy，每一个 `md` 文件代表一个 case
     - `examples/`
       - 比较长的 few-shot 样本存放地
       - example 应至少包含：
         - `example`
         - `input`
         - `expected handling`
         - `response style`

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
## 4. 各层的推荐职责边界
1. `SKILL.md`
   - 负责总控
   - 不负责承载全部细节知识
2. `references/`
   - 负责承载复杂判断、taxonomy、policy、theory、tone、section architecture
3. `scripts/` / `mcp-server/`
   - 负责真实执行、格式转换、multi-step deterministic operations
4. `config/`
   - 负责 runtime configuration、adapter data、external linkage
5. `examples/` / `tests/` / `evals/`
   - 负责稳定性与质量控制，但侧重点不同：
     - `examples/`：few-shot demonstration
     - `tests/`：case coverage
     - `evals/`：regression and automated checking

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
