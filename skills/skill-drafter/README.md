---
## 1. `skill-drafter` 是做什么的
1. `skill-drafter` 负责 skill creation 的第三步：把 plan 落成第一版 skill bundle。
2. 它的重点是 drafting，不是重新做 architecture。
3. 它适合：
   - 用户已经有 `architecture plan`
   - 用户希望开始写 `SKILL.md`、`README.md`、以及必要 supporting files

---
## 2. 输入与输出
1. 输入最好是：
   - 一个结构化 `architecture plan`
2. 输出可以是：
   - `SKILL.md` draft
   - `README.md` draft
   - 必要的 `references/*` 初稿
   - 如 plan 要求，也可以包括 `examples/`、`tests/`、`evals/` 的 skeleton
3. 如果 plan 不完整：
   - 先指出缺口
   - 再向用户提问，而不是静默脑补

---
## 3. 和其他 skill 的关系
1. 它是最后一段。
2. 推荐输入来源：
   - `skill-architect` 的输出 plan
3. 如果用户没有 plan，建议先回到 `skill-briefer` 或 `skill-architect`。

---
## 4. 相关文件
1. 主指令见 [SKILL.md](SKILL.md)。
2. supporting folder taxonomy 见 [../../references/skill-folder-system.md](../../references/skill-folder-system.md)。
3. 设计原则见 [../../references/good-skill-principles.md](../../references/good-skill-principles.md)。
