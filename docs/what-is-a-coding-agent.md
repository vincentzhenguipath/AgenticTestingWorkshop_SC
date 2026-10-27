简介 + 理论知识
{: .eyebrow }

# 🤝 智能体测试与编码智能体 { #agentic-testing-coding-agents }
了解用 UiPath Test Cloud 做测试是什么样子，智能体测试（Agentic Testing）又带来了什么，编码智能体如何工作，以及两者在你的测试生命周期中如何交汇。

## 🧪 测试与 UiPath Test Cloud { #testing-and-uipath-test-cloud }

### 🔬 测试速览 { #testing-in-a-nutshell }

测试是一种调查活动，目的是向相关方提供被测产品的质量信息。测试分为四个层级：

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**单元测试**

针对系统中的单个单元，确认每个单元的代码都按预期运行。由开发人员编写并执行。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**集成测试**

把多个单元组合起来作为一个整体测试，找出它们交互时的问题

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**系统测试 / 端到端测试**

针对完整集成后的系统，按照端到端规格进行验证

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**验收测试**

对照业务需求检验系统，判断它是否可以交付

</div>
</div>

</div>

UiPath Test Cloud 最能发挥价值的是中间这两层：**集成测试**和**端到端测试**，而本次课程中的 UiBank 测试用例正是这一类。另外还有两个概念，你今天会反复用到：

- **黑盒测试。** 应用测试从外部检查软件是否满足需求，只看输入和预期输出，不接触代码。每个 UiBank 测试都是这样进行的。
- **尽早测试。** 在测试阶段发现缺陷，成本远低于上线后再紧急修复。自动化并不会取代人：它接手那些重复性的检查，让测试人员可以专注于探索性测试和可用性测试。

### ☁️ UiPath Test Cloud 是什么 { #what-uipath-test-cloud-is }

**UiPath Test Cloud** 是 UiPath 面向应用测试人员的产品：它是 Automation Cloud 中专注于应用测试的专属界面，支持云端和本地部署。

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">📋</span>
<span class="f-title" markdown="span">Test Manager</span>

规划、执行、管理和分析测试：需求、测试用例、测试集、执行、结果

</div>

<div class="feature" markdown>
<span class="f-icon">🛠️</span>
<span class="f-title" markdown="span">Studio</span>

用可视化设计器或代码构建自动化测试用例

</div>

<div class="feature" markdown>
<span class="f-icon">⚙️</span>
<span class="f-title" markdown="span">Orchestrator</span>

在机器人上大规模执行和管理测试自动化

</div>

<div class="feature" markdown>
<span class="f-icon">✨</span>
<span class="f-title" markdown="span">Agentic Testing</span>

加速测试设计与执行的 AI 智能体：Autopilot for Testers，以及你自己构建的智能体

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">Agent Builder</span>

用来构建这些自定义智能体。包含在 App Tester 许可证中

</div>

</div>

### 🧱 Test Manager 中的基本构件 { #the-building-blocks-in-test-manager }

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">📁</span>
<span class="f-title" markdown="span">项目</span>

下面所有对象的容器

💡 每个对象的键都以项目的**前缀**开头，例如 `UIB:1`。项目在 Orchestrator 中的**默认文件夹**就是自动化执行和自主执行运行的地方。

</div>

<div class="feature" markdown>
<span class="f-icon">📋</span>
<span class="f-title" markdown="span">需求</span>

应用必须做什么，以及对应的验收标准

💡 需求也可以来自 **Jira**、**ServiceNow** 或 **Redmine**

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">测试用例</span>

包含手动步骤的场景，关联到它所覆盖的需求

💡 它可以关联到 Studio 中的自动化，也可以由 Autopilot 自主执行

</div>

<div class="feature" markdown>
<span class="f-icon">📦</span>
<span class="f-title" markdown="span">测试集</span>

一起执行的一组测试用例

💡 测试用例可以**静态**分配（手动挑选）或**动态**分配（按标签）。只有静态分配的测试用例才能强制指定执行顺序。

</div>

<div class="feature" markdown>
<span class="f-icon">▶️</span>
<span class="f-title" markdown="span">执行</span>

测试用例或测试集的一次运行

💡 分为**手动**、**自动化**、**自主**或**待执行（Pending）**，每个测试用例都有各自的日志、结果和证据。详见[执行](executions.md)。

</div>

</div>

