动手实践 · 测试环境准备
{: .eyebrow }

# 🧭 智能体测试（Agentic Testing）：动手实践课程 { #agentic-testing-hands-on-session }

**借助 Autopilot for Testers、Autopilot for Developers 和编码智能体，在 UiPath Test Cloud 中把 UiBank 设计文档一步步变成需求、测试用例、自动化、测试集和执行。**

## 👋 概述 { #overview }

某银行的 QA 团队每个迭代都会收到一份新的应用说明。有人把它整理成需求；有人在 **Test Manager** 里手动录入测试用例；又有人在 **Studio** 里逐个重建，把每个字段、每个按钮都捕获一遍；第四个人把它们分组成测试集、运行，再把结果复制进状态邮件。四次交接，几个小时的点点点——而且不出一个月，文档、需求、测试用例和自动化就各说各话了。

在本次课程中，你会让 AI 智能体来完成上面每一项工作，同时看清哪些地方仍需要人来拍板。**Autopilot** 在产品内部工作：在 **Studio** 中，它可以创建需求、测试用例、测试集和表达式；在 **Test Manager** 中，它可以评估需求、生成测试用例，并自主运行测试用例。**Codex** 或 **Claude Code** 这样的**编码智能体**则在你的终端里工作，通过 **`uip` CLI**（命令行）和 **UiPath skills**（UiPath 技能）完成同样的自动化工作。你会先亲手构建一个测试用例，这样才能判断智能体替你做出来的东西好不好。

!!! tip "培训环境"
    请访问 **[{{ training_url }}]({{ training_url }})**，使用租户 **{{ training_tenant }}** 登录。本课程中的 Autopilot 功能运行在 **{{ env_label }}** 上，请确保 Studio、`uip` CLI 和浏览器都指向这个环境。

## 🗺️ 你将做什么 { #what-youll-do }

