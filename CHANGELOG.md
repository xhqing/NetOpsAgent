# 更新日志

本项目所有重要变更均会记录在此文件中。

格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [1.0.2] - 2026-10-17

### 变更（Agent 进驻子项目：新增项目级 `.pi/`，子项目清单节同步 2026-10-17 新规）

- **为什么改**：用户 2026-10-17 修订全局规则（细则见 `~/.claude/docs/agents-registry.md`「智能体专属文件归属与子项目映射」节，取代 2026-10-12 的「子项目一律不得存在」）：智能体专属文件的**实体只在 Agent 项目**；子项目根目录挂 `AGENTS.md → ../NetOpsAgent/AGENTS.md`、`.pi → ../NetOpsAgent/.pi` 两条相对路径软链接（随仓库提交），在子项目目录直接开会话即继承 Hermes 的身份 / 规则 / 技能；后台开启 / 唤醒会话（intercom / `agent_call` / `agent_wake`）仍只以 Agent 项目根目录为工作目录。
- **改了什么**：① 新建项目级 `.pi/` 目录（含 `.gitkeep`，作为子项目 `.pi` 软链接的目标）；② `CLAUDE.md`「子项目清单」节按新规更新（实体只在 Agent 项目 + 子项目挂两条指回软链接 + 后台会话仍限本项目根目录）；③ 子项目 XPilot 已挂两条软链接（子项目侧改动记 XPilot 仓 CHANGELOG 与提交）。

## [1.0.1] - 2026-10-12

### 变更（子项目清单表述随全局新规重写：智能体专属文件只属于 Agent 项目）

- **为什么改**：用户 2026-10-12 修订全局规则（细则见 `~/.claude/docs/agents-registry.md`「智能体专属文件归属与子项目映射」节，取代 2026-08-10 立的「子项目 `.claude/` 超集」规则）：`CLAUDE.md` / `AGENTS.md` / `.claude/` / 项目级 `.pi/` 等智能体专属文件只有 Agent 项目允许拥有，非 Agent 项目（含子项目）一律不得存在；后台开启 pi 会话（intercom / `agent_call` / `agent_wake`）只能以 Agent 项目根目录为工作目录。随本规则落地，子项目 XPilot 的存量智能体专属文件（根 `CLAUDE.md` + `.claude/CLAUDE.md`）一并清理（子项目侧改动记 XPilot 仓 CHANGELOG）。
- **改了什么**：`CLAUDE.md`「子项目清单」节重写——删除「权威源 / 超集 / 全文随附进子项目」旧表述，改为新规表述（子项目不携带智能体专属文件、子项目工作在本项目会话里按路径操作、后台会话以本项目根目录为工作目录、引用全局 agents-registry 新节）；仅改表述与流程说明，本仓文件结构与其余内容不变。
### 变更（assets/logo.svg 注释去中文）

- **为什么改**：全局规则新增「Logo / 图标资产文字一律用英文」（2026-09-12 用户立，起因 Swing 仓库 logo 副标题混入中文被指出）：logo 是面向全球读者的视觉标识，中文受众已有 README_cn.md 双语通道；且 SVG 中文依赖查看环境的字体回退，渲染不可控。本次为按新规批量清理存量。
- **改了什么**：`assets/logo.svg` 内部注释「网络运维图标：中心节点 + 雷达扫描弧 + 分布式节点」改为英文注释（渲染文字本就是英文，仅清注释；按新规使文件内中文归零，grep 自检干净）。

### 变更（项目指令文件迁至仓库根：`CLAUDE.md` + `AGENTS.md` / `CODEBUDDY.md` 软链接）

- **为什么改**：对齐团队脚手架现行标准——角色化 `CLAUDE.md` 直接放项目根目录、不再建 `.claude/` 目录（通用能力经全局 `~/.claude/` 与 CapabilityManagerAgent 镜像统一分发，项目内不留副本）；`AGENTS.md`（ZCode 等工具入口）与 `CODEBUDDY.md`（CodeBuddy 入口）以相对软链接指向根 `CLAUDE.md`，单一来源、内容天然同步。
- **改了什么**：① 项目指令文件从 `.claude/CLAUDE.md` 迁至根目录 `CLAUDE.md`（迁移时内容逐字不变），删除 `.claude/` 目录；② 新增根目录软链接 `CODEBUDDY.md` → `CLAUDE.md`，删除 `.codebuddy/` 目录；③ `AGENTS.md` 软链接目标由 `.claude/CLAUDE.md` 改为 `CLAUDE.md`（原目标随迁移失效，修正后不再悬空）；④ 迁后按新布局更新 `CLAUDE.md`「目录结构」节（原 `.claude/`、`.codebuddy/CODEBUDDY.md` 两条描述已过时）。

### 新增（根目录软链接 `AGENTS.md` → `.claude/CLAUDE.md`）

- **为什么改**：ZCode 等新一代 agent 工具读取项目级指令的入口文件名是 `AGENTS.md`（不是 `CLAUDE.md`），不建入口则这类工具会话中加载不到本项目指令；建软链接指向 `.claude/CLAUDE.md`，单一源维护、两种文件名约定都能读到，无需双份同步。
- **改了什么**：项目根新增软链接 `AGENTS.md`，用相对路径指向 `.claude/CLAUDE.md`（相对路径保证仓库移动或 clone 后链接依然有效）；`.claude/CLAUDE.md` 本身无任何改动。

### 变更（措辞统一 fleet → team：`.claude/CLAUDE.md` + `.commit-cache.md` 跟随全局统一）

- **为什么改**：用户 2026-08-16 已把 xhqing 主页 README 的自称从「舰队 / fleet」改为「团队 / team」，本仓 `.claude/CLAUDE.md`（含同步到子项目 XPilot 的超集内容）与 `.commit-cache.md` 缓存标记仍是 fleet 旧措辞；2026-08-21 用户裁定全量存量一次清零、统一为团队 / team。
- **改了什么**：`.claude/CLAUDE.md` 2 处（「fleet 项目名」→「团队项目名」、「README 人格与 fleet 注册表」→「团队注册表」）并按超集关系同步 XPilot `.claude/CLAUDE.md`（diff 验证超集一致）；`.commit-cache.md` 2 处缓存标记「fleet 例外 / fleet Visitors 徽章」→「团队」。仅改措辞，职责、徽章、结构均不变。

### 变更（README 徽章组合对齐 fleet 新标准：补 Version 徽章、移除 Last Commit 动态徽章）

- **为什么改**：`/commit` 第 9l 步检测（2026-08-18）发现两版 README 仍含 `github/last-commit/` 动态徽章——按 2026-08-16 fleet 徽章新标准（License / Version / Type 三枚必须含有、不含 GitHub 动态数值 / 时间徽章），Last Commit 属须移除的违规徽章；且本项目从未挂过 Version 徽章（缓存 2026-08-08 写入时还是旧标准「License / Last Commit / Type」，Version 一直是缺项）。
- **改了什么**：README（EN/CN）徽章区移除 Last Commit 动态徽章、新增 Version-1.0.0 静态徽章（版本号取 `VERSION` 文件），Visitors 访问量徽章（fleet 允许例外）保留不动。

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
