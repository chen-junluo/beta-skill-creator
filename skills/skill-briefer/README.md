---
## 1. `skill-briefer` 是做什么的
1. `skill-briefer` 负责 skill creation 的第一步：把问题定义清楚。
2. 它适合两类起点：
   - 从 `0` 开始，用户只有一个模糊想法
   - 用户已经有一个旧 skill、旧 `SKILL.md`、或一个现有 folder，想先分析现状再重做
3. 它的输出不是最终 skill，而是一个结构化 `intake brief`，供 `skill-architect` 继续使用。

---
## 2. 输入与输出
1. 输入可以是：
   - 一句话需求
   - 零散笔记
   - 一个已有 `SKILL.md`
   - 一个已有 skill folder 的结构说明
2. 输出应该包括：
   - 问题定义
   - 触发条件
   - 输入 / 输出
   - 边界与红线
   - 缺失信息
   - 是否已经足够进入 architecture 阶段

---
## 3. 和其他 skill 的关系
1. 它是前置 skill。
2. 推荐衔接：
   - `skill-briefer` → `skill-architect` → `skill-drafter`
3. 如果用户已经有清晰 plan，可以跳过它。

---
## 4. 相关文件
1. 主指令见 [SKILL.md](SKILL.md)。
2. supporting folder taxonomy 见 [../../references/skill-folder-system.md](../../references/skill-folder-system.md)。
3. 设计原则见 [../../references/good-skill-principles.md](../../references/good-skill-principles.md)。
