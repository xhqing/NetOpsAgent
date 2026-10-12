# NetOpsAgent — Agent 项目说明

**拟人名**：Hermes（赫尔墨斯）
**职称**：网络运维管理员（Network Operations Agent）
**团队项目名**：NetOpsAgent
**仓库**：xhqing/NetOpsAgent

本项目是 Agent 项目，定位为「网络运维管理员 Hermes」——总体职责是处理**网络连接相关的问题**（代理转发只是众多网络问题中的一部分），当前专职节点真实流量测速、自动选路、故障转移、订阅刷新。项目根目录为 Agent 定位与对外文档；**XPilot** 是 Hermes 开发的 CLI 工具——一个方便使用 Xray-core 的 Python CLI 工具，通过 `xpilot` 命令提供全部节点管理能力，位于**独立仓库** [xhqing/XPilot](https://github.com/xhqing/XPilot)。CLI 命令名保持 `xpilot`（向后兼容，不改命令名与包名）；Agent 化体现在定位、README 人格与团队注册表，不影响工具实际功能。

## 目录结构

- 根目录 README：Agent 项目（Hermes）对外说明，指向独立仓库 XPilot 的工具文档。
- 根目录 `CLAUDE.md`（本文件）：项目角色化说明的单一来源；根目录 `AGENTS.md`、`CODEBUDDY.md` 均为指向它的相对软链接，兼容只认这两种入口文件名的 agent 工具。
- 通用能力（skills / rules 等）从全局 `~/.claude/` 或 CapabilityManagerAgent 的 `claude/` 开源镜像获取，项目内不留副本、不建 `.claude/` 目录（「通用能力开源单一出口」规则，2026-08-09 立）。
- 工具本体在独立仓库 [xhqing/XPilot](https://github.com/xhqing/XPilot)（含其独立 README、配置、测试、Docker 与开发工具链）。

## 子项目清单

本项目（Hermes）负责维护以下子项目。按全局规则「智能体专属文件归属与子项目映射」（2026-10-12 用户修订，取代原「子项目 `.claude/` 超集」规则；细则见 `~/.claude/docs/agents-registry.md`）：`CLAUDE.md` / `AGENTS.md` / `.claude/` / 项目级 `.pi/` 等智能体专属文件**只有 Agent 项目允许拥有，子项目一律不得存在**；子项目的工作在本 Agent 项目会话里按路径操作（如 `git -C <子项目目录>`），通过 intercom / `agent_call` / `agent_wake` 开启的后台会话一律以本 Agent 项目根目录为工作目录。

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
