# Research Agent Kit — 通用科研 Agent 协作模板

面向计算科学、机器学习与实验类科研项目的通用 Agent 工作流包，工具无关，兼容 Antigravity、Codex、Claude Code 等读取 `AGENTS.md` 与 `.agents/skills/` 的工具。

核心结构为**“两文档 + 模块化知识库 + 飞轮 + 按需 Skills”**：
- `docs/PROJECT.md` 聚焦**论文故事线**与**模块索引**（其余宏观项按需增删）。
- `docs/modules/*.md` 按模块四段式沉淀现行认识与踩坑记录。
- `docs/TODO.md` 维护当前状态「现在」、问题队列、临时排查笔记与版本路径表。
- `.agents/skills/auto-drive/` 支持口令开启自动驾驶（独立分支单飞轮自治，或 `git worktree` 多飞轮并行探索）。

## 目录结构

```text
.
├── AGENTS.md                        # 常驻核心约定（每次会话加载）
├── docs/
│   ├── PROJECT.md                   # 论文故事线 + 模块索引 + 可选宏观补充
│   ├── TODO.md                      # 「现在」状态块 + 问题队列 + 版本与路径表
│   ├── modules/
│   │   └── _TEMPLATE.md             # 模块四段式模板（按项目核心组件复制）
│   └── records/                     # 冻结的历史快照（预登记协议、定案记录）
└── .agents/
    └── skills/                      # 按需加载的科研技能
        ├── research-flywheel/       # 取 TODO → 查历史/挑刺/定判据 → 写代码+冒烟测试
        ├── auto-drive/              # 口令开启自动驾驶：单飞轮自治 / git worktree 多飞轮并行
        ├── log-finding/             # 实验收敛后原地更新模块文档与 TODO「现在」
        ├── release-component/       # 组件定案：升版本常量 → 更新文档 → 打 annotated tag
        ├── data-inspect/            # 先看图再看数：离线 HTML 查看器与分层诊断
        └── paper-writing/           # 论文叙事、查重、防泄露评测与改稿规范
```

## 快速接入（新项目 / 已有项目）

1. 将本包解压到项目仓库根目录（已有项目注意避免覆盖已存在的 `docs/PROJECT.md` 与 `docs/TODO.md`）。
2. **工具适配**：
   - **Antigravity / Codex 等原生支持 `AGENTS.md` 与 `.agents/skills/` 的工具**：开箱即用，无需额外配置。
   - **Claude Code（可选）**：如需兼容，建立软链接：
     ```bash
     ln -s AGENTS.md CLAUDE.md
     mkdir -p .claude && ln -s ../.agents/skills .claude/skills
     ```
3. 初始化项目文档：
   - 填写 `docs/PROJECT.md` 的**论文故事线**和**模块索引**（其余宏观项按需保留或删掉）。
   - 按模块索引复制 `docs/modules/_TEMPLATE.md` 为各模块文档。
   - 在 `docs/TODO.md` 填入当前正在跑的任务和问题队列。
4. 提交初始化 commit：

```bash
git add AGENTS.md .agents docs
git commit -m "chore: initialize research agent workflow and docs structure"
```

## 常用口令示例

- **正常飞轮**：`取 TODO 顶部非【卡】问题跑一圈飞轮`
- **单路 Auto-Drive**：`开启 auto-drive：排查 TODO #3，预算 3 轮、单次 ≤15 分钟、GPU 1`
- **多路并行 Auto-Drive**：`开启并行 auto-drive：飞轮 A 用 GPU 0 跑 TODO #2，飞轮 B 用纯 CPU 查 TODO #4，各最多 3 轮`
- **收敛落盘**：`执行 log-finding，把今天结论落盘`