它们之间的关联就是 Test Manager 所说的**可追溯性**：从一条需求出发，你可以看到哪些测试用例覆盖了它，以及这些测试用例在最近一次运行中的表现。

### 🛠️ Studio 中的测试自动化项目 { #test-automation-projects-in-studio }

**测试自动化项目**是 Studio 中专门用于应用测试的项目类型。只有拥有 **App Tester Developer** 许可证的用户才能创建和发布这类项目。

- **测试用例与数据驱动测试用例。** 一个项目可以包含多个测试用例。数据驱动测试用例会针对测试数据的每一行各运行一次。
- **Given / When / Then。** 每个测试用例都由三部分组成：准备、操作、验证。验证放在 **Then** 中。
- **内置测试活动。** **Verify Expression**（验证表达式）、**Verify Expression With Operator**（使用运算符验证表达式）和 **Verify Control Attribute**（验证控件属性）用于检查预期结果，并且可以为每个结果附上截图。
- **对象存储库。** 从应用中捕获的 UI 目标，由项目中所有测试用例共享。
- **Test Explorer。** 在构建过程中运行和调试测试用例。它的结果只在当前 Studio 会话中保留。
- **VB 或 C#。** 两种表达式语言都支持，测试用例也可以直接用代码编写。
- **发布。** 将项目发布到 **Orchestrator Tenant Process Feed**（Orchestrator 租户流程源）后，会在 Orchestrator 中创建对应的流程。Test Manager 运行的是最新发布的版本。

### 🎫 许可证 { #licenses }

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🎫</span>
<span class="f-title" markdown="span">App Tester</span>

手动测试、测试管理，以及运行（而非构建）自动化。包含 Agent Builder。

</div>

<div class="feature" markdown>
<span class="f-icon">👩‍💻</span>
<span class="f-title" markdown="span">App Tester Developer</span>

构建自动化测试用例，以及测试自动化（包括智能体）

</div>

<div class="feature" markdown>
<span class="f-icon">🤖</span>
<span class="f-title" markdown="span">App Test Robot</span>

在机器人上以无人值守方式运行自动化测试

</div>

</div>

### 🔌 Test Cloud 的集成对象 { #where-test-cloud-connects }

- **需求：** 通过 **Test Manager Connect** 对接 Jira、ServiceNow、Redmine 及其他 ALM 工具，保持测试与需求之间的可追溯性。
- **版本控制：** 通过 Studio 对接 Git 和 TFS。
- **CI/CD：** 对接 Jenkins、Azure DevOps 和 GitHub Actions，让测试集成为流水线的一部分。

## ✨ UiPath Test Cloud 中的智能体测试 { #agentic-testing-in-uipath-test-cloud }

**UiPath Test Cloud** 覆盖整个测试生命周期：你在 **Test Manager** 中规划和设计测试，在 **Studio** 中实现自动化，再通过 **Orchestrator** 大规模运行。智能体测试在每一个环节都加入了 AI 智能体。它们是测试人员能力的延伸，而不是替代。

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**规划 <span class="pill">Test Manager</span>**

需求、包含手动步骤的测试用例、测试集

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**自动化 <span class="pill">Studio</span>**

测试自动化项目、Given / When / Then 测试用例、对象存储库

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**执行 <span class="pill">Test Manager + Orchestrator</span>**

以手动或自动化方式在机器人上运行测试集

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**分析 <span class="pill">Test Manager</span>**

结果、测试用例日志、断言、截图、报告

</div>
</div>

</div>

### 🤖 Autopilot for Testers { #autopilot-for-testers }

UiPath 开箱即提供多个测试智能体，内置于 Studio 和 Test Manager 中。本次课程会用到下面这些：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">📝</span>
<span class="f-title" markdown="span">Autopilot panel（Autopilot 面板） <span class="pill ">Studio</span></span>

根据你提供的文档生成需求，根据你的测试用例生成测试集，并保存到 Studio 项目所连接的 Test Manager 项目中

</div>

<div class="feature" markdown>
<span class="f-icon">🔍</span>
<span class="f-title" markdown="span">Evaluation Agent（评估智能体） <span class="pill ">Test Manager</span></span>

检查需求是否清晰、完整、可测试

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Test Case Generation Agent（测试用例生成智能体） <span class="pill ">Test Manager</span></span>

