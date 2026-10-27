动手实践 · 第 2 部分（共 4 部分）
{: .eyebrow }

# 🧪 测试用例 { #test-cases }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">先生成，再亲手自动化一个，剩下的交给智能体</div>

## 🤖 让 Test Manager 中的 Autopilot 创建测试用例 { #ask-autopilot-in-test-manager-to-create-test-cases }

**Test Case Generation Agent**（测试用例生成智能体）会根据需求编写测试用例，包含手动步骤和预期结果。

1. 在 Test Manager 的 **Requirements**（需求）下打开一条需求，例如 **Login and Initial Account State**。
2. 让 Autopilot 为它生成测试用例。想引导生成方向，可以从 **Prompt Library**（提示词库）中选一个提示词：**Valid E2E Scenario Testing**（有效端到端场景测试）用于有效的端到端场景，**Boundary-Value Testing**（边界值测试）用于边界情况。
3. 审阅生成的建议。保留正常路径（happy path），并将其命名为 **Login and Initial Account State**。再保留一两个反向用例，例如密码错误。其余的丢弃。
4. 打开 **Login and Initial Account State**，阅读它的手动步骤。每个步骤都需要有一个操作，以及一个你能在屏幕上核对的预期结果。

!!! tip "Prompt Library"
    Prompt Library 中存放着预定义的提示词，例如 **Valid E2E Scenario Testing**、**End-to-End Flow Verification**（端到端流程验证）、**Rapid Test Idea Generation**（快速生成测试思路）、**Elusive Issue Detection**（隐蔽问题检测）和 **Boundary-Value Testing**，还有你的团队保存的自定义提示词。一个提示词在某条需求上好用，通常在下一条上也好用，所以把好用的都存起来。

## ✍️ 手动实现 Login 测试用例 { #implement-the-login-test-case-by-hand }

在让任何智能体替你自动化测试之前，先自己动手做一个。这会花更长时间，而这正是目的所在：等智能体五分钟就搞定时，你会清楚地知道该检查什么。

<div style="background: #16213e; border-left: 10px solid #FA4616; padding: 22px 28px; margin: 1.2rem 0 1.4rem;">
  <div style="font-size: 19px; font-weight: 700; color: #ffffff; line-height: 1.35;">每个 UiPath 测试用例都由三部分组成：Given、When、Then。</div>
  <div style="font-size: 15px; font-style: italic; color: #f6c3ab; margin-top: 9px;">准备好测试所需的一切。执行被测的那一个操作。检查应用显示的内容。</div>
</div>

**创建测试用例**

1. 在 **Studio** 中，从你的 Test Manager 测试用例里找到 **Login and Initial Account State**，并创建一个与之关联的 Studio 测试用例。将文件命名为 `T0_LoginTC.xaml`。
2. 新测试用例打开后包含三个序列：**Given**、**When** 和 **Then**。

**Given：准备**

3. 添加一个 **Get Credential**（获取凭据）活动。将资产名称设为 `{YourName}_UiBankCredential`，文件夹设为 `{{ training_folder }}`。将输出分别保存到 `var_Username`（String）和 `var_Password`（SecureString）。

**When：登录并打开 Accounts**

4. 在 Chrome 中打开 `https://uibank.uipath.com/login`。
5. 添加一个 **Use Application/Browser**（使用应用程序/浏览器）活动，并指定 UiBank 登录页面。
6. 在其中为 **Enter username**（输入用户名）字段添加 **Type Into**（输入信息），值为 `var_Username`；再为 **Enter password**（输入密码）字段添加 **Type Into**，以安全文本方式输入 `var_Password`。
7. 在 **Sign In**（登录）上添加 **Click**（单击）。
8. 添加 **Check App State**（检查应用程序状态），并指定 Welcome 横幅。它会检查登录后该横幅是否出现。将结果保存到 `var_WelcomeBannerShown`（Boolean）。
9. 在 **Accounts**（账户）上添加 **Click**，然后在账户摘要区域添加 **Get Text**（获取文本），并将结果保存到 `var_AccountSummary`。

**Then：验证**

10. 添加 **Verify Expression**（验证表达式），使用 `var_WelcomeBannerShown`。
11. 再添加一个 **Verify Expression**，检查 `var_AccountSummary` 要么包含 *"No accounts at this time"*，要么至少列出了一个账户。
12. 在每个验证上打开截图选项，这样证据就会附加到结果中。

**运行**

13. 在 **Test Explorer** 中运行测试用例。两个验证都必须通过。
14. 再运行一次。必须再次通过。

!!! tip "使用对象存储库"
    指定目标时，将其保存到 **Object Repository**（对象存储库）。你在下一个测试用例中使用的智能体会复用这些目标，所以你亲手捕获的登录字段，正是 Autopilot 和你的编码智能体后续工作的基础。

