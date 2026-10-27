动手实践 · 第 4 部分（共 4 部分）
{: .eyebrow }

# 📦 测试集 { #test-sets }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">分组、运行、解读结果</div>

## 📤 将测试项目发布到租户源 { #publish-your-testing-project-to-the-tenant-feed }

Autopilot 会根据它在 Orchestrator 中找到的自动化测试用例来构建测试集，而 Test Manager 则从已发布的包中运行它们。所以，先发布。

1. 在 **Studio** 中打开你的 `{YourName}UiBankTests` 项目，选择 **Publish**（发布）。
2. 在 **Publish to**（发布到）中，选择 **Orchestrator Tenant Process Feed**（Orchestrator 租户流程源）。
3. 如果之前发布过，先把版本号调高，然后选择 **Publish**。
4. 等待包已发布的确认提示。

!!! info "为什么要发布到租户源"
    测试集的自动化运行只会包含发布到 **Orchestrator Tenant Process Feed** 的最新包版本中的测试用例。发布到个人工作区源的包，或者旧版本的包，都不会被选中。每次修改测试用例后，都要重新发布。

## 🪄 让 Studio 中的 Autopilot 创建测试集 { #ask-autopilot-in-studio-to-create-test-sets }

1. 在 **Studio** 中，打开 `{YourName}UiBankTests` 项目里的 **Autopilot** 面板。
2. 把下面这段提示词交给 Autopilot：

    ```text
    In my {YourName}_UIB_Test Test Manager project, create two test sets from the
    existing test cases:
    - "UiBank Smoke" with Login and Initial Account State only.
    - "UiBank Regression" with every test case that is automated
      in this Studio project.
    Show me the test cases you'll put in each set before you create them.
    ```

3. 检查它给出的方案，然后接受。在 Test Manager 中打开 **Test Sets**（测试集），确认两个测试集都已存在，且包含正确的测试用例。

!!! tip "为什么要有冒烟测试集？"
    冒烟测试集能快速回答一个问题：应用是否正常运行，我能不能登录？先运行它。如果它失败了，就没必要再等完整的回归测试集了。

## ▶️ 运行测试集 { #run-the-test-sets }

Test Manager 会在 `{{ training_folder }}` 文件夹中的机器人上，使用你发布到租户源的包来运行自动化测试用例。

1. 在 Test Manager 中打开 **Test Sets**，选择 **UiBank Smoke**，然后选择 **Execute** > **Automated**（执行 > 自动化）。
2. 它通过之后，用同样的方式运行 **UiBank Regression**。

=== "或者让你的编码智能体来做"

    ```text
    Publish {YourName}UiBankTests to the tenant feed of the {{ training_tenant }}
    tenant if the latest version isn't there yet, check that each automated
    test case is linked to its
    Test Manager test case in my {YourName}_UIB_Test project, then run my
    "UiBank Smoke" and "UiBank Regression" test sets as
    automated executions, wait for them to finish, and give me a report.
    Confirm `uip login status` first, and stop if any step fails.
    ```

    编码智能体会加载 `uipath-test` 技能，并运行 `uip rpa pack`、`uip or packages upload`、`uip tm testcases link-automation`、`uip tm testsets run` 和 `uip tm wait`。

!!! tip "自动化测试用例不够？"
    那就改用讲师提供的 `DemoUiBankTests` 测试用例。让 Autopilot 或你的编码智能体，把 `{{ training_folder }}` 文件夹中的 `DemoUiBankTests` 包关联到你的 Test Manager 中同名的测试用例上，然后运行测试集。参见[资源](resources.md)。

!!! warning "机器人使用的是你的凭据资产"
    机器人会从 `{{ training_folder }}` 文件夹读取 `{YourName}_UiBankCredential`，和你本地运行时一样。如果该资产放在别处，每个测试都会在打开浏览器之前就在 **Given** 阶段失败。

!!! info "只能手动执行的测试用例怎么办？"
    自动化执行会跳过没有自动化的测试用例。如果要包含它们，请以 **Manually**（手动）方式执行测试集，或者自主运行它们。

## 🔎 查看测试集的执行 { #look-into-the-executions-of-the-test-sets }

1. 在 Test Manager 中打开 **Execution**（执行）选项卡，找到你刚刚启动的两次执行。
2. 打开 **UiBank Regression**，查看每个测试用例的结果。
3. 如果有失败的测试用例，打开它的日志。阅读失败的断言及其截图。问题出在测试本身，还是 UiBank？
4. 选中这些结果，然后选择 **Generate Insights**（生成洞察）。Autopilot 会生成一份报告，包含 **Overview**（概览）、**Top Failing Tests**（失败最多的测试）、**Common Errors**（常见错误）、**Error Patterns**（错误模式）和 **Recommendations**（建议）。

!!! success "测试集完成"
    两个由 Autopilot 创建的测试集，从 Test Manager 在机器人上执行，每个自动化测试用例都有结果和证据。

## 🛠️ 常见出错点 { #where-it-usually-breaks }

<div class="fix-grid" markdown>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 运行失败，提示 *"Please assign folder to project level"*</span>

<span class="lbl">原因</span> 你的 Test Manager 项目没有默认文件夹

<span class="lbl">解决</span> 将项目的默认文件夹设置为 `{{ training_folder }}`，然后重新运行

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 Autopilot 找不到 **UiBank Regression** 的自动化测试用例</span>

<span class="lbl">原因</span> 项目还没有发布到租户源

<span class="lbl">解决</span> 将其发布到 **Orchestrator Tenant Process Feed**，然后再问一次 Autopilot

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 部分测试用例没有结果</span>

<span class="lbl">原因</span> 它们没有自动化，或者不在最新发布的包中

<span class="lbl">解决</span> 重新发布到 **Orchestrator Tenant Process Feed**，并检查每个 Studio 测试用例是否都已关联到对应的 Test Manager 测试用例

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 每个测试都在 **Given** 阶段失败</span>

<span class="lbl">原因</span> 机器人无法读取凭据资产

<span class="lbl">解决</span> 检查资产名称和所在文件夹

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 测试单独运行能通过，放进测试集就失败</span>

<span class="lbl">原因</span> 它依赖其他测试遗留下来的数据

<span class="lbl">解决</span> 让它的 **Given** 把所需的一切都准备好

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 上传被拒绝</span>

<span class="lbl">原因</span> 该包版本已经存在

<span class="lbl">解决</span> 调高项目版本号，然后重新发布

</div>

<div class="fix" markdown>
<span class="f-title" markdown="span">🚨 执行一直停留在 Pending</span>

<span class="lbl">原因</span> 文件夹中没有空闲的机器人

<span class="lbl">解决</span> 告诉讲师。机器人是大家共享的。

</div>

</div>
