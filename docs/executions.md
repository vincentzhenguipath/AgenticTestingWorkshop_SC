动手实践 · 第 3 部分（共 4 部分）
{: .eyebrow }

# ▶️ 执行 { #executions }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">每一次运行都会留下证据</div>

## 🗂️ 执行类型一览 { #execution-types-at-a-glance }

在 Test Manager 中，每一次运行都是一次**执行**，而每次执行都有自己的类型。在本次课程中，你会把它们全部见识一遍：

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">✋</span>
<span class="f-title" markdown="span">手动</span>

👤 由人来执行，**Manual Execution Assistant** 全程引导

▶️ 在测试用例或测试集上选择 **Execute** > **Manually**（执行 > 手动）

</div>

<div class="feature" markdown>
<span class="f-icon">🤖</span>
<span class="f-title" markdown="span">自动化</span>

👤 由机器人运行与测试用例关联的自动化

▶️ 测试用例完成自动化并发布后，选择 **Execute** > **Automated**（执行 > 自动化）

</div>

<div class="feature" markdown>
<span class="f-icon">🎬</span>
<span class="f-title" markdown="span">自主</span>

👤 由 Autopilot 按照手动步骤在应用上操作

▶️ 在测试用例上选择 **Run Autonomously**（自主运行）

</div>

<div class="feature" markdown>
<span class="f-icon">⏳</span>
<span class="f-title" markdown="span">待执行（Pending）</span>

👤 暂时还没人执行。每个测试用例的结果都是 *None*（无），方便你稍后分批或逐个运行

▶️ **Execute** > **Pending**（执行 > 待执行）

</div>

</div>

!!! info "本地运行与执行的区别"
    在 Studio 的 **Test Explorer** 中运行，是给你自己在构建过程中用的。这些运行只存在于你的 Studio 会话中，关掉就没了。而 Test Manager 中的执行是给整个团队看的：它们会被保存下来，与需求关联，并附带证据。接下来你将通过测试集来创建执行。

## 🔎 探索 Execution 选项卡 { #explore-the-execution-tab }

到目前为止你运行过的所有内容，都在 Test Manager 中留下了记录。在你的项目中，从左侧菜单选择 **Execution**（执行），四处看看：

1. **列表。** 找到目前为止的所有执行及其类型：你的自主运行，以及任何手动或自动化运行。
2. **一次执行。** 打开你的自主运行，查看每个测试用例的结果、由谁运行、何时运行。
3. **测试用例日志。** 打开测试用例日志，逐条阅读每个步骤及其结果，并打开作为证据附上的截图。
4. **从需求出发。** 在 **Requirements**（需求）下，打开你的测试用例所覆盖的需求，找到覆盖它的各个测试用例的最新结果。这就是你在需求和测试用例阶段建立起来的可追溯性。

## ✋ 手动运行测试用例 { #run-a-test-case-manually }

在自主执行旁边再添加一次手动执行，这样你就能对比人和 Autopilot 是如何记录同一个测试的。

1. 在 Test Manager 中，打开你自主运行过的那个测试用例。
2. 选择 **Execute** > **Manually**。如果浏览器询问，请允许 Test Manager 弹出窗口：**Manual Execution Assistant** 会在新窗口中打开。
3. 亲自在 UiBank 上执行每个步骤，并将其标记为 **Passed**（通过）或 **Failed**（失败）。如果某处与预期结果不一致，就添加一条备注。
4. 如果连续好几个步骤都通过了，可以选择 **Set Passed Till Here**（到此处均设为通过），不必一个个去标记。
5. 选择 **Done**（完成）。新的手动执行会出现在 **Execution** 选项卡中，就在自主执行旁边。

!!! tip "对比一下两者"
    把两次执行并排打开。你和 Autopilot 在每个步骤上的结果都一致吗？如果有分歧，就看看 Autopilot 在该步骤的截图：它准确展示了 Autopilot 当时看到的画面。

## 🧭 筛选、查找与重新执行 { #filter-find-and-re-execute }

1. **筛选。** 在 **Execution** 选项卡中按结果筛选列表，例如只看失败的。
2. **用 Autopilot Search 查找。** 用自然语言（英文）描述你要找的执行，例如：

    ```text
    executions with failed test cases this week
    ```

3. **重新执行。** 打开一次执行，选择 **More Options**（更多选项）或 **Tasks**（任务），然后选择 **Re-execute manually**（手动重新执行）或 **Re-execute automated**（自动化重新执行）。Test Manager 会再次运行相同的测试用例，你无需做任何设置。重新执行不会显示活动覆盖率。

## ⏳ 为什么我的执行一直是 Pending？ { #why-does-my-execution-stay-pending }

以 **Pending** 方式启动的执行，按设计每个测试用例都显示 *None*。在你执行它之前，什么都不会运行。但如果是**自动化**或**自主**执行一直停留在 Pending，那就是另一回事了：没有任何东西接手它。

!!! warning "自动化和自主运行需要文件夹中有无人值守机器人"
    Test Manager 会把自动化和自主执行作为作业在 Orchestrator 中运行，所在位置是项目的默认文件夹 **{{ training_folder }}**。只有当一个连接到 Orchestrator 的**无人值守机器人**能访问该文件夹时，作业才会启动。有两种配置看起来已经连上了，但其实不会接手作业：

    - **Serverless。** 发送到 **Default Serverless** 机器模板的运行，由于没有运行时槽位，会一直停在 Pending，而且不报任何错误。
    - **你的个人工作区机器人。** Studio 登录时使用的机器人服务的是你的个人工作区，而不是 **{{ training_folder }}**。

    **怎么办：**

    1. 告诉讲师：共享文件夹中的机器人是为所有人准备好的。
    2. 一旦有机器人可用，就**停止这次待执行的执行，然后重新运行**。Orchestrator 不会重新检查已经处于 Pending 的作业，所以即使机器人空闲下来，旧作业也会一直等下去。

## 💻 进阶练习：用编码智能体读取执行 { #stretch-read-executions-with-your-coding-agent }

你的编码智能体可以通过 `uip` CLI（命令行）读取同样的执行，并把它们整理成摘要，或生成供 CI 流水线使用的文件。在 Studio 的 **Terminal**（终端）面板中启动你的编码智能体，并给它下面这段提示词：

```text
In my {YourName}_UIB_Test Test Manager project (prefix UIB), summarise the
latest execution: its type, the result per test case, and which steps
failed, with links to their screenshots. Then download its JUnit XML
results into ./results. Confirm `uip login status` first.
```

编码智能体会加载 `uipath-test` 技能，并运行 `uip tm executions list`、`uip tm executions testcaselogs list` 和 `uip tm result download` 等命令。

!!! info "出现 \"Tool 'tm' … is not discoverable\"？"
    你的机器上还没有安装 `uip` CLI 的 Test Manager 部分。错误信息里会给出安装命令。让你的编码智能体运行它，然后再试一次提示词。