根据需求生成测试用例，生成方向由 **Prompt Library**（提示词库）引导：Valid E2E Scenario Testing、End-to-End Flow Verification、Rapid Test Idea Generation、Elusive Issue Detection、Boundary-Value Testing，以及你自己保存的提示词

</div>

<div class="feature" markdown>
<span class="f-icon">🎬</span>
<span class="f-title" markdown="span">Run Autonomously（自主运行） <span class="pill ">Test Manager</span></span>

无需自动化，直接按手动步骤运行测试用例。你可以实时观看，每个步骤的执行情况都会附带截图记录

</div>

<div class="feature" markdown>
<span class="f-icon">🔎</span>
<span class="f-title" markdown="span">Autopilot Search（Autopilot 搜索） <span class="pill ">Test Manager</span></span>

用自然语言提问，即可查找需求、测试用例和其他对象

</div>

<div class="feature" markdown>
<span class="f-icon">📥</span>
<span class="f-title" markdown="span">Import Test Cases（导入测试用例） <span class="pill ">Test Manager</span></span>

从 Excel 文件导入手动测试用例，并用一段提示词告诉 Autopilot 如何读取这个文件

</div>

<div class="feature" markdown>
<span class="f-icon">📊</span>
<span class="f-title" markdown="span">Generate Insights（生成洞察） <span class="pill ">Test Manager</span></span>

基于选定的测试结果生成报告：概览、失败最多的测试、常见错误、错误模式以及改进建议

</div>

<div class="feature" markdown>
<span class="f-icon">🪄</span>
<span class="f-title" markdown="span">Generate Test Case with Autopilot（使用 Autopilot 生成测试用例） <span class="pill ">Studio</span></span>

在 **Test Explorer** 中把手动测试用例转换为自动化测试用例，并利用项目的对象存储库定位 UI 元素

</div>

</div>

针对团队测试流程中独有的环节，你还可以构建自己的智能体。

### 🪄 Autopilot for Developers { #autopilot-for-developers }

Autopilot for Developers 位于 Studio 中，也就是你构建和修复自动化的地方。它会利用工作流的上下文（变量、数据类型以及当前表达式）来建议或直接应用修改：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🪄</span>
<span class="f-title" markdown="span">修复</span>

📍 **Expression Editor**（表达式编辑器）顶部的魔法棒

修正存在验证错误的表达式

</div>

<div class="feature" markdown>
<span class="f-icon">✍️</span>
<span class="f-title" markdown="span">生成或修改表达式</span>

📍 **Expression Editor** 底部的 Autopilot 输入框

根据自然语言指令编写或改写表达式，例如 *"Change the result of this expression to String"*（把这个表达式的结果改为 String）

</div>

<div class="feature" markdown>
<span class="f-icon">📝</span>
<span class="f-title" markdown="span">根据注释生成</span>

📍 工作流注释旁边的 Autopilot 选项

生成注释中描述的活动

</div>

</div>

!!! tip "如何给 Autopilot 写提示词"
    要清晰、具体、简洁。说明你期望的输出内容和格式，必要时设定限制。*"Summarize this."*（总结一下）只会得到一个笼统的回答；*"Summarize the following text in 100 words, highlighting key findings."*（用 100 个词总结以下文本，突出关键发现）才能得到真正有用的结果。

## 💻 什么是编码智能体？ { #whats-a-coding-agent }

编码智能体是一种能阅读、编写代码并对代码进行推理的 AI 助手，而不只是自动补全。它不是简单地建议下一行代码，而是理解你用自然语言描述的目标，探索代码库，做出决策，并生成完整可用的组件。控制权始终在你手里：你审查它构建的内容，让它调整，反复迭代直到满意为止。

如今已有多种编码智能体可选，各有所长：

- **Claude Code**：Anthropic 推出的基于 CLI（命令行）的智能体，在终端中运行，与文件系统深度集成。本次练习使用的就是它。
- **Codex CLI**：OpenAI 的命令行编码智能体，同样以终端为主
- **Cursor**：围绕 AI 打造的 IDE，与编辑器紧密集成，支持行内生成和多文件上下文
- **Gemini CLI**：Google 的终端智能体，擅长推理和长上下文
- **GitHub Copilot Agent**：内嵌于 VS Code 和 JetBrains，非常适合在编辑器内完成工作

编码智能体之所以特别适合 UiPath 工作，关键在于技能层：通过加载有关 UiPath 活动、API 和项目约定的领域知识，智能体能够生成可直接用于生产的测试自动化，而不是千篇一律的样板代码。这正是本次练习中 UiPath skills（UiPath 技能）所做的事情。

