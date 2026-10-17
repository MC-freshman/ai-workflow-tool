# 上游来源与致谢（NOTICE）

本仓的技能（skill）、工作流（workflow）与能力包（pack）由 **MC-freshman 与 Codex（OpenAI Codex 命令行助手）协作完成**：
从 GitHub 上的开源 skill 项目中**搜集、筛选、改写与重构**，再按本架构的发布契约
（语义化版本目录、冻结字节、SHA256SUMS、manifest、SOURCE 溯源）重新组织为统一注册表。

## 上游来源汇总

| sourceId | 上游仓库 | 许可证 | 参考范围 |
|---|---|---|---|
| `ecc` | https://github.com/affaan-m/ECC | MIT | 软件工程、数据/基础设施、自动化等领域技能与方法学 |
| `awesome-coding` | https://github.com/Wade-DevCode/awesome-coding-skills-cn | MIT | 中文开发者 AI 编程技能合集（API 设计、CI/CD、代码评审、Godot/Unity/Unreal 等） |
| `mattpocock` | https://github.com/mattpocock/skills | MIT | 工程规划与工程纪律类技能 |
| `nature-skills` | https://github.com/Yuan1z0825/nature-skills | Apache-2.0 | 科研论文写作、图表与可视化类技能（`nature-*`、`paper-*`） |
| `novelhub` | 导入快照 `novel-skills-hub-main`（snapshot-2026.08.31；截至导出时未能在 GitHub 检索到现行 URL） | 导入时标注为 user-confirmed open-source | 中文小说与内容创作类技能（`novel-*`） |
| `gameforge` | https://github.com/AlterLab-IEU/AlterLab_GameForge | MIT | 游戏创作工作流（`game-*`，改写为结构化流水线版本） |
| `math-modeling-skill` | https://github.com/XiaoMaColtAI/math-modeling-skill | **上游仓库未声明许可证（GitHub license = null）** | 数学建模工作流的参考方法；**未包含其逐字副本**，仅保留重构文本与来源指针 |
| `tons-of-skills` | https://github.com/jeremylongshore/tons-of-skills-marketplace | MIT | `skills/security-web-resources`（安全检测技能集合） |
| `oh-story` | https://github.com/zenstory-ai/oh-story-claudecode | MIT | `skills/novel-writing-resources`（小说写作资源） |

大部分上游快照基线为 `snapshot-2026.08.31`；记录了精确 commit 的以其 `SOURCE.json` 为准
（例：security-web-resources 记录 commit `80f86dfbdb02e5d74c625f411ba6834c66ca0705`）。

## 关于 `math-modeling-skill` 的特别说明

上游 https://github.com/XiaoMaColtAI/math-modeling-skill 在 GitHub 上**未声明任何开源许可证**。
在无许可证的情况下，他人对公开仓库仅享有浏览/克隆权，逐字再分发并不当然被授权。
因此本公开导出**没有包含该项目的任何逐字副本**（私有正本的 9 个版本 `references/upstream/` 快照均已排除），
只保留：（1）参考其思路**重新撰写**的工作流与技能文本；（2）`SOURCE.json` 中的来源指针。
如需使用上游原始内容，请直接访问其仓库并遵循作者最新声明。

## 关于 `novel-skills-hub` 的说明

`novel-*` 系列技能的导入快照名为 `novel-skills-hub-main`（snapshot-2026.08.31），
导入时按"用户确认其为开源"登记；截至本次导出，该上游仓库的现行 GitHub 地址未能确认。
本仓保留的是改写后的技能文本而非逐字快照；如上游作者对来源归属有异议，欢迎联系更正。

## 自研部分

以下组件**不来源于上述开源 skill，为本架构原创**（由 MC-freshman 与 Codex 设计实现）：

- 运行引擎与契约：`wf-runner`、`runtime-contracts`、`expert-task`
- 校验与发布工具：`repo-lint`、`platform-conformance`、`architecture-ops`
- 各领域 `*-pipeline` 工作流的编排层、能力包（`packs/`）与注册表工具（`_registry/`）

## 许可证

本仓原创与重构内容以 **Apache License 2.0** 发布（见 `LICENSE`）。
上游内容归各自作者所有，许可证在各 `SOURCE.json` 中逐文件标注；存在冲突时以上游原许可为准。
若本页任何来源 URL 或许可信息过时或错漏，欢迎提 issue 指正。
