---
## 1. `beta-skill-creator` Installation Guide
1. 这个 repo 不是 `Python package` 或 `npm package`。
2. 它的可复用单元主要是：
   - 顶层共享 `references/`
   - `skills/skill-briefer/`
   - `skills/skill-architect/`
   - `skills/skill-drafter/`
3. 最重要的安装原则：
   - 不要只复制某个 `SKILL.md`
   - 要保留对应 skill folder
   - 同时要保留顶层 `references/`，因为三个 skill 都会依赖这些共享文档

---
## 2. 安装时真正要保留什么
1. 最小可用单元不是单文件，而是这整套结构：
   ```text
   beta-skill-creator/
   ├── README.md
   ├── install.md
   ├── references/
   └── skills/
       ├── skill-briefer/
       ├── skill-architect/
       └── skill-drafter/
   ```
2. 原因：
   - `skill-briefer`、`skill-architect`、`skill-drafter` 都不是孤立 prompt
   - 它们会按需读取：
     - `references/skill-folder-system.md`
     - `references/good-skill-principles.md`
3. 如果只复制一个 `SKILL.md`：
   - 共享 reference context 会丢失
   - skill 的设计哲学和 supporting folder taxonomy 会断掉

---
## 3. Quick choice
1. 如果你用 `Codex`：
   - 推荐复制整个 `beta-skill-creator/` 到你的 skill library，再按需做 wrapper
2. 如果你用 `Claude Code`：
   - 推荐保留本地 stable clone
   - 再为三个 skill 分别创建 thin wrapper
3. 如果你用其他 agent：
   - 也建议把整个目录当作 reusable prompt bundle

---
## 4. Install for Codex
1. Clone repo：
   ```bash
   git clone <your-repo-url>
   cd <repo-root>
   ```
2. 安装整套 bundle：
   ```bash
   mkdir -p ~/.codex/skills
   cp -R beta-skill-creator ~/.codex/skills/
   ```
3. 如果你的 agent 只认单个 skill folder：
   - 也不要只复制 `SKILL.md`
   - 至少要让 wrapper 能访问：
     - `beta-skill-creator/skills/<skill-name>/`
     - `beta-skill-creator/references/`
4. Verify：
   - 启动新 session
   - 明确提出类似以下任务：
     - `Help me define a new skill from scratch for literature search and citation export.`
     - `I have an existing skill folder. Analyze it and propose a better architecture.`
     - `Draft the skill bundle from this plan.`

---
## 5. Install for Claude Code
1. Claude Code 更适合用 `wrapper` 方式，而不是把这套 repo 拆碎。
2. 推荐做法：
   - 本地保留整个 `beta-skill-creator/` 目录
   - 在 `~/.claude/agents/` 或 `~/.claude/commands/` 中给三个 skill 建 wrapper

---
## 6. Claude Code subagent wrapper 示例
1. 先保证 repo 在稳定路径，例如：
   ```text
   ~/ai-skills/beta-skill-creator
   ```
2. 为 `skill-briefer` 建 subagent：
   ```bash
   mkdir -p ~/.claude/agents
   cat > ~/.claude/agents/skill-briefer.md <<'EOF'
   ---
   name: skill-briefer
   description: Use proactively when the user wants to define a new skill, refine an existing skill idea, or clarify trigger, scope, inputs, outputs, and boundaries before architecture or drafting.
   ---

   First read `~/ai-skills/beta-skill-creator/skills/skill-briefer/SKILL.md`.
   Then read shared references from `~/ai-skills/beta-skill-creator/references/` when the skill instructs you to.
   Treat the referenced files as the governing workflow.
   EOF
   ```
3. 为 `skill-architect` 建 subagent：
   ```bash
   cat > ~/.claude/agents/skill-architect.md <<'EOF'
   ---
   name: skill-architect
   description: Use proactively when the user wants to choose supporting modules, design a skill folder structure, or decide whether a skill should rely on prompt, references, scripts, config, or routing logic.
   ---

   First read `~/ai-skills/beta-skill-creator/skills/skill-architect/SKILL.md`.
   Then read shared references from `~/ai-skills/beta-skill-creator/references/` when the skill instructs you to.
   Treat the referenced files as the governing workflow.
   EOF
   ```
4. 为 `skill-drafter` 建 subagent：
   ```bash
   cat > ~/.claude/agents/skill-drafter.md <<'EOF'
   ---
   name: skill-drafter
   description: Use proactively when the user already has a skill architecture plan and wants to draft the actual SKILL.md, README.md, references, or other initial files for the skill bundle.
   ---

   First read `~/ai-skills/beta-skill-creator/skills/skill-drafter/SKILL.md`.
   Then read shared references from `~/ai-skills/beta-skill-creator/references/` when the skill instructs you to.
   Treat the referenced files as the governing workflow.
   EOF
   ```

---
## 7. Claude Code slash command wrapper 示例
1. 如果你更喜欢 command 而不是 subagent：
   ```bash
   mkdir -p ~/.claude/commands
   cat > ~/.claude/commands/skill-architect.md <<'EOF'
   Read `~/ai-skills/beta-skill-creator/skills/skill-architect/SKILL.md` first.
   Then read any directly needed files from `~/ai-skills/beta-skill-creator/references/`.

   $ARGUMENTS
   EOF
   ```
2. 然后在 Claude Code 中：
   ```text
   /skill-architect Design a new skill for multi-source academic search and export.
   ```

---
## 8. Install for other agents
1. 如果目标 agent 支持 reusable prompt folders / profile bundles：
   - 直接保留整个 `beta-skill-creator/` 即可
2. 推荐规则：
   1. 复制整个目录
   2. 不要拆开 `skills/` 与 `references/`
   3. 只适配最外层 wrapper 格式，不要改内部相对组织

---
## 9. Common mistake
1. 不要这样做：
   ```bash
   cp beta-skill-creator/skills/skill-architect/SKILL.md ~/.claude/agents/
   ```
2. 这样会导致：
   - skill 脱离共享 references
   - supporting folder taxonomy 和 design principles 不再可用
3. 更稳妥的做法是：
   - 保留 repo 原目录
   - wrapper 指向真正的 `SKILL.md` 与共享 `references/`

---
## 10. Final recommendation
1. 如果你想把这套东西长期复用：
   - 保持一个 stable local clone
   - 给三个 skill 各建一个 wrapper
2. 如果你只想临时参考：
   - 也至少保留整个 `beta-skill-creator/` 目录
3. 总之，安装单位不是单个 `SKILL.md`，而是：
   - `一个 skill folder` + `顶层共享 references`
