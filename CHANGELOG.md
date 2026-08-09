# 更新日志

本项目所有重要变更均会记录在此文件中。

格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [未发布]

### 变更

- 仓库重建（2026-08-09）：XPilot 工具从仓库内子项目拆出为**独立仓库** [xhqing/XPilot](https://github.com/xhqing/XPilot)（工具侧改回独立工具项目、版本 0.5.1，功能不变）；本仓库恢复为纯 Agent 项目，README（中英双语）、`.claude/CLAUDE.md`、`.codebuddy/CODEBUDDY.md` 同步改为指向独立 XPilot 仓库。**为什么**：8-08 的 Agent 化把工具塞进 `XPilot/` 子目录、仓库与目录改名 `NetOpsAgent`，实际使用中发现工具独立成库更合适——Agent 定位（Hermes）保留在本仓库，工具独立演进、互不干扰。
- 项目级配置按 fleet 标准补齐：`.claude/settings.json`（hooks 空，AutoMemory 已全局禁用）、`.claude/settings.local.example.json`（入库模板）+ `.claude/settings.local.json`（本机，已 gitignore）、`.gitignore`（运行时数据 / 密钥 / 本地配置一律忽略）。

### 移除

- 移除与全局重复的通用能力副本：`.claude/skills/anysearch/`、`.claude/skills/find-skill/`、`.claude/rules/`（通用三件套）、`.claude/commands/install-skill.md`；`.gitignore` 同步去掉 find-skill 忽略条目。**为什么**：按全局新规则「通用能力开源单一出口」（2026-08-09 立），新建 Agent 项目不再放置与全局 `~/.claude/` 重复的通用能力——全局通用能力已由 CapabilityManagerAgent（Prometheus）的 `claude/` 镜像一次性开源，各项目不再重复维护副本（副本易过期分叉，本次新建时就发现 anysearch `runtime.conf` 副本与全局不一致、find-skill 副本多出 `.env.example`）。项目只保留独有能力与配置（settings、README、CLAUDE.md 等）。

## [1.0.0] - 2026-08-08

### 新增

- 项目定位为「网络运维管理员 Hermes」Agent 项目：仓库根目录承载 Agent 定位与对外文档（README 中英双语 + LOGO + 徽章 + 版权署名），并注册到全局 fleet 智能体命名注册表（Hermes / NetOpsAgent，独立于销售流水线）。
- XPilot 独立子项目（`XPilot/`）：CLI 工具的代码、配置、测试、Docker 与开发工具链全部迁入 `XPilot/` 子目录，工具自身沿用其独立的 README / CHANGELOG / VERSION / LICENSE；发布工作流（`.github/workflows/release.yml`）在 `XPilot/` 目录内构建并上传 Release 资产。
