<div align="center">
  <img src="assets/logo.svg" alt="NetOpsAgent logo" width="380">

  <p>
    <a href="LICENSE.md"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
    <img src="https://img.shields.io/badge/Version-1.0.2-blue.svg" alt="Version: 1.0.2">
    <img src="https://img.shields.io/badge/Type-AI%20Agent-blueviolet" alt="Type: AI Agent">
  <img src="https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/xhqing/xhqing/main/traffic/badges/NetOpsAgent.json" alt="Visits/day (14d)" />
  </p>

  <p>
    <a href="README.md">English</a>
    &nbsp;|&nbsp;
    简体中文
  </p>
</div>

## 🛰️ Hermes —— 网络运维管理员 Agent

**Hermes（赫尔墨斯）** 是本项目的**网络运维管理员 Agent**。名字取自希腊神话中掌管道路、路口与信使的神——Hermes 的总体职责是处理**网络连接相关的问题**：保障你对外的连接稳定、快速，排查并修复各种挡路的网络故障。**代理转发只是众多网络问题中的一部分**，同样的思路也适用于任何你不想手动盯着的网络问题。

当前 Hermes 具备以下能力：

- **真实流量节点检测**——逐个节点起临时实例走真实流量，验证节点是否真能代理流量，而不只是 TCP 能否连上服务器（能揪出密钥失效、协议握手失败、对端无法出网这类常见故障）。
- **智能节点选优**——按延迟与带宽在可用节点里选最快的，提供三种策略：纯延迟、纯带宽、带宽为主延迟兜底的混合策略。
- **自动故障转移**——当前节点变差时立即切到更优节点；全部节点都不通时自动刷新订阅后重试。
- **灵活路由**——让指定域名（GitHub、OpenAI、Google 等）走指定节点，其余走默认节点。

## 项目结构

本仓库是 **Hermes Agent 项目**——Agent 的身份、能力与运营手册所在。工具本体在**独立仓库**中：

| 仓库 | 用途 |
|------|------|
| [xhqing/XPilot](https://github.com/xhqing/XPilot) | **XPilot** CLI 工具——一个方便使用 [Xray-core](https://github.com/XTLS/Xray-core) 的 Python CLI，通过 `xpilot` 命令调用。Hermes 的全部代理能力都由它实现。 |

## 快速开始

工具本体及其全部文档都在独立的 **XPilot** 仓库：

- **安装与使用**：见 [XPilot/README.md](https://github.com/xhqing/XPilot)
- **中文安装与使用文档**：[XPilot/README_cn.md](https://github.com/xhqing/XPilot/blob/main/README_cn.md)

```bash
git clone https://github.com/xhqing/XPilot.git
cd XPilot
pip install -e .
xpilot --help
```

你可以自己执行命令，也可以交给 AI 助手——无论哪种方式，干活的都是 Hermes。

---

## 版权与署名

本项目基于 [MIT 协议](LICENSE.md) 开源。

Copyright (c) 2026 All Contributors。

### 署名方式

如果你复用或再分发本项目的任何部分，请：

- 保留上方版权声明与 MIT 协议文本。
- 通过链接回项目原始来源的方式注明出处。

**项目地址：** [https://github.com/xhqing/NetOpsAgent](https://github.com/xhqing/NetOpsAgent)
