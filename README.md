<div align="center">

<img src="docs/labos-banner.jpg" alt="LabOS Banner" width="100%">

# LabOS

**下一代全自动科研实验平台**

覆盖完整研究生命周期：创意生成 · 文献调研 · 假设设计 · 实验执行 · 论文撰写

本地优先 · 多模型支持 · 完全开源

[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg)](./LICENSE)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-3776AB.svg?logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688.svg?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![SQLite](https://img.shields.io/badge/SQLite-003B57.svg?logo=sqlite&logoColor=white)](https://sqlite.org)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

[English](./README.en.md) · [快速开始](#快速开始) · [功能截图](#功能截图) · [贡献指南](./CONTRIBUTING.md) · [路线图](https://github.com/YUANXICHE98/LabOS/issues)

</div>

---

> **✦ 核心能力**
>
> **研究流水线** · 四阶段自动化 &nbsp;│&nbsp; **AI 对话** · 多模型流式对话 &nbsp;│&nbsp; **实验执行** · SSH 远程 GPU 服务器 &nbsp;│&nbsp; **Codex 集成** · AI 自动写实验代码
>
> **记忆系统** · 跨实验知识持久化 &nbsp;│&nbsp; **多模型配置** · 通用 / 代码 / 论文 / 实验 独立配置 &nbsp;│&nbsp; **阶段报告** · 调研→分析→实验 &nbsp;│&nbsp; **本地优先** · 数据全在你手里

---

## 演示视频

<div align="center">

[🎬 **点击观看 LabOS 演示视频（4分钟中文讲解）**](https://github.com/YUANXICHE98/LabOS/releases/download/v3.4.1/labos-demo-zh.mp4)

> 也可以在 [Releases 页面](https://github.com/YUANXICHE98/LabOS/releases/tag/v3.4.1) 直接下载观看

</div>

## 功能截图

<details open>
<summary><strong>📊 概览面板</strong> — 快速了解项目概况，一键导航到对话、项目或新建实验</summary>
<br>
<div align="center">
<img src="docs/screenshots/screenshot-dashboard.png" width="800" alt="LabOS Dashboard">
</div>
</details>

<details open>
<summary><strong>📁 项目管理</strong> — 多项目管理，每个项目关联独立的实验、记忆和论文库</summary>
<br>
<div align="center">
<img src="docs/screenshots/screenshot-projects.jpg" width="800" alt="LabOS Projects">
</div>
</details>

<details open>
<summary><strong>🧪 实验流水线</strong> — 四阶段流水线运行状态、阶段审批、实验日志</summary>
<br>
<div align="center">
<img src="docs/screenshots/screenshot-experiment.jpg" width="800" alt="LabOS Experiment Pipeline">
</div>
</details>

## 特性

| 功能 | 描述 |
|:-----|:-----|
| 🔬 **四阶段研究流水线** | 创意生成 → 方案设计 → 实验执行 → 论文撰写，每阶段生成独立报告 |
| 💬 **对话驱动** | AI 助手流式对话，支持从对话直接创建项目 |
| 🤖 **多 LLM 配置档** | 为通用对话、代码分析、论文撰写、实验设计分别配置不同模型和 API |
| 🖥️ **远程实验执行** | SSH 连接 GPU 服务器（AutoDL 等），实时日志流推送 |
| ⚡ **Codex CLI 集成** | full-auto 模式，JSONL 实时流式输出，自动写实验代码 |
| 🧠 **记忆系统** | 跨实验知识持久化，项目级记忆检索 |
| ✅ **阶段审批** | 批准 → 下一阶段 / 修改重跑 / 拒绝终止 |
| ⚙️ **完全可配置** | 所有设置通过 Web UI 暴露，支持任意 OpenAI 兼容 API |
| 💾 **本地优先** | SQLite 存储，所有数据在你本地 |

## 快速开始

```bash
git clone https://github.com/YUANXICHE98/LabOS.git
cd LabOS
bash start.sh
```

或手动启动：

```bash
pip install -r requirements.txt
cd src && python api_server.py
```

打开浏览器访问 `http://localhost:8000`

### 首次配置

1. 进入 **设置** → 配置你的 LLM API 端点和密钥（支持任意 OpenAI 兼容 API）
2. （可选）配置 SSH 服务器信息，用于远程实验执行
3. 进入 **对话** → 开始聊天 → 从对话创建项目
4. 或进入 **项目** → 手动创建项目 → 启动实验

### 多 LLM 配置

LabOS 支持为不同任务类型配置独立的 LLM：

| 任务类型 | 用途 | 推荐模型 |
|:---------|:-----|:---------|
| 通用对话 | 日常研究讨论 | DeepSeek-Chat / GPT-4o |
| 代码分析 | 代码审查、实验代码生成 | DeepSeek-Coder / Claude |
| 论文分析 | 文献综述、论文撰写 | GPT-4o / Claude |
| 实验设计 | 假设生成、实验方案 | DeepSeek-Chat / Claude |

通过 **设置 > LLM 配置档** 配置，每个任务类型可以设置独立的 Base URL + API Key + 模型名。

## 项目结构

```
LabOS/
├── src/
│   ├── api_server.py      # FastAPI 后端 — 所有 API 端点和流水线逻辑
│   ├── index.html          # 主页面（单页应用）
│   ├── app.js              # 前端 — UI 逻辑、API 调用、SSE 实时流
│   └── style.css           # 样式
├── docs/
│   ├── screenshots/        # 截图
│   └── videos/             # 演示视频
├── start.sh                # 一键启动脚本
├── requirements.txt        # Python 依赖
├── CONTRIBUTING.md         # 贡献指南
├── GOVERNANCE.md           # 贡献者治理与激励制度
└── LICENSE                 # AGPL-3.0
```

## 技术栈

| 层 | 技术 |
|:---|:-----|
| 后端 | Python / FastAPI / uvicorn |
| 数据库 | SQLite（零配置，本地文件） |
| 前端 | 原生 HTML + CSS + JavaScript（无构建步骤） |
| 远程执行 | Paramiko（SSH） |
| LLM 调用 | httpx（OpenAI 兼容协议） |
| 实时通信 | Server-Sent Events (SSE) |

## Open Core 模式

LabOS 采用 **开源核心 + 付费增值** 模式：

### 🆓 免费开源（本仓库）
本仓库所有代码永久免费开源：完整研究流水线、对话、项目管理、LLM 配置、记忆系统、实验执行。

### 💎 付费增值（即将推出）
- **Skill Library** — 经过验证的研究方法论、实验路径、最佳实践。可以理解为"哪条路走得通"的知识库
- **高级集成** — 更多云 GPU 平台、HPC 集群的预置连接器
- **优先支持** — 直接对接开发团队

> 平台本身永远开源。真正的价值在于**经过验证的研究方法论**——节省数周试错时间的成熟路径。

## 贡献者激励

我们重视每一份贡献。详见 **[GOVERNANCE.md](./GOVERNANCE.md)**

| 等级 | 条件 | 激励 |
|:-----|:-----|:-----|
| 🌱 贡献者 | 1 个 PR 合并 | Contributors Wall 署名 |
| 🌿 活跃贡献者 | 3+ PR | 免费 Skill Library 访问 + Beta 早期体验 |
| 🌳 核心贡献者 | 10+ PR 或 1 个大功能 | **30% 收益分成** + 论文共同作者 |
| 💰 悬赏任务 | `💰 bounty` 标签 | 加密货币 / Sponsors 现金奖励 |

代码不是唯一的贡献方式——文档、翻译、Bug 报告、研究方法论、设计都同等计算。

欢迎 PR！详见 [CONTRIBUTING.md](./CONTRIBUTING.md)，浏览 [Issues](https://github.com/YUANXICHE98/LabOS/issues) 找到你感兴趣的任务。

## 支持项目

<div align="center">

⭐ **Star 本仓库** — 帮助更多人发现 LabOS &nbsp;│&nbsp; 🍴 **Fork & 贡献** — 代码、文档、翻译 &nbsp;│&nbsp; 💰 **赞助** — 帮助持续开发

</div>

### 加密货币

| 链 | 地址 |
|:---|:-----|
| **ETH / ERC-20** (USDT, USDC 等) | `0xc6B4720835E6C3CB58618B4df26B64F595C30202` |

### 支付宝

<div align="center">
<img src="docs/alipay-qr.jpg" width="250" alt="支付宝收款码">
</div>

### GitHub Sponsors

点击仓库顶部的 **「Sponsor」** 按钮支持本项目。

---

<div align="center">

## Contributors

<a href="https://github.com/YUANXICHE98/LabOS/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=YUANXICHE98/LabOS" />
</a>

---

**[AGPL-3.0](./LICENSE)** — 修改后必须开源，网络服务必须提供源码，衍生作品须引用上游仓库。

Made with ❤️ for the research community

</div>
