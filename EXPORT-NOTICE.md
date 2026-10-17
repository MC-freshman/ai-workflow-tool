# 公开导出说明（EXPORT NOTICE）

本仓是私有治理仓中 `tool/` 共享目录的**公开导出快照**。为保持许可证清洁与仓库精简，
相对私有正本做了以下**仅删除、不改写**的处理：

## 被排除的内容

所有发布版本下的 `upstream/` 逐字副本目录（vendor snapshots），共涉及 31 个版本目录：

- `math-modeling-programmer/versions/1.1.0 ~ 1.7.2/references/upstream/`（9 个版本，
  含 `nature-skills-main`（Apache-2.0）与 `math-modeling-skill-main`（上游未声明许可证）的完整副本及其图片资产）
- `skills/security-web-resources/versions/1.0.0/upstream/`（MIT 来源的逐字副本）
- `skills/novel-writing-resources/versions/1.0.0/upstream/`（MIT 来源的逐字副本）
- 20 个 `game-*` 工作流版本下的 `upstream/`（MIT 来源的原始工作流单文件）

排除后，所有保留文件的内容与私有正本对应字节**逐字一致**，没有任何修改。

## 保留的溯源信息

- 每个版本的 `SOURCE.json` **完整保留**：来源 sourceId、仓库、快照、许可证、
  以及被排除的上游文件与本仓文件的**逐文件 sha256 对照表**（部分版本）。
- 汇总后的来源清单见 [NOTICE.md](NOTICE.md)。
- 因此，依据 `SOURCE.json` 中的仓库地址、commit 与 sha256，可以从上游重新获取被排除的逐字副本并核对。

## 被排除内容的恢复

上游副本在私有正本中按"已发布版本只读"冻结保存，不随公开仓发布。
如需按原始许可从上游直接获取，请参考 NOTICE 表中的仓库地址与 `SOURCE.json` 记录的快照/commit。
