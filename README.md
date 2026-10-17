# AI Workflow · Tool Registry

一个多平台 AI 工作流架构的**共享工具仓**：2000+ 个技能（skill）、8 个能力包（pack）、
55 个工作流（workflow）与运行引擎/契约工具，以语义化版本目录 + 冻结字节 + SHA256 校验的方式发布，
可被 Codex、Qoder、ZCode、WorkBuddy、豆包（Doubao）等任意命令行 AI 客户端按统一契约加载。

> 这些技能与工作流**由 Codex（OpenAI Codex CLI）与作者本人（MC-freshman）协作完成**：
> 从 GitHub 上的开源 skill 项目中**搜集、筛选、改写与重构**，再按本架构的版本、锁定与验收契约重新组织；
> 同时包含一套本架构自研的运行引擎与契约工具。
> 完整的上游来源与许可证清单见 [NOTICE.md](NOTICE.md)，每个版本的逐文件来源记录见其 `SOURCE.json`。

## 目录结构

```
tool/
├── registry.json                 # 全局注册表（技能/包/工作流指针）
├── skills/<skill-id>/
│   ├── current.json              # 技能当前版本指针
│   └── versions/<semver>/
│       ├── SKILL.md              # 技能定义（触发条件、步骤、约束）
│       ├── manifest.json         # 技能清单
│       ├── references/ scripts/  # 参考资料与可执行脚本（如适用）
│       ├── SOURCE.json           # 上游来源、许可与逐文件溯源
│       └── SHA256SUMS            # 冻结校验和
├── packs/<pack-id>/              # 能力包：把一组技能按领域打包（如 game-core、security-audit）
├── <workflow-id>/versions/<semver>/
│   ├── workflow.md / workflow.yaml   # 分阶段工作流定义（阶段、门禁、修复回路）
│   ├── schemas/ scripts/ tests/      # 输入输出契约、门禁脚本与测试
│   ├── SOURCE.json / SHA256SUMS
├── _registry/                    # 技能分源目录（skills-<source>.json）与发布/校验脚本
└── docs/REGISTRY-README.md       # 注册表内部原始说明（保留结构溯源）
```

**已发布版本只读、不可覆盖**：任何修改都必须新建语义化版本目录，并通过 `current.json` 切换默认指针。

## 内容组成

### 1. 技能（skills/，2000+ 发布目录）

按来源家族重构的技能，在 `SOURCE.json` 中逐批标注来源：

| 家族 | 来源（详见 NOTICE） | 覆盖内容 |
|---|---|---|
| `nature-*` / `paper-*` | Yuan1z0825/nature-skills（Apache-2.0） | 论文写作、图表、审稿、专利与统计 |
| `novel-*` | novel-skills-hub / oh-story（MIT） | 小说与中文内容创作、剧本、封面 |
| `coding-*` / `matt-*` | ECC、awesome-coding-skills-cn、mattpocock/skills（均 MIT） | 工程纪律、API 设计、CI/CD、调试、安全评审 |
| `*-task-*`、`paper-programmer-*` 等 | 自研工作流配套技能 | 六阶段任务卡、论文编程流水线 |
| `security-web-resources` | tons-of-skills-marketplace（MIT） | Web 安全检测与漏扫方法 |

### 2. 工作流（55 个顶层目录）

- 领域流水线：`automation-engineer-pipeline`、`data-analyst-pipeline`、`se-pipeline`、
  `novel-pipeline`、`paper-pipeline`、`game-pipeline` 等 20+ 条专家主流水线。
- 游戏创作全流程：`game-brainstorm`、`game-gdd-author`、`game-prototype`、`game-playtest`、
  `game-ci-pipeline`、`game-launch` 等（参考 MIT 的 AlterLab GameForge 重构为带门禁的结构化流水线）。
- 数学建模：`math-modeling-programmer`（建模分析 → 编程 → 论文/图表三阶段）。
- 安全：`mastermind-bug-bounty`、`mastermind-peer-task`。
- 可视化质检：`visualization-qa`。

### 3. 自研运行引擎与契约工具（非搜集重构，为本架构原创）

| 组件 | 职责 |
|---|---|
| `wf-runner` | 工作流运行引擎：阶段展开、分档严谨度、门禁、修复回路、run 锁定 |
| `runtime-contracts` | run-lock / handoff 等运行时契约 schema |
| `expert-task` | 专家任务编排入口 |
| `repo-lint` | 三仓一致性与冻结字节校验器 |
| `platform-conformance` | 平台能力地板与符合性报告（单条 `conform` 命令） |
| `architecture-ops` | 验收矩阵与运维操作工具 |

## 版本与锁定机制

- 解析顺序：显式版本 → 平台本地默认 → 资源 `current.json`；执行前记录确切版本与来源。
- Agent 通过 `tool-lock.json` 精确锁定本仓技能/工作流/包版本，平台默认不能覆盖。
- 技能与工作流发布物冻结、不可变；`SHA256SUMS` 是字节级权威，`SOURCE.json` 是来源级权威。
- 运行期状态（run、产物、日志、凭据）属于加载它的平台，**本仓不存放任何运行时内容**。

## 与姊妹仓的关系

| 仓库 | 职责 |
|---|---|
| [ai-workflow-agent](https://github.com/MC-freshman/ai-workflow-agent) | 专家 Agent：提示词、领域策略、测试与版本锁（锁定本仓实体） |
| **tool**（本仓） | 技能、能力包、工作流与运行引擎 |
| software 仓 | 外部软件配方与能力快照（暂未公开发布） |

## 快速开始

1. 阅读 `registry.json` 与 `_registry/skills-<source>.json`，按来源/领域定位技能。
2. 打开目标 `versions/<semver>/SKILL.md`（或 `workflow.yaml`）了解能力与契约。
3. 用 `SHA256SUMS` 校验字节，用 `SOURCE.json` 查看来源与许可。
4. 本公开导出相对私有正本的差异（排除了上游逐字副本）见 [EXPORT-NOTICE.md](EXPORT-NOTICE.md)。

## 许可证

[Apache License 2.0](LICENSE)。上游内容归各自作者所有，来源与许可见 [NOTICE.md](NOTICE.md) 与各 `SOURCE.json`；
自研引擎与工具同样以 Apache-2.0 发布。

## 说明

本仓为共享资源的**定义与发布面**，不含平台配置、密钥、运行时环境或任何项目输出；
仓库中出现的内部工作区路径（如 `E:\ai\...`）是开发期绝对路径，仅用于溯源，不影响在其他环境加载。