## 🧠 心智模型 { #the-mental-model }

每个编码智能体都离不开这五个概念：

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**工具（Tools）**

智能体可以执行的内置操作：读取文件、运行 bash 命令、搜索网页、编辑代码等。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**技能（Skills）**

领域知识包，智能体遇到匹配的任务时就会加载。就像专门针对某件事的操作手册。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**命令（Commands）**

你手动输入的快捷方式：`/commit`、`/test`、`/deploy`。由你触发，而不是智能体。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**钩子（Hooks）**

在生命周期事件发生时自动运行：编辑之前、提交之后、会话开始时。用于设置防护措施。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">5</span>
<div class="ci-body" markdown>

**子智能体（Subagents）**

由主智能体派生出来的专职工作者。用于并行处理或隔离复杂任务。

</div>
</div>

</div>

!!! info "插件（Plugins）"
    插件是把上述任意组件打包在一起的软件包，相当于编码智能体的「应用市场应用」。本次练习中使用的 UiPath skills 就是插件。

## 🔧 工具实战 { #tools-in-practice }

Claude Code 的内置工具随时可用，无需任何配置：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">📖</span>
<span class="f-title" markdown="span">Read</span>

读取项目中的任意文件

</div>

<div class="feature" markdown>
<span class="f-icon">✏️</span>
<span class="f-title" markdown="span">Edit / Write</span>

修改或创建文件

</div>

<div class="feature" markdown>
<span class="f-icon">⌨️</span>
<span class="f-title" markdown="span">Bash</span>

执行 shell 命令

</div>

<div class="feature" markdown>
<span class="f-icon">🔍</span>
<span class="f-title" markdown="span">Glob / Grep</span>

在整个代码库中搜索

</div>

<div class="feature" markdown>
<span class="f-icon">🌐</span>
<span class="f-title" markdown="span">WebSearch / WebFetch</span>

上网查找资料

</div>

<div class="feature" markdown>
<span class="f-icon">👥</span>
<span class="f-title" markdown="span">Task</span>

派生一个子智能体

</div>

</div>

!!! info "扩展工具（MCP）"
    MCP（Model Context Protocol，模型上下文协议）是为编码智能体添加新工具的标准方式，无需改动智能体本身。

    - **GitHub MCP**：读取 issue、创建 PR
    - **Atlassian MCP**：Jira、Confluence
    - **Slack MCP**：读取频道、发送消息
    - **Custom UiPath MCP**：调用 Orchestrator、Maestro

## 🧩 技能实战 { #skills-in-practice }

一个技能就是一个文件夹，位于 `.claude/skills/`（或等效位置）下，里面有一个 `SKILL.md` 文件。

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🔎</span>
<span class="f-title" markdown="span">自动发现</span>

智能体会读取每个 `SKILL.md` 的描述。当你的提示词与之匹配时，它会按需加载完整的技能。

</div>

<div class="feature" markdown>
<span class="f-icon">📦</span>
<span class="f-title" markdown="span">不只是文本</span>

技能可以打包参考文档、代码模式、辅助脚本，甚至是智能体可以运行的已编译二进制文件。

</div>

<div class="feature" markdown>
<span class="f-icon">🔒</span>
<span class="f-title" markdown="span">限定权限</span>

技能会声明它允许使用哪些工具。Bash 访问权限可以被严格控制。

</div>

</div>

### 📄 SKILL.md 文件里有什么 { #whats-in-a-skillmd-file }

每个技能都围绕一个 `SKILL.md` 文件构建。下面是一个示例：

```yaml
---
name: uipath-test
description: UiPath Test Manager — manage test projects, cases, sets, executions; generate reports...
allowed-tools: Bash, Read, Write, Glob, Grep
---

# UiPath Test Assistant

When the user asks to work with Test Manager:

1. Run `uip login status` and stop if the session isn't valid
2. Ask for the project name or key, then resolve it with `uip tm project list`
3. Use `uip tm` commands, always with `--output json`
4. If a command fails or a name matches more than one object, stop and ask

## References
- references/publish-and-link-guide.md
- references/failure-triage-guide.md
- references/test-result-report-guide.md
```

这个文件由四部分组成：

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**Frontmatter（前置元数据）**

