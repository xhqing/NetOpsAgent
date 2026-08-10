# NetOpsAgent — Agent 项目说明

**拟人名**：Hermes（赫尔墨斯）
**职称**：网络运维管理员（Network Operations Agent）
**fleet 项目名**：NetOpsAgent
**仓库**：xhqing/NetOpsAgent

本项目是 Agent 项目，定位为「网络运维管理员 Hermes」——总体职责是处理**网络连接相关的问题**（代理转发只是众多网络问题中的一部分），当前专职节点真实流量测速、自动选路、故障转移、订阅刷新。项目根目录为 Agent 定位与对外文档；**XPilot** 是 Hermes 开发的 CLI 工具——一个方便使用 Xray-core 的 Python CLI 工具，通过 `xpilot` 命令提供全部节点管理能力，位于**独立仓库** [xhqing/XPilot](https://github.com/xhqing/XPilot)。CLI 命令名保持 `xpilot`（向后兼容，不改命令名与包名）；Agent 化体现在定位、README 人格与 fleet 注册表，不影响工具实际功能。

## 目录结构

- 根目录 README：Agent 项目（Hermes）对外说明，指向独立仓库 XPilot 的工具文档。
- `.claude/`：本项目独有的能力与配置目录（settings 等）。**不放与全局重复的通用能力**——通用 skills / rules 从全局 `~/.claude/` 或 CapabilityManagerAgent 的 `claude/` 开源镜像获取（「通用能力开源单一出口」规则，2026-08-09 立）。
- `.codebuddy/CODEBUDDY.md`：CodeBuddy 项目说明（一行引用 `../.claude/CLAUDE.md`，单一来源）。
- 工具本体在独立仓库 [xhqing/XPilot](https://github.com/xhqing/XPilot)（含其独立 README、配置、测试、Docker 与开发工具链）。

## 子项目清单

本项目（Hermes）负责维护以下子项目，`.claude/` 与子项目 `.claude/` 之间维护「Agent 项目为权威源、子项目为超集」的关系（全局规则「Agent 项目与子项目的 `.claude/` 超集关系」，2026-08-10 立）：本文件全文随附进子项目 `.claude/CLAUDE.md`，其中「本项目」均指 NetOpsAgent。

- **NetOpsAgent（Hermes）→ XPilot**：独立仓库 [xhqing/XPilot](https://github.com/xhqing/XPilot)，Hermes 开发的 Xray-core 节点管理 CLI 工具。

## commit skill 检测缓存

<!-- commit-skill: readme-standard = ok -->
- README 中英双语 + LOGO + 徽章 + 版权署名：已就绪（2026-07-22 确认；2026-08-07 徽章更新为 Agent 标准 + 加 Hermes 身份节）

<!-- commit-skill: license = ok -->
- LICENSE.md：已存在，无冗余（2026-07-22 确认）

<!-- commit-skill: github-about = ok -->
- GitHub About：已配置于 xhqing/NetOpsAgent（英文 description + topics，2026-07-22）

<!-- commit-skill: attribution-name = ok -->
- 版权人/署名引用名字：已归一为 All Contributors（2026-07-22 确认）

<!-- commit-skill: readme-link-text = ok -->
- 英文版 README 跳转中文版链接文字：已统一为「简体中文」（2026-07-22 确认）

<!-- commit-skill: repo-sponsors = ok -->
- 仓库 Sponsors 按钮：已就绪（xhqing/.github 全局默认 FUNDING.yml，2026-07-22 确认）

## 跳过的检测项及原因

- **automemory（9e）**：按全局 `~/.claude/CLAUDE.md` 约定（2026-07-20 立），AutoMemory 全局已禁用（`autoMemoryEnabled: false`），新建项目一律不配 AutoMemory。故本项目不创建 `.claude/memory/`、不写 `autoMemoryDirectory`、`.gitignore` 不挂 memory 条目，9e 永久跳过。