动手实践部分按照[议程](agenda.md)进行：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">⚙️</span>
<span class="f-title" markdown="span">**[环境准备](#setup)**</span>

在 Test Manager 中新建项目，在 Studio 中新建测试自动化项目，并把两者连接起来

👤 你

</div>

<div class="feature" markdown>
<span class="f-icon">📋</span>
<span class="f-title" markdown="span">**[需求](requirements.md)**</span>

把 UiBank 设计文档转化为需求，讨论它们、评估质量、加以改进，再重新评估

👤 **Studio 中的 Autopilot**、**Test Manager 中的 Autopilot**、你

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">**[测试用例](test-cases.md)**</span>

根据需求生成测试用例，亲手自动化 Login 测试用例，生成下一个，观看测试用例自主运行，再多加几个

👤 **Test Manager 中的 Autopilot**、你、**Studio 中的 Autopilot** 或**编码智能体**

</div>

<div class="feature" markdown>
<span class="f-icon">▶️</span>
<span class="f-title" markdown="span">**[执行](executions.md)**</span>

解读每次运行留下的记录

👤 你

</div>

<div class="feature" markdown>
<span class="f-icon">📦</span>
<span class="f-title" markdown="span">**[测试集](test-sets.md)**</span>

用你的测试用例创建测试集，运行它们，并查看其执行情况

👤 **Studio 中的 Autopilot**、你

</div>

<div class="feature" markdown>
<span class="f-icon">🚀</span>
<span class="f-title" markdown="span">**[后续步骤](#next-steps)**</span>

把这一切带回你自己的应用

👤 你

</div>

</div>

## 🏦 场景 { #the-scenario }

<div style="font-family: inherit; margin: 1.5rem 0 2rem;">

  <div style="background: #16213e; border-left: 10px solid #FA4616; padding: 26px 32px; margin-bottom: 22px;">
    <div style="font-size: 20px; font-weight: 700; color: #ffffff; line-height: 1.35;">一家银行的 QA 团队正在把回归测试套件迁移到智能体测试。</div>
    <div style="font-size: 15px; font-style: italic; color: #f6c3ab; margin-top: 10px; line-height: 1.45;">一份设计文档。需求、测试用例、测试集和执行，都由 Autopilot 和编码智能体构建，而由测试人员来决定什么才算通过。</div>
  </div>

  <div style="display: flex; flex-wrap: wrap; gap: 18px; align-items: stretch;">
  <div style="flex: 1 1 200px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 5px solid #FA4616; padding: 20px 22px 22px; box-sizing: border-box;">
    <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 18px;">
      <span style="font-size: 40px; line-height: 46px;">📋</span>
      <span style="font-size: 34px; font-weight: 700; color: #f6c3ab; line-height: 1;">01</span>
    </div>
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 12px;">需求</div>
    <div style="font-size: 13.5px; color: #4a4a4a; line-height: 1.55; margin-bottom: 18px;">Studio 中的 Autopilot 根据文档编写需求，Test Manager 中的 Autopilot 为它们打分。</div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12.5px; color: #FA4616; font-weight: 600;">&rarr; 8 条已评估的需求</div>
  </div>
  <div style="flex: 1 1 200px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 5px solid #FA4616; padding: 20px 22px 22px; box-sizing: border-box;">
    <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 18px;">
      <span style="font-size: 40px; line-height: 46px;">🧪</span>
      <span style="font-size: 34px; font-weight: 700; color: #f6c3ab; line-height: 1;">02</span>
    </div>
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 12px;">测试用例</div>
    <div style="font-size: 13.5px; color: #4a4a4a; line-height: 1.55; margin-bottom: 18px;">在 Test Manager 中生成，由你、Autopilot 或编码智能体完成自动化。</div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12.5px; color: #FA4616; font-weight: 600;">&rarr; 已自动化的测试用例</div>
  </div>
  <div style="flex: 1 1 200px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 5px solid #FA4616; padding: 20px 22px 22px; box-sizing: border-box;">
    <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 18px;">
      <span style="font-size: 40px; line-height: 46px;">🔎</span>
      <span style="font-size: 34px; font-weight: 700; color: #f6c3ab; line-height: 1;">03</span>
    </div>
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 12px;">执行</div>
    <div style="font-size: 13.5px; color: #4a4a4a; line-height: 1.55; margin-bottom: 18px;">每一次运行，无论手动、自动化还是自主执行，都附带结果和证据。</div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12.5px; color: #FA4616; font-weight: 600;">&rarr; 一目了然的结果</div>
  </div>
  <div style="flex: 1 1 200px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 5px solid #FA4616; padding: 20px 22px 22px; box-sizing: border-box;">
    <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 18px;">
      <span style="font-size: 40px; line-height: 46px;">📦</span>
      <span style="font-size: 34px; font-weight: 700; color: #f6c3ab; line-height: 1;">04</span>
    </div>
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 12px;">测试集</div>
    <div style="font-size: 13.5px; color: #4a4a4a; line-height: 1.55; margin-bottom: 18px;">Autopilot 为你的测试用例分组，你来运行并解读结果。</div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12.5px; color: #FA4616; font-weight: 600;">&rarr; 一个已执行的测试集</div>
  </div>
  </div>

</div>

整个课程中，工作是这样流转的：

```text
UiBank 设计文档 (.docx)
   │
   ▼
环境准备       在 Test Manager 中新建 {YourName}_UIB_Test 项目 ──▶ 在 Studio 中新建测试自动化项目 ──▶ 完成连接
   │
   ▼
需求           Studio 中的 Autopilot ──▶ 需求 ──▶ Test Manager 中的 Autopilot 评估 ──▶ 你来改进 ──▶ 重新评估
   │
   ▼
测试用例       Test Manager 中的 Autopilot ──▶ 测试用例（手动步骤）
                 ├─ Login：你在 Studio 中亲手自动化
                 ├─ 下一个：由 Studio 中的 Autopilot 或你的编码智能体自动化
                 ├─ Run Autonomously：Autopilot 亲自运行一个手动测试用例
                 └─ 再多加几个
   │
   ▼
执行           Executions 选项卡 ──▶ 迄今为止的每一次运行
   │
   ▼
测试集         Studio 中的 Autopilot ──▶ 测试集 ──▶ 发布 ──▶ 运行 ──▶ 执行
```

## 📄 设计文档 { #the-design-document }

本课程的一切都源自 UiBank Web 应用的一份设计文档：**E2E UiBank Online Banking**。请下载 `E2E UiBank Online Banking.docx`，并保存到你的工作坊文件夹中。

[下载设计文档 (.docx)](resources.assets/E2E%20UiBank%20Online%20Banking.docx){ .md-button .md-button--primary }

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🏦</span>
<span class="f-title" markdown="span">应用</span>

UiBank Web Application v2.0.0（Accounts / Transfers / Loans / Profile）

</div>

<div class="feature" markdown>
<span class="f-icon">🌐</span>
<span class="f-title" markdown="span">环境</span>

在 Google Chrome 中访问 `https://uibank.uipath.com`

</div>

<div class="feature" markdown>
<span class="f-icon">📝</span>
<span class="f-title" markdown="span">文档内容</span>

登录，开立一个 Checking 账户和一个 Savings 账户，在两者之间转账，申请贷款，按 Loan ID 查询贷款，并核验用户资料

</div>

</div>

文档用八个步骤描述了客户旅程。你不会把它当成一条很长的端到端流程来测试，而是让每个步骤都成为**一条需求**，并拥有**自己的测试用例**。这样一旦失败，就能直接定位到出问题的功能，某个页面坏了也不会掩盖其他功能的结果。

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">0</span>
<div class="ci-body" markdown>

**登录与初始账户状态**

`/login`、`/welcome`、`/accounts`

✅ 登录成功；记录初始账户状态

</div>
</div>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**创建 Checking 账户**

`/accounts/account-apply`

✅ Checking 账户出现在账户汇总中

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**创建 Savings 账户**

`/accounts/account-apply`

✅ Savings 账户出现在账户汇总中

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**账户间转账**

`/accounts/transfer-money`

✅ 两个账户的余额变动恰好等于转账金额

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**提交贷款申请**

`/loans/apply`

✅ 生成 Loan ID

</div>
</div>

<div class="circle-item" markdown>
<span class="num">5</span>
<div class="ci-body" markdown>

**查询贷款状态**

`/loans/lookup`

✅ 金额和期限与提交时一致

</div>
</div>

<div class="circle-item" markdown>
<span class="num">6</span>
<div class="ci-body" markdown>

**用户资料身份核验**

`/userprofile`

✅ 用户名和邮箱与当前登录用户一致

</div>
</div>

<div class="circle-item" markdown>
<span class="num">7</span>
<div class="ci-body" markdown>

**退出登录与证据收集**

`/`

✅ 会话已关闭；截图已附到报告中

</div>
</div>

</div>

### 🔢 测试数据 { #the-test-data }

以下是设计文档中定义的变量。请在提示词和自动化中都使用它们，让需求、测试用例和结果描述的是同一件事。

| 变量 | 含义 | 取值 / 规则 |
| :--- | :--- | :--- |
| `var_Username`, `var_Password` | UiBank 登录凭据 | 来自 Orchestrator 凭据资产 `{YourName}_UiBankCredential`，绝不硬编码。 |
| `var_CheckingNickname` | 新建的 Checking 账户 | `AutoChecking_<yyyyMMddHHmmss>`，每次运行唯一 |
| `var_SavingsNickname` | 新建的 Savings 账户 | `AutoSavings_<yyyyMMddHHmmss>`，每次运行唯一 |
| `var_TransferAmount` | 转账金额 | `10`，不得超过转出账户余额 |
| `var_LoanEmail` | 贷款申请人邮箱 | 你在 UiBank 上注册的邮箱 |
| `var_LoanAmount` | 贷款金额 | `5000` |
| `var_LoanTerm` | 贷款期限（年） | `3`（可选值：1、3、5、10） |
| `var_YearlyIncome` | 税前年收入 | `60000` |
| `var_Age` | 申请人年龄 | `35` |
| `var_LoanID` | UiBank 返回的 Loan ID | 提交贷款后提取 |

!!! warning "每个测试用例都必须处理的三件事"

    - **独立运行。** 测试用例可能以任意顺序、在任意机器人上运行。在文档里，转账使用的是第 1 步和第 2 步创建的账户，查询使用的是第 4 步得到的 Loan ID。而作为测试用例，转账要在开头自行开立两个账户，查询也要在开头自行提交一笔贷款。
    - **还没有账户。** 全新的 UiBank 用户看到的不是表格，而是 *"No accounts at this time, apply for a new account today!"*。这是合法的初始状态，不是失败。
    - **规则未知。** UiBank 是一个演示应用。余额和贷款审批规则都没有文档说明，数据也可能被重置。请检查贷款的实际结果，而不是默认它一定获批。

### 📋 Test Manager 是什么？ { #whats-test-manager }

<div style="background: #16213e; border-left: 10px solid #FA4616; padding: 22px 28px; margin: 1.2rem 0 1.4rem;">
  <div style="font-size: 19px; font-weight: 700; color: #ffffff; line-height: 1.35;">UiPath Test Cloud 的规划与报告中枢。</div>
  <div style="font-size: 15px; font-style: italic; color: #f6c3ab; margin-top: 9px;">需求说明什么必须可用，测试用例说明你如何证明它，测试集和执行则告诉你它到底行不行。</div>
</div>

<div style="display: flex; flex-wrap: wrap; gap: 14px; align-items: stretch; margin-bottom: 1.5rem;">
  <div style="flex: 1 1 220px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 4px solid #FA4616; padding: 18px 20px; box-sizing: border-box;">
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 9px;">需求</div>
    <div style="font-size: 14.5px; color: #4a4a4a; line-height: 1.55;">应用必须做到什么，以及验收标准</div>
  </div>
  <div style="flex: 1 1 220px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 4px solid #FA4616; padding: 18px 20px; box-sizing: border-box;">
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 9px;">测试用例</div>
    <div style="font-size: 14.5px; color: #4a4a4a; line-height: 1.55;">一个带手动步骤的场景，关联到它所覆盖的需求，也可以关联到一个自动化</div>
  </div>
  <div style="flex: 1 1 220px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 4px solid #FA4616; padding: 18px 20px; box-sizing: border-box;">
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 9px;">测试集</div>
    <div style="font-size: 14.5px; color: #4a4a4a; line-height: 1.55;">一起执行的一组测试用例</div>
  </div>
  <div style="flex: 1 1 220px; background: #ffffff; border: 1px solid #e8e8e8; border-top: 4px solid #FA4616; padding: 18px 20px; box-sizing: border-box;">
    <div style="font-size: 17px; font-weight: 700; color: #16213e; margin-bottom: 9px;">执行</div>
    <div style="font-size: 14.5px; color: #4a4a4a; line-height: 1.55;">一次运行，每个测试用例都有日志、结果和证据</div>
  </div>
</div>

## ⚙️ 环境准备 { #setup }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">一个 Test Manager 项目，以及一个与之连接的测试自动化项目</div>

<div style="background: #faf8f6; border: 1px solid #eee3dc; border-left: 4px solid #FA4616; padding: 18px 22px; margin: 1.4rem 0;">
  <div style="font-size: 14px; font-weight: 700; letter-spacing: 0.09em; color: #FA4616; margin-bottom: 9px;">你需要准备</div>
  <ul style="margin: 0; padding-left: 18px; font-size: 15px; color: #4a4a4a; line-height: 1.55;"><li style="margin-bottom: 5px;">在浏览器中打开 <strong>{{ training_tenant }}</strong> 租户上的 <strong>Test Manager</strong>。</li></ul>
</div>

### 🆕 在 Test Manager 中新建项目 { #create-a-new-project-in-test-manager }

需求、测试用例、测试集和执行都存放在 Test Manager 项目中。先把你的项目建好：后面各部分中 Autopilot 生成的所有内容都会放进去。

1. 访问 **[{{ training_url }}]({{ training_url }})**，选择 **{{ training_tenant }}** 租户，然后打开 **Test Manager**。
2. 在 **Projects**（项目）页面，选择 **Create new project**（新建项目）。
3. 在 **Create new project** 对话框中填写：
    - **Name:**（名称）`{YourName}_UIB_Test`
    - **Prefix:**（前缀）`UIB`。至少 3 个字符，只能包含字母和数字。
    - **Description:**（描述）可选，例如 *UiBank online banking tests*。

    ![Test Manager 中的 Create new project 对话框，名称为 {YourName}_UIB_Test，前缀为 UIB，描述为空，以及 Create 按钮](agentic-testing-hands-on.images/test-manager-create-new-project-W.png){ .screenshot width="900" }
    *Create new project 对话框，已填写 `{YourName}_UIB_Test`，前缀为 `UIB`。*

    !!! info "前缀有什么用"
        项目中的每个对象都会获得一个以前缀开头的键：第一条需求是 `UIB:1`，下一条是 `UIB:2`，依此类推，需求、测试用例和测试集统一编号。前缀要简短好认，不必追求描述性。

4. 选择 **Create**（创建），然后打开项目。目前它还是空的。
5. 设置项目的默认 Orchestrator 文件夹。之后测试集运行自动化测试用例时需要用到它。
    1. 在项目左侧菜单中选择 **Project Settings**（项目设置），然后打开 **Automation**（自动化）选项卡。
    2. 在 **Default Folder**（默认文件夹）中选择 `{{ training_folder }}`。
    3. 选择 **Save**（保存）。

    ![Test Manager 项目设置中的 Automation 选项卡，Default Folder 选择了 AgenticTesting，以及 Save 按钮](agentic-testing-hands-on.images/test-manager-default-folder.png){ .screenshot width="800" }
    *Project Settings > Automation，默认文件夹为 `{{ training_folder }}`。*

!!! tip "为什么项目名里要带上你的名字"
    课程中所有人都在同一个租户里工作。带上名字，你就能在 **Projects** 列表中轻松找到自己的项目，也能让你的需求、测试用例和结果与其他人的互不干扰。

### 🛠️ 在 UiPath Studio Desktop 中新建测试自动化项目 { #create-a-new-test-automation-project-in-uipath-studio-desktop }

1. 打开 **Studio**。在 **Start**（开始）界面的 **New Project**（新建项目）下，选择 **Test Automation**（测试自动化）。
2. 在 **New Blank Test Project**（新建空白测试项目）对话框中填写：
    - **Name:** `{YourName}UiBankTests`
    - **Description:** 可选，例如 *Test Automation Project*

    ![Studio 中的 New Blank Test Project 对话框，名称为 {YourName}UiBankTests，带有描述，以及高级选项 Location、Compatibility Cross-platform、Language VB 和 Minimum Robot version](agentic-testing-hands-on.images/studio-new-test-project-W.png){ .screenshot width="900" }

3. 选择 **Create**。
4. Studio 会打开新项目。在 **Project**（项目）面板中展开 **Dependencies**（依赖项），确认测试相关的包都已就位，例如 `UiPath.Testing.Activities` 和 `UiPath.UIAutomation.Activities`。

!!! tip "为什么要用测试自动化项目"
    测试自动化项目就是为测试用例而生的：它自带测试活动、Given / When / Then 模板和 **Test Explorer** 面板。其中的每个测试用例都可以关联到 Test Manager 中的测试用例，在那里运行时，结果也会回传到 Test Manager。

### 🔗 连接到 Test Manager { #connect-it-to-test-manager }

项目需要知道它的需求、测试用例和结果归属于哪个 Test Manager 项目。任选一种方式：

=== "在 Studio 中"

    1. 在 **Explorer**（资源管理器）面板中右键单击项目名称，选择 **Project Settings**。
    2. 选择 **Test Manager Configuration**（Test Manager 配置）。
    3. 在 **Test Manager Settings**（Test Manager 设置）下输入 Test Manager URL `{{ training_url }}/{{ training_tenant }}/testmanager_`，然后选择 **Connect**（连接）。状态会变为 **Connected**（已连接）。
    4. 在 **Default Project**（默认项目）中输入前缀 `UIB`，然后选择 **{YourName}_UIB_Test (UIB)**。
    5. 选择 **OK**（确定）。

    <video src="../agentic-testing-hands-on.images/studio-connect-test-manager.mp4" autoplay loop muted playsinline controls aria-label="将 Studio 项目连接到 Test Manager：Project Settings、Test Manager Configuration、输入 Test Manager URL、Connect、选择默认项目，然后 OK" style="display: block; width: 100%; margin: 1.5rem auto; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);"></video>

=== "使用编码智能体"

    在 Studio 中关闭项目，在工作坊文件夹中启动编码智能体，然后给它这段提示词：

    ```text
    Connect the Studio project in ./{YourName}UiBankTests to Test Manager at
    {{ training_url }}/{{ training_tenant }}/testmanager_ with my {YourName}_UIB_Test project
    (prefix UIB) as the default project, and show me uip rpa tm status.
    ```

    然后在 Studio 中重新打开项目。连接信息保存在项目的 `.tmh/config.json` 中，因此 Studio、Autopilot 和 CLI 用的都是同一个连接。

### ✅ 确认准备就绪 { #check-youre-ready }

- Studio 显示 **{YourName}_UIB_Test** 为默认 Test Manager 项目。
- Studio 中可以打开 **Autopilot** 面板。
- 浏览器中已打开 **Test Manager**，并位于 **{YourName}_UIB_Test** 项目中。

你的工作坊文件夹现在应该是这样的：

```text
workshop/
├── {YourName}UiBankTests/           ← Studio 测试自动化项目，已连接到 Test Manager
└── E2E UiBank Online Banking.docx   ← 设计文档
```

!!! success "环境准备完成"
    Test Manager 中有了新的 **{YourName}_UIB_Test** 项目，Studio 中也有了与之连接的新测试自动化项目。现在，Autopilot 可以直接把需求写进去了。

## 🚀 后续步骤 { #next-steps }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">你构建了什么，以及可以带回去的收获</div>

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">📋</span>
<span class="f-title" markdown="span">需求</span>

由 Studio 中的 Autopilot 根据一份设计文档生成的八条需求，并经 Test Manager 中的 Autopilot 评估和改进

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">测试用例</span>

由 Test Manager 中的 Autopilot 生成的测试用例；Login 由你亲手自动化；更多测试用例由 Studio 中的 Autopilot 或编码智能体自动化；外加一次自主运行

</div>

<div class="feature" markdown>
<span class="f-icon">🔎</span>
<span class="f-title" markdown="span">执行</span>

每次运行都记录了结果和证据，并可追溯到对应的需求

</div>

<div class="feature" markdown>
<span class="f-icon">📦</span>
<span class="f-title" markdown="span">测试集</span>

一个冒烟测试集和一个回归测试集，由 Autopilot 创建并在机器人上执行

</div>

</div>

**本周**

- 明天再跑一次回归测试集。还能通过吗？如果不能，是测试的问题，还是 UiBank 的问题？
- 自动化 Autopilot 生成的某个反向测试用例，例如转账金额大于 Checking 账户余额。

**未来 30 天**

- 拿一份你们团队真实的设计文档，按同样的几个部分走一遍：需求、测试用例、测试集。
- 换另一种智能体试试：如果你的第二个测试用例用的是 Autopilot，那就用编码智能体自动化下一个，反之亦然。
- 把一个测试用例改成数据驱动，让它用多组取值运行。

**长期**

- 带着问题来。没有哪个问题算太基础，尤其是在起步阶段。
- 遇到问题请告诉我们。一旦技能猜错、命令失败，或者某一步要试三次才成功，马上运行 `uip feedback send`。

## ⚠️ 你会遇到的常见问题 { #gotchas-youll-hit }

每个 QA 团队在第一个月都会学到的事。

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🔍</span>
<span class="f-title" markdown="span">信任，但要验证</span>

Autopilot 和编码智能体又快又自信。请认真阅读生成的需求、测试用例和断言：一个什么都不检查的测试，每次都会通过。

</div>

<div class="feature" markdown>
<span class="f-icon">🎯</span>
<span class="f-title" markdown="span">选对智能体</span>

产品里眼前的活交给 Autopilot；跨文件、跨项目、跨产品的工作交给编码智能体。

</div>

<div class="feature" markdown>
<span class="f-icon">🧩</span>
<span class="f-title" markdown="span">测试用例相互独立</span>

每个测试都在 **Given** 中准备好自己的数据。找机会换个顺序运行一次，证明这一点。

</div>

<div class="feature" markdown>
<span class="f-icon">✍️</span>
<span class="f-title" markdown="span">好的手动步骤，一举两得</span>

每个步骤只包含一个操作和一个预期结果，既能帮助 Autopilot 生成自动化，也能帮助它自主运行测试用例。

</div>

<div class="feature" markdown>
<span class="f-icon">🎯</span>
<span class="f-title" markdown="span">绝不手写选择器</span>

从运行中的应用捕获目标，存入对象存储库（Object Repository）。一个看似合理却什么都匹配不到的选择器，代价远比捕获一次要高。

</div>

<div class="feature" markdown>
<span class="f-icon">🌐</span>
<span class="f-title" markdown="span">同一个环境</span>

Studio、CLI 和浏览器都要在同一个租户上。大多数「Autopilot 找不到我的项目」的问题，都是因为 Studio 登录到了别的地方。

</div>

</div>

## ⌨️ 附录：CLI 速查表 { #appendix-cli-cheat-sheet }

如果你用编码智能体生成测试用例或运行测试集，就会看到它通过 `uip` CLI 运行以下命令。每条命令都可以加上 `--output json`。

| 命令 | 作用 | 何时会看到 |
| :--- | :--- | :--- |
| `uip skills install` | 将 UiPath skills 安装到你的编码智能体中 | 首次设置 |
| `uip login` / `uip login status` | 向租户进行身份验证 / 检查会话 | 每次会话开始时 |
| `uip tm project list --filter <key>` | 查找 Test Manager 项目 | 进行任何 Test Manager 工作之前 |
| `uip tm requirements list` / `uip tm testcases list` | 列出需求和测试用例 | 检查覆盖率 |
| `uip rpa tm connect` / `set-default-project` | 将 Studio 项目连接到 Test Manager | 环境准备 |
| `uip rpa validate` / `uip rpa build` | 检查并构建项目 | 每次修改之后 |
| `uip rpa pack` + `uip or packages upload` | 打包并发布到 Orchestrator | 运行测试集之前 |
| `uip tm testcases link-automation` | 将自动化绑定到 Test Manager 测试用例 | 发布之后 |
| `uip tm testsets run` + `uip tm wait` | 执行测试集并等待结果 | 运行测试集 |
| `uip tm report get` / `uip tm result download` | 汇总一次执行 / 下载 JUnit XML | 生成报告 |
| `uip feedback send` | 报告缺陷或猜错的技能 | 任何出问题的时候 |