声明技能的名称、描述，以及允许使用的工具。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**发现提示词**

`description` 字段是智能体用来与你的请求进行匹配的依据，技能就是这样被自动加载的。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**指令**

文件的正文：技能激活时智能体遵循的分步提示词。

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**参考资料**

指向技能文件夹中其他文件的路径，智能体可以读取它们获取更深入的上下文，例如 API 文档、代码模式、示例项目。

</div>
</div>

</div>

## 🔗 UiPath 在其中的位置 { #where-uipath-fits-in-this-picture }

UiPath 为 Claude Code 提供了一个插件。它打包了技能、钩子和参考资料，让智能体开箱即具备 UiPath 产品的领域知识。

```bash
npm -g install @uipath/cli
uip skills install
```

这个插件包含三部分内容：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">20+ 个技能</span>

覆盖每个 UiPath 产品的领域知识：`uipath-test`、`uipath-rpa`、`uipath-platform`、`uipath-agents`、`uipath-maestro-flow` 等。

</div>

<div class="feature" markdown>
<span class="f-icon">🤖</span>
<span class="f-title" markdown="span">1 个子智能体</span>

`uipath-project-discovery-agent`：首次接触 UiPath 项目时自动运行，为智能体构建上下文。

</div>

<div class="feature" markdown>
<span class="f-icon">🪝</span>
<span class="f-title" markdown="span">钩子与参考资料</span>

会话启动时的提示、活动文档，以及安全只读命令的允许列表。

</div>

</div>

## 📚 UiPath 技能目录 { #the-uipath-skill-catalog }

这个插件包含覆盖 UiPath 平台各个部分的技能。本次练习的实验由其中三个驱动：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-test` <span class="pill ">今日使用</span></span>

Test Manager：项目、需求、测试用例及步骤、测试集、执行、失败分析和报告。还能把 Studio 自动化关联到测试用例。

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-rpa` <span class="pill ">今日使用</span></span>

以「先发现、再动手」的方式生成和编辑 Studio 项目，包括测试自动化项目、Given / When / Then 测试用例和数据驱动测试

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-platform` <span class="pill ">今日使用</span></span>

认证、Orchestrator 管理（文件夹、包、资产）、Integration Service、CLI 工具

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-troubleshoot`</span>

当作业或运行出现异常时进行根因调查

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-agents`</span>

搭建、构建、运行、评估和部署编码智能体与低代码智能体

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">`uipath-maestro-flow`</span>

创建、验证和调试 UiPath Flow 项目

</div>

</div>

!!! tip "本次练习使用的技能"
    加粗显示的三个技能：`uipath-test`、`uipath-rpa` 和 `uipath-platform`。在动手实践课程中，如果你选择用编码智能体来自动化测试用例或运行测试集，它用到的就是这三个技能。

## ⚖️ 编码智能体的定位 { #where-the-coding-agent-fits }

Autopilot 一次只在一个产品内工作，处理的是你眼前的内容。编码智能体则在你的终端里，通过 `uip` CLI 跨产品工作：

<div class="vs" markdown>
<div class="vs-side" markdown>
<span class="f-title" markdown="span">🤖 Autopilot for Testers 与 Autopilot for Developers</span>

- **在哪里使用：** 在 Studio 或 Test Manager 内部
- **它能看到什么：** 你眼前的需求、表达式或结果
- **最适合：** 从文档生成需求和测试用例、评估需求质量、建议测试用例、修复表达式、解释结果

</div>
<div class="vs-mid">VS</div>
<div class="vs-side alt" markdown>
<span class="f-title" markdown="span">💻 编码智能体 + UiPath skills</span>

- **在哪里使用：** 你的终端或编辑器
- **它能看到什么：** 在同一个会话中看到你机器上的文件、你的 Studio 项目、Test Manager 和 Orchestrator
- **最适合：** 跨文件、跨产品的工作：对照文档检查覆盖率、批量编写 Given / When / Then 自动化，以及发布、关联、运行和报告

</div>
</div>

在动手实践课程中，Autopilot 唱主角。Studio 中的 Autopilot 编写需求和测试集，Test Manager 中的 Autopilot 评估需求、生成测试用例，并自主运行其中一个。Login 测试用例由你亲手实现自动化，这样你就知道「好的自动化」长什么样。接着，你用 Studio 中的 Autopilot 或编码智能体来自动化下一个测试用例，再把两者做个对比。
