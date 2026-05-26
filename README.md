---
## 1. `beta-skill-creator` 是什么
1. `beta-skill-creator` 是一个 `architecture-first` 的 skill creation bundle。
2. 它不把重点放在后续的 benchmark / eval loop，而是把重点放在：
   - 先把问题定义清楚
   - 再把 skill 的结构设计清楚
   - 最后再把 skill draft 出来
3. 它把创建 skill 的过程拆成三个独立但可串联的 skill：
   - `skill-briefer`：需求分析、边界澄清、输入确认
   - `skill-architect`：基于 supporting folders 体系推荐架构并输出 plan
   - `skill-drafter`：根据 plan 起草 skill 文件，并在信息不足时与用户沟通

---
## 2. 为什么拆成这三个 skill
1. 这个 repo 的设计假设是：
   - skill creation 不只是“写一个 `SKILL.md`”
   - 更关键的是先判断：
     - 这个 skill 到底要解决什么问题
     - 什么时候触发
     - 应该靠 `prompt`、`reference`、`script` 还是 `config`
2. 所以这里不直接从 drafting 开始，而是按以下流水线分工：
   1. `需求分析`
      - 把目标、输入、触发、输出、边界说清楚
   2. `架构设计`
      - 决定要不要引入 `references/`、`scripts/`、`config/`、`examples/` 等 supporting folders
   3. `draft`
      - 根据 plan 产出 `SKILL.md`、`README.md`、必要 reference skeleton
3. 这种拆法更适合：
   - 从零搭一个 skill
   - 基于已有 skill 做 redesign
   - 想把“文件应该放哪一层”这件事做得更稳定的人

---
## 3. 目录结构
1. 顶层结构：
   - `README.md`：给人看的总说明
   - `install.md`：安装与复用方式
   - `references/`：共享理论、模块体系、设计原则
   - `skills/`：三个独立 skill unit
2. 当前目录：
   ```text
   beta-skill-creator/
   ├── SKILL.md
   ├── README.md
   ├── install.md
   ├── references/
   │   ├── good-skill-principles.md
   │   └── skill-folder-system.md
   └── skills/
       ├── skill-briefer/
       │   ├── README.md
       │   └── SKILL.md
       ├── skill-architect/
       │   ├── README.md
       │   └── SKILL.md
       └── skill-drafter/
           ├── README.md
           └── SKILL.md
   ```

---
## 4. 三个 skill 分别做什么
1. `skill-briefer`
   - 输入：
     - `blank-slate` 的想法、零散笔记、用户口头描述
     - 或已有的 skill folder / `SKILL.md`
   - 输出：
     - 一个结构化的 `intake brief`
   - 核心任务：
     - 澄清问题、触发场景、输出格式、边界、缺失输入
2. `skill-architect`
   - 输入：
     - `intake brief`
     - 或用户直接给出的 skill 目标描述
   - 输出：
     - 一个结构化 `architecture plan`
   - 核心任务：
     - 基于 supporting folders 体系决定 skill 应该由哪些模块组成
     - 判断更偏 `流程化导向` 还是 `路由导向`
3. `skill-drafter`
   - 输入：
     - `architecture plan`
   - 输出：
     - `SKILL.md`、`README.md`、必要 supporting file drafts
   - 核心任务：
     - 按 plan 写 draft
     - 遇到不确定处停下来问用户，不擅自补全关键事实

---
## 5. 共享 references 的作用
1. 这里把共用知识从 skill 主体里拆出来，避免三个 skill 重复写同样的理论。
2. `references/skill-folder-system.md`
   - 解释一个 skill 常见的文件层次：
     - `SKILL.md`、`README.md`
     - `agents/`、`config/`
     - `references/`、`assets/`
     - `scripts/`、`mcp-server/`
     - `evals/`、`tests/`、`examples/`
3. `references/good-skill-principles.md`
   - 归纳“怎样做一个好 skill”的原则
   - 帮三个 skill 在 intake / architecture / drafting 阶段保持一致的设计哲学

---
## 6. 推荐使用方式
1. 最完整的使用方式：
   1. 先用 `skill-briefer`
   2. 再用 `skill-architect`
   3. 最后用 `skill-drafter`
2. 如果你已经很清楚需求：
   - 可以直接跳过 intake，直接进入 `skill-architect`
3. 如果你已经有 plan：
   - 可以直接调用 `skill-drafter`
4. 如果你是在改旧 skill：
   - 推荐先把旧的 `SKILL.md` 或整个 skill folder 交给 `skill-briefer`
   - 让它先识别现状、缺口与重构方向

---
## 7. 设计立场
1. 这个 bundle 默认遵循以下 stance：
   - 先定边界，再定能力
   - 先定结构，再写 prompt
   - 先决定什么放 `SKILL.md`，再决定什么下沉到 `references/` 或 `scripts/`
2. 它不鼓励：
   - 一开始就堆很长的 prompt text
   - 把所有知识硬塞进 `SKILL.md`
   - 在没有 plan 的情况下直接写完整 skill bundle
3. 它更适合帮助用户产出：
   - 可维护、可扩展、可解释的 skill structure

---
## 8. 相关文件
1. 安装与复用方法见 [install.md](install.md)。
2. 三个 skill 的独立说明见：
   - [skills/skill-briefer/README.md](skills/skill-briefer/README.md)
   - [skills/skill-architect/README.md](skills/skill-architect/README.md)
   - [skills/skill-drafter/README.md](skills/skill-drafter/README.md)
3. 共享参考资料见：
   - [references/skill-folder-system.md](references/skill-folder-system.md)
   - [references/good-skill-principles.md](references/good-skill-principles.md)