!!! success "Login 测试用例完成"
    `T0_LoginTC.xaml` 已关联到对应的 Test Manager 测试用例，连续通过两次，每个验证都带有截图。记下花了多长时间，待会儿要和下一个测试用例做对比。

## 🪄 用 Autopilot 或编码智能体生成下一个测试用例 { #generate-the-next-test-case-with-autopilot-or-a-coding-agent }

现在让智能体来自动化下一个。选一条排在 Login 之后的需求，例如 **Checking Account Creation**。先按照 Login 的做法在 Test Manager 中为它生成测试用例，并将正常路径保留为 **Checking Account Creation**。

!!! warning "使用 Autopilot 实际生成的测试用例名称"
    Test Manager 中的 Autopilot 给测试用例起名并不总是一样的。你的可能叫 **Open a Checking Account**、**Step 1: Open a Checking Account**，或者别的名字。请在 Test Manager 的 **Test Cases**（测试用例）下确认准确的名称，并在下面的提示词中凡是出现 **Checking Account Creation** 的地方都换成它。否则 Studio、Autopilot 或你的编码智能体会把自动化关联到错误的测试用例，或者根本找不到测试用例。

然后用下面这个提示词来自动化它。你可以把它交给 Studio 中的 Autopilot，也可以交给编码智能体。提示词完全相同，只是输入的地方不同：

```text
In this test automation project, which is connected to my
{YourName}_UIB_Test Test Manager project, automate the Test Manager test
case "Checking Account Creation" as T1_CheckingAccountCreation.xaml,
linked to that test case.

Use Given / When / Then. Given logs in: read var_Username and var_Password
from the credential asset {YourName}_UiBankCredential in the
{{ training_folder }} folder, and reuse the login steps and Object Repository
targets from T0_LoginTC.xaml. When applies for a Checking account with the
nickname AutoChecking_<yyyyMMddHHmmss>. Then verifies the account is
listed with its nickname and type, with a screenshot on every
verification.

Capture any new UI targets from the live UiBank site into the Object
Repository. Don't write selectors by hand. Inspect the project before you
edit it, then validate and build it. Ask me before you run it.
```

=== "Studio 中的 Autopilot"

    1. 在 **Studio** 中打开你的 `{YourName}UiBankTests` 项目，然后打开 **Autopilot** 面板。
    2. 将提示词粘贴到 **Ask Autopilot anything**（向 Autopilot 提问）中并发送。
    3. 在接受之前，先审阅 Autopilot 的方案：**Given** 是否先登录？**Then** 是否检查了新账户以正确的昵称和类型出现？
    4. 接受更改，然后在 **Test Explorer** 中运行该测试用例，运行两次。

=== "编码智能体（Codex、Claude Code）"

    1. 在 **Studio** 中打开你的 `{YourName}UiBankTests` 项目，然后打开窗口底部的 **Terminal**（终端）面板。它会在你的项目文件夹中打开。
    2. 在那里启动你的编码智能体：

        ```bash
        claude
        # 或者
        codex
        ```

    3. 将提示词粘贴到终端中，然后按 **Enter**（回车）。
    4. 回答它提出的问题，并在批准之前读一遍它建议的每条命令。
    5. 完成后，在 **Test Explorer** 中运行该测试用例，运行两次。

    编码智能体会加载 `uipath-rpa` 技能，先读取项目和你的 Login 测试用例，然后编写新的测试用例。如果它在浏览器中访问不到 UiBank，它不会去猜选择器，而是把无法定位目标的活动命名为 `TODO Indicate — …`。你可以在 Studio 中手动指定这些目标，或者在 Chrome 中打开 UiBank，然后让它再试一次。

!!! warning "检查、验证并修正生成的测试用例"
    不管是哪个智能体生成的，测试用例都要由你来签字确认。在继续之前，在 Studio 中打开它，对照它的 Test Manager 测试用例和设计文档进行检查：

    - **Given** 会先登录，并准备好测试所需的一切，使其可以独立运行。
    - **When** 执行手动步骤所描述的操作，作用在正确的界面和字段上。
    - **Then** 验证每一个预期结果，值都正确，并且每个验证都带有截图。
    - 它在 **Test Explorer** 中运行并通过，连续两次。

    发现有错误或缺失的地方，就去修正：在 Studio 中自己动手改，针对单个表达式使用 Autopilot，或者让智能体修复，并准确告诉它哪里有问题。

和你亲手构建的 Login 测试用例做个对比：

- 花了多长时间？
- 结果和你写的一样易读吗？你会不看内容就信任它的 **Then** 部分吗？
- 它复用了你的登录目标，还是重新捕获了新的目标？

