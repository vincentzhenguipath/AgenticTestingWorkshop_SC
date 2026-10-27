# UiPath 智能体测试与编码智能体 — 站点

> 本仓库（AgenticTestingWorkshop_SC）是 [AgenticTestingWorkshop](https://github.com/madapopescu24/AgenticTestingWorkshop)（英文原版）的简体中文版，发布后的站点地址为 https://vincentzhenguipath.github.io/AgenticTestingWorkshop_SC/。

这是一门面向客户和合作伙伴的动手实践课程，讲授如何借助编码智能体（Claude Code）和 `uip` CLI（命令行）进行 UiPath 智能体测试（Agentic Testing）：在 Test Manager 中规划测试用例，在 Studio 中实现自动化，执行测试并生成报告。课程场景基于 UiBank 测试用例设计文档 E2E UiBank Online Banking，它会转化为八个需求和八个相互独立的测试用例。

本站基于与 [Agentic Practice Workshop](https://github.com/uipath-practice/AgenticPracticeCourse) 相同的 MkDocs 框架构建，并新增了三项内容：一个私有知识库、一个可配置的培训环境，以及在截图路径之外的一条由 CLI/知识库驱动的课程生成路径。

## 工作原理

```
../knowledge-base/  (private SSOT, NOT in this repo)
        ↓  used as context to generate accurate lessons
docs/*.md  →  MkDocs builds HTML  →  GitHub Actions  →  gh-pages  →  GitHub Pages
```

| 路径 | 用途 |
|------|---------|
| `docs/` | 发布的页面内容 — 每个页面一个 `.md` |
| `mkdocs.yml` | 站点配置 + **已发布**的导航 |
| `mkdocs.local.yml` | 仅限本地的导航，包含进行中的内容（已加入 gitignore） |
| `main.py` | 用于培训提示框的环境变量（staging 与 prod） |
| `Master/` | 编写规则与模板（复制自基础框架） |
| `.claude/commands/` | 编写用的斜杠命令（复制自基础框架） |
| `hooks/`, `scripts/` | 双栏钩子；截图元数据流水线（复制而来） |
| `.github/workflows/deploy.yml` | 推送到 `main` 时自动部署到 GitHub Pages |

知识库被有意放在**这个公开仓库之外**（`../knowledge-base/`），以确保内部资料永远不会被发布。

## 首次设置

```bash
# 1. 从基础仓库拉取可复用的框架文件
./bootstrap-framework.sh

# 2. 安装依赖
pip install -r requirements.txt

# 3. 本地预览（编写环境 + 进行中的导航）
COURSE_ENV=staging mkdocs serve -f mkdocs.local.yml
# 打开 http://127.0.0.1:8000

# 4. 与正式发布等效的构建检查（CI 部署 staging 配置）
COURSE_ENV=staging mkdocs build
```

## 发布到 GitHub

本仓库是在本地搭建的。要创建远程仓库并部署：

```bash
cd AgenticTestingWorkshop
git init && git add . && git commit -m "Initial scaffold"
gh repo create madapopescu24/AgenticTestingWorkshop --public --source=. --push
# 然后在 gh-pages 分支上启用 GitHub Pages（该分支由部署工作流创建）
```

## 讲师备注（内部）

本节仅供讲师/引导者使用。它保留在这个 README 中而不是 `docs/` 里，因为 GitHub Pages 无法按邮箱限制访问——任何仅限管理员的内容都必须放在仓库本身，而不是公开站点上。请勿将本节内容移入 `docs/`，也不要在 `mkdocs.yml`/`mkdocs.local.yml` 中引用它。

### 环境与租户设置

站点的 `main.py` 定义了一个 `COURSE_ENV` 开关，包含两个配置（`staging` 和 `prod`），用于驱动课程中随处使用的 `{{ training_url }}`、`{{ training_org }}`、`{{ training_tenant }}` 和 `{{ training_folder }}` 宏。**工作坊在 staging 上运行**：它所展示的 Autopilot for Testers 和 Autopilot for Developers 最新功能只在那里可用。CI 使用 `COURSE_ENV=staging` 部署，这也是默认值。

| 配置 | 组织 | URL | 租户 | 用途 |
|---|---|---|---|---|
| `staging` | `partnersuccess` | https://staging.uipath.com/partnersuccess | `MadalinaTest` | **学员环境。** Studio、`uip` CLI、Test Manager 和 Orchestrator 都指向这里。 |
| `prod` | `tpenlabs` | https://cloud.uipath.com/tpenlabs | `AgenticTesting` | 课程中不使用。留待 Autopilot 功能上线 Automation Cloud 时使用。 |

已确认：staging 上的 `partnersuccess` / `MadalinaTest` 已启用 Test Manager、Autopilot for Testers 和 Autopilot for Developers。如需在其他租户上开展课程，请修改 `main.py` 中 `staging` 配置的 `training_tenant`（必要时还有 `training_org`）。

所有练习都在 staging 上的同一个共享 Orchestrator 文件夹中进行。该租户的 Test Manager 地址为
`https://staging.uipath.com/partnersuccess/MadalinaTest/testmanager_`。

- **文件夹名称：** `AgenticTesting`（即 `main.py` 中的 `training_folder` 宏）。它是每位学员 Test Manager 项目的默认 Orchestrator 文件夹，存放测试包和凭据资产。
- **文件夹密钥：** _TODO — 在 staging 上创建或确认 `AgenticTesting` 文件夹，并在此记录其密钥。_

每个可部署的产物（测试包、凭据资产、Test Manager 项目）都以 `{YourName}` 为前缀命名（例如 `{YourName}UiBankTests`），这样共享同一租户/文件夹的学员就不会与彼此的包、流程或 Orchestrator 实体发生冲突。

### 邀请学员

每期课程开始前，邀请每位学员加入 staging 组织（`staging.uipath.com` 上的 `partnersuccess`），以便他们用自己的邮箱登录：

1. 在 staging 组织中，进入 **Admin**（管理）选项卡。
2. 进入 **Accounts and Local Groups**（账户和本地组）。
3. 使用每位学员的邮箱地址邀请他们。
4. 确保每位受邀学员都被加入 **CodingAgentsGroup** 本地组（如果 staging 上没有，就创建一个）——正是这个组授予他们对 `MadalinaTest` 租户、Test Manager 和 `AgenticTesting` 文件夹的访问权限。

### 每次培训前

智能体测试课程（约 8 小时）只有在开始前平台前提条件全部就绪时才能顺利进行：

- [ ] 在 **AgenticTesting** 文件夹中构建并发布备用测试包 `DemoUiBankTests`。它的测试入口点 `T0_LoginAndInitialAccountState` 到 `T7_LogoutAndEvidenceCollection` 分别自动化了八个测试用例，每个对应一个，并且以任意顺序都能通过。在测试用例环节中自己的自动化没做好的学员，可以在测试集环节把它关联到自己的测试用例上。
- [ ] 在该文件夹中为演示包的 UiBank 用户创建凭据资产，并完整演练一遍：把 `DemoUiBankTests` 关联到某个 Test Manager 测试用例，以自动化方式运行它的测试集，并检查截图是否到位。
- [ ] 确保 **AgenticTesting** 文件夹中有可用的、能运行 Chrome 浏览器自动化的**无人值守机器人**——自动化测试集以及每位学员的 **Run Autonomously**（自主运行）执行都在那里运行。Serverless（"Default Serverless" 模板没有运行时槽位）和学员个人工作区的机器人都不会接手这些作业：它们会一直停留在 Pending，且不报错。在机器人可用之前就进入 Pending 的作业，要停止后重新运行。请规划足够的容量，让整个小组能在同一个 10 分钟内运行各自的自主执行和测试集。这是测试集环节最可能出现的瓶颈。
- [ ] 确认 staging 租户已为小组中的每个人启用 **Autopilot**：Studio 中的 Autopilot 面板（动手实践部分一开始就用它生成需求，之后又用它创建测试集）、Test Explorer 中的 **Generate Test Case with Autopilot**（使用 Autopilot 生成测试用例）、Test Manager 中的 Evaluation Agent、Test Case Generation、Prompt Library、**Run Autonomously** 和 Generate Insights，以及 Studio 表达式编辑器中的 Fix / generate。演练一次需求提示词，检查它是否生成了以步骤命名的八个需求。端到端地自主运行一个测试用例，并检查实时画面和逐步截图对学员是否正常。
- [ ] 确认 **CodingAgentsGroup** 可以创建 Test Manager 项目（动手实践的环境准备环节会为每位学员创建一个）、创建凭据资产，并在该文件夹中上传包。
- [ ] 检查学员能否让 Studio 登录到 `staging.uipath.com`。Studio 登录到了 Automation Cloud，是环境准备环节最常见的失败原因。
- [ ] 设计文档以 `docs/resources.assets/E2E UiBank Online Banking.docx` 的形式发布在站点上（动手实践页面和资源页面上有下载按钮）。这是一份清理过的副本：已删除来自其他项目的残留图片、作者元数据，以及一个真实的用户名/邮箱。如果你更新了原始文档，替换前请用同样的方式清理。
- [ ] 至少提前两天发送[环境准备](docs/setup.md)页面，包括 UiBank 注册和凭据资产。环境准备不计入 8 小时。请 Mac 用户从 Login 测试用例开始与一位 Windows 用户结对。

### TODO — 下一期课程前补充

- [ ] 两期课程之间是否需要重置/清理步骤（上一期遗留的 Test Manager 项目、包、凭据资产、执行）？请在此记录步骤或脚本。
- [ ] UiBank 的数据随时可能被重置。学员是否需要在每期课程前重新注册？
- [ ] 如果学员在工作坊中途需要重新发放凭据/租户访问权限，应该联系谁？

### 时间与议程

课程持续**约 8 小时**（9:00–17:00），需求环节之后有 15 分钟休息，测试用例环节中间有 45 分钟午餐（12:30），执行环节之前有 10 分钟休息。最后是 SAP 测试、问答和反馈。时间安排是大致的：工作坊期间可以灵活调整，休息时间也一样。没有课后作业。面向学员的日程在议程页面上；以下是讲师视角：

| 时间 | 议程项 | 讲师重点 |
|---|---|---|
| 0:00–0:30 | 欢迎 | 自我介绍和当天的计划 |
| 0:30–1:45 | 1. 介绍 + 理论部分 | 讲解*智能体测试与编码智能体*：Test Cloud、Autopilot for Testers、Autopilot for Developers、编码智能体；各自适用的场景。检查每个人的 Studio 都已登录到 staging。 |
| 1:45–2:00 | 环境准备 | 每个人创建一个 Test Manager 项目（名称 `{YourName}_UIB_Test`，前缀 `UIB`）并设置其默认文件夹，然后创建 Studio 测试自动化项目，再将两者连接；继续之前检查每个人都能打开 Autopilot 面板 |
| 2:00–2:15 | Studio 中的 Autopilot 创建需求 | 先在屏幕上演示提示词；检查每个人都得到以步骤命名的八个需求 |
| 2:15–2:25 | 讨论需求 | 可追溯性、可测试性、遗漏之处；Autopilot 有没有凭空编造规则？ |
| 2:25–2:45 | 评估、改进、再评估 | 在大家动手之前，先用一个需求演示 Evaluation Agent |
| 2:45–3:00 | 休息 | |
| 3:00–3:30 | Test Manager 中的 Autopilot 创建测试用例 | Login 需求；展示 Prompt Library |
| 3:30–4:15 | 午餐 | 帮助还在创建测试用例的落后学员 |
| 4:15–4:45 | 手动实现 Login 测试用例 | 讲解 Given / When / Then；确保目标元素都放进对象存储库 |
| 4:45–5:15 | Studio 中的 Autopilot / Codex 生成测试用例 | 把学员分成 Autopilot 组和编码智能体组；最后对比结果 |
| 5:15–5:30 | 自主运行 | 每个人自主运行一个登录反向测试用例；指出实时画面和逐步截图 |
| 5:30–6:05 | 再实现几个测试用例 | 引导大家关注 *Given* 列：转账和查询会自行准备数据 |
| 6:05–6:15 | 休息 | |
| 6:15–6:25 | 执行选项卡 | 每个人探索自己的执行：自主运行、其测试用例日志以及截图 |
| 6:25–6:35 | 测试集 | 每个人先把测试项目发布到 Orchestrator Tenant Process Feed；然后由 Autopilot 创建冒烟 + 回归测试集；运行；留意机器人容量；Generate Insights |
| 6:35–6:45 | 后续步骤 | *你构建了什么*、*常见问题* |
| 6:45–7:45 | SAP 测试 | |
| 7:45–7:55 | 问答 | |
| 7:55–8:00 | 反馈 | |

之前的招聘流水线课程（Coded Agent → RPA → Maestro Flow）已在本地归档到 `Archive/recruitment-pipeline/` 下。

**控时规则：** 某个步骤的时间一到，就带着已有的成果继续往下走。进度落后的学员在测试集环节关联 `DemoUiBankTests`，照样可以运行测试集并查看其执行。

### 参考答案 / 预期输出

_尚未记录 — 请在此添加参考解答 / 预期结果。_
