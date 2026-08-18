# 更新日志

本项目所有重要变更均会记录在此文件中。

格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [未发布]

### 变更（Visitors 徽章更名 Visits/day (14d)：alt 文本与 xhqing 集中统计新 label 对齐）

- **为什么改**：用户要求（2026-08-17）访问量徽章名需表达「最近半月日均访问量」口径——xhqing 集中统计侧的 badge JSON label 已从 `Visitors` 改为 `Visits/day (14d)`（`Visits/day` 是 shields.io 表达日均的惯例写法、`(14d)` 标注 14 天滚动窗口），各仓 README 的徽章 alt 文本同步对齐，避免 alt 与徽章实际显示文字脱节。
- **改了什么**：README 徽章区 `alt="Visitors"` → `alt="Visits/day (14d)"`，仅改 alt 文本，endpoint URL、数据源、徽章口径均不变（口径改动记 xhqing 仓库 CHANGELOG，本仓只改 alt）。

### 变更（Visitors 徽章 alt 文本首字母大写：README 访问量徽章命名统一）

- **为什么改**：用户指令（2026-08-16）「Visitors 徽章全局统一，首字母大写」——配合全局 `~/.claude/CLAUDE.md`「徽章英文首字母必须大写」新规，集中统计上线时挂的访问量徽章 `alt="visitors"` 为小写存量，与 badge JSON label（`Visits/day`）及大写规范不一致，本次一次收口。
- **改了什么**：README（EN/CN）徽章区 visitors 徽章 `alt="visitors"` → `alt="Visitors"`，仅改 alt 显示文本，endpoint URL 与数据源不变。

### 新增（README 访问量徽章——舰队集中式访问统计）

- **为什么改**：全舰队上线集中式「真去重」访问统计（图片徽章方案无法去重，走官方 Traffic API 路线）：统计集中部署在 xhqing 仓库（`scripts/update_traffic.py` + 每日 GitHub Action），各 fleet 仓库只需在 README 挂徽章、零运行负担。
- **改了什么**：README（EN/CN）徽章区新增 visitors 徽章（shields.io endpoint 指向 `xhqing/xhqing` 仓库 `traffic/badges/<repo>.json`，由每日采集的官方 Traffic API 数据更新）。徽章数字含义：按日去重访客的累计（GitHub 只提供每日 uniques，跨天不去重），自 2026-08-16 起累计。

### 新增

- 子项目 XPilot 纳入负责范围（2026-08-10）：用户将独立仓库 [xhqing/XPilot](https://github.com/xhqing/XPilot) 交由本项目（Hermes）负责维护，按全局规则「Agent 项目与子项目的 `.claude/` 超集关系」执行：`CLAUDE.md` 新增「子项目清单」节；XPilot 新建 `.claude/CLAUDE.md`（XPilot 项目说明 + 负责工程师 Hermes 节 + 本文件全文随附，带指代说明）；XPilot `.gitignore` 补 `.claude/settings.local.json` 忽略规则（防止本机配置入库）。**为什么**：用户明确将 XPilot 划归 Hermes，需建立超集关系，使用户只操作子项目时也能看到 Agent 完整规则。

### 变更

- 仓库重建（2026-08-09）：XPilot 工具从仓库内子项目拆出为**独立仓库** [xhqing/XPilot](https://github.com/xhqing/XPilot)（工具侧改回独立工具项目、版本 0.5.1，功能不变）；本仓库恢复为纯 Agent 项目，README（中英双语）、`.claude/CLAUDE.md`、`.codebuddy/CODEBUDDY.md` 同步改为指向独立 XPilot 仓库。**为什么**：8-08 的 Agent 化把工具塞进 `XPilot/` 子目录、仓库与目录改名 `NetOpsAgent`，实际使用中发现工具独立成库更合适——Agent 定位（Hermes）保留在本仓库，工具独立演进、互不干扰。
- 项目级配置按 fleet 标准补齐：`.claude/settings.json`（hooks 空，AutoMemory 已全局禁用）、`.claude/settings.local.example.json`（入库模板）+ `.claude/settings.local.json`（本机，已 gitignore）、`.gitignore`（运行时数据 / 密钥 / 本地配置一律忽略）。

### 移除

- 移除与全局重复的通用能力副本：`.claude/skills/anysearch/`、`.claude/skills/find-skill/`、`.claude/rules/`（通用三件套）、`.claude/commands/install-skill.md`；`.gitignore` 同步去掉 find-skill 忽略条目。**为什么**：按全局新规则「通用能力开源单一出口」（2026-08-09 立），新建 Agent 项目不再放置与全局 `~/.claude/` 重复的通用能力——全局通用能力已由 CapabilityManagerAgent（Prometheus）的 `claude/` 镜像一次性开源，各项目不再重复维护副本（副本易过期分叉，本次新建时就发现 anysearch `runtime.conf` 副本与全局不一致、find-skill 副本多出 `.env.example`）。项目只保留独有能力与配置（settings、README、CLAUDE.md 等）。

## [1.0.0] - 2026-08-08

### 新增

- 项目定位为「网络运维管理员 Hermes」Agent 项目：仓库根目录承载 Agent 定位与对外文档（README 中英双语 + LOGO + 徽章 + 版权署名），并注册到全局 fleet 智能体命名注册表（Hermes / NetOpsAgent，独立于销售流水线）。
- XPilot 独立子项目（`XPilot/`）：CLI 工具的代码、配置、测试、Docker 与开发工具链全部迁入 `XPilot/` 子目录，工具自身沿用其独立的 README / CHANGELOG / VERSION / LICENSE；发布工作流（`.github/workflows/release.yml`）在 `XPilot/` 目录内构建并上传 Release 资产。