!!! warning "同一时间只在一个地方修改"
    Studio、Autopilot 和你的编码智能体都可以编辑同一批文件。在编码智能体修改某个文件之前，先在 Studio 中关闭它；你在 Studio 中改了什么，也要告诉编码智能体，让它重新读取项目，而不是覆盖你的工作。

!!! tip "Autopilot for Developers"
    审阅生成的测试用例时，可以针对单个表达式使用 Autopilot。在 **Expression Editor**（表达式编辑器）中，对任何有验证错误的表达式选择 **Fix**（修复，魔术棒图标），或者在底部的 Autopilot 输入框中输入指令，例如 *"Build the nickname AutoChecking_ followed by the current time as yyyyMMddHHmmss."*

## 🎬 在 Test Manager 中自主运行 { #run-autonomously-in-test-manager }

并不是每个测试用例都得先有自动化才能运行。在 Test Manager 中，Autopilot 可以**自主**运行测试用例：它读取手动步骤，直接在应用上执行，然后为每个步骤记录结果并附上证据。

拿你在 Autopilot 生成测试用例时保留的某个登录反向用例来试试：

1. 在 Test Manager 的 **Test Cases** 下，打开一个有手动步骤但没有自动化的测试用例。
2. 选择 **Run Autonomously**（自主运行）。
3. 打开 **live stream**（实时画面），实时观看测试用例的运行过程：Autopilot 就在你眼前，在 UiBank 上一步步执行手动步骤。
4. 运行结束后，打开结果。每个步骤的执行都有记录，附有 Autopilot 当时看到的画面截图，旁边是该步骤的结果。

大家一起讨论：

- 什么时候你会选择自主运行测试用例，而不是把它自动化？对新功能的一次性检查，或者每个迭代都在变化的测试用例，都是不错的候选。
- 什么样的手动步骤让 Autopilot 容易照着执行？和让人容易照着执行的一样：一个操作、一个预期结果、使用屏幕上的准确标签。

## ➕ 再实现几个测试用例 { #implement-a-few-more-test-cases }

再挑两三条需求，重复这个循环：在 Test Manager 中生成测试用例，保留正常路径，然后用 Studio 中的 Autopilot 或你的编码智能体将其自动化。建议顺序如下，并列出了每个测试用例的 **Given** 必须准备的内容，以便其独立运行：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Savings Account Creation</span>

📄 `T2_SavingsAccountCreation.xaml`

**Given：** 登录

**Then：** 储蓄账户已列出，显示其昵称和类型

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Funds Transfer Between Accounts</span>

📄 `T3_FundsTransferBetweenAccounts.xaml`

**Given：** 登录，开立一个支票账户和一个储蓄账户，读取两者的余额

**Then：** 支票账户 = 转账前 − `var_TransferAmount`；储蓄账户 = 转账前 + `var_TransferAmount`

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Loan Application Submission</span>

📄 `T4_LoanApplicationSubmission.xaml`

**Given：** 登录

**Then：** 捕获结果消息；返回 Loan ID

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Loan Status Lookup</span>

📄 `T5_LoanStatusLookup.xaml`

**Given：** 登录，提交一笔贷款，保留 `var_LoanID`

**Then：** 金额和期限一致

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">User Profile Identity Verification</span>

📄 `T6_UserProfileIdentityVerification.xaml`

**Given：** 登录

**Then：** 用户名和电子邮件一致

</div>

<div class="feature" markdown>
<span class="f-icon">🧪</span>
<span class="f-title" markdown="span">Logout and Evidence Collection</span>

📄 `T7_LogoutAndEvidenceCollection.xaml`

**Given：** 登录

**Then：** 会话已关闭；顶部菜单不再可用

</div>

</div>

!!! warning "别想当然地认为贷款会获批"
    UiBank 的贷款审批规则没有文档说明。无论贷款被批准还是被拒绝，贷款测试都必须通过，只要返回了 Loan ID，并且查询结果显示的金额和期限一致即可。

!!! tip "余额检查失败了？"
    先看截图，再看代码。常见原因有两个：一是读取到的余额是带货币符号的文本（`$1,000.00` 在解析之前并不是数字）；二是在账户摘要刷新之前就读取了余额。表达式编辑器中的 Autopilot 做这种转换很快：*"Convert this text, for example "$1,000.00", to a Decimal."*

!!! success "测试用例完成"
    至少四个自动化测试用例，每个都关联到对应的 Test Manager 测试用例，并且能独立运行通过：Login 是你亲手构建的，其余的由 Autopilot 或你的编码智能体构建。此外还有几个由 Autopilot 生成的纯手动测试用例，以及一次自主运行。
