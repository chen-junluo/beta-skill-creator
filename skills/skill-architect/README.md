---
## 1. `skill-architect` 是做什么的
1. `skill-architect` 负责 skill creation 的第二步：根据目标与 supporting folders 体系，给出 skill architecture plan。
2. 它的重点不是写正文，而是决定：
   - 哪些模块要有
   - 各模块放什么
   - 什么内容留在 `SKILL.md`
   - 什么内容下沉到 `references/`、`scripts/`、`examples/` 等
3. 它特别适合：
   - 用户已经有一个 `brief`
   - 用户已经知道大致目标，但不知道 skill folder 怎么搭

---
## 2. 输入与输出
1. 输入可以是：
   - 来自 `skill-briefer` 的结构化 brief
   - 用户直接给出的目标描述
2. 输出应该是一个 `architecture plan`，至少包括：
   - skill 类型判断
   - 推荐 supporting folders
   - 每层职责边界
   - 建议目录结构
   - 是否偏 `流程化导向` 或 `路由导向`

---
## 3. 和其他 skill 的关系
1. 它位于中间层。
2. 推荐衔接：
   - `skill-briefer` → `skill-architect` → `skill-drafter`
3. 如果用户已经有成熟 plan，可以跳过它。

---
## 4. 相关文件
1. 主指令见 [SKILL.md](SKILL.md)。
2. supporting folder taxonomy 见 [../../references/skill-folder-system.md](../../references/skill-folder-system.md)。
3. 设计原则见 [../../references/good-skill-principles.md](../../references/good-skill-principles.md)。
