动手实践 · 第 1 部分（共 4 部分）
{: .eyebrow }

# 📋 需求 { #requirements }

<div style="font-size: 15px; font-style: italic; color: #d1603a; margin: -0.6rem 0 1rem;">从设计文档到你愿意签字确认的需求</div>

<div style="background: #faf8f6; border: 1px solid #eee3dc; border-left: 4px solid #FA4616; padding: 18px 22px; margin: 1.4rem 0;">
  <div style="font-size: 14px; font-weight: 700; letter-spacing: 0.09em; color: #FA4616; margin-bottom: 9px;">你需要准备</div>
  <ul style="margin: 0; padding-left: 18px; font-size: 15px; color: #4a4a4a; line-height: 1.55;"><li style="margin-bottom: 5px;">在 <strong>Studio</strong> 中打开你的 <code>{YourName}UiBankTests</code> 项目，并已连接到你的 <strong>{YourName}_UIB_Test</strong> Test Manager 项目。参见<a href="../agentic-testing-hands-on/#setup">环境准备</a>。</li><li style="margin-bottom: 5px;">在浏览器中打开同一租户上的 <strong>Test Manager</strong>。</li></ul>
</div>

## 🪄 让 Studio 中的 Autopilot 创建需求 { #ask-autopilot-in-studio-to-create-the-requirements }

设计文档进去，需求出来，全程没人需要手敲一个字。

1. 在 Studio 中打开 **Autopilot** 面板。
2. 将 `E2E UiBank Online Banking.docx` 附加到对话中，然后给 Autopilot 输入以下提示词：

    ```text
    Generate the requirements for the UiBank web application from the
    attached design document. Create one requirement per step in section 3,
    Step 0 to Step 7, in that order.
    ```

3. 查看 Autopilot 给出的方案，然后接受这些需求，将它们保存到你的 Test Manager 项目中。

!!! warning "找不到 Autopilot，或者无法保存需求？"
    通常有两个原因。一是 Studio 登录到了错误的环境：本次课程中的 Autopilot 功能位于 **{{ env_label }}**，因此请让 Studio 登录到 **{{ training_authority }}**，组织 **{{ training_org }}**，租户 **{{ training_tenant }}**。二是项目没有连接到你的 Test Manager 项目：请在 Studio 中检查 Test Manager 设置，或者让你的编码智能体在项目文件夹中运行 `uip rpa tm status`。

## 💬 在 Test Manager 中讨论需求 { #discuss-the-requirements-in-test-manager }

在 Test Manager 中刷新 **Requirements**（需求）。你应该能看到八条需求，对应设计文档的每一个步骤，键值从 `UIB:1` 到 `UIB:8`。Autopilot 生成的名称和措辞可能与下面略有不同：

<div class="circles" markdown>

<div class="circle-item" markdown>
<span class="num">0</span>
<div class="ci-body" markdown>

**Login and Initial Account State**

`UIB:1` · Step 0

</div>
</div>

<div class="circle-item" markdown>
<span class="num">1</span>
<div class="ci-body" markdown>

**Checking Account Creation**

`UIB:2` · Step 1

</div>
</div>

<div class="circle-item" markdown>
<span class="num">2</span>
<div class="ci-body" markdown>

**Savings Account Creation**

`UIB:3` · Step 2

</div>
</div>

<div class="circle-item" markdown>
<span class="num">3</span>
<div class="ci-body" markdown>

**Funds Transfer Between Accounts**

`UIB:4` · Step 3

</div>
</div>

<div class="circle-item" markdown>
<span class="num">4</span>
<div class="ci-body" markdown>

**Loan Application Submission**

`UIB:5` · Step 4

</div>
</div>

<div class="circle-item" markdown>
<span class="num">5</span>
<div class="ci-body" markdown>

**Loan Status Lookup**

`UIB:6` · Step 5

</div>
</div>

<div class="circle-item" markdown>
<span class="num">6</span>
<div class="ci-body" markdown>

**User Profile Identity Verification**

`UIB:7` · Step 6

</div>
</div>

<div class="circle-item" markdown>
<span class="num">7</span>
<div class="ci-body" markdown>

**Logout and Evidence Collection**

`UIB:8` · Step 7

</div>
</div>

</div>

打开其中两三条，大家一起讨论：

- **可追溯性。** 你能从每条需求看出它来自文档的哪个步骤吗？
- **可测试性。** 你能为每一条验收标准写出明确的通过/失败检查吗？哪些写得含糊不清？
- **遗漏。** 文档没有说明转账金额超过余额时会怎样，也没有说明贷款审批规则是什么。Autopilot 注意到了吗，还是直接跳过了？它有没有编造文档里没写的内容？

!!! tip "为什么每个步骤对应一条需求"
    八条小需求比一条大需求更容易评估、覆盖和汇报。之后某个测试失败时，你能准确知道它影响的是哪个步骤、哪条需求。

## 🔍 用 Test Manager 中的 Autopilot 评估、改进、再评估 { #evaluate-improve-and-re-evaluate-with-autopilot-in-test-manager }

Test Manager 的 **Evaluation Agent**（评估智能体）会从清晰度、完整性和可测试性三个方面检查需求。

1. 在 **Requirements** 下打开 **Funds Transfer Between Accounts**。
2. 选择 **Description**（描述）旁边的 **Evaluate Requirement**（评估需求）。阅读 Autopilot 的发现和建议。

    ![Test Manager 中的一条需求「Step 3: Transfer Funds Between Accounts」，显示其描述，以及 Description 旁边的 Evaluate Requirement 按钮](requirements.images/test-manager-evaluate-requirement-W.png){ .screenshot width="900" }
    *资金转账需求，Description 旁边就是 Evaluate Requirement。*

3. 挑两三条你认同的建议，通过编辑需求来落实。一个典型的例子是：为转账金额超过转出账户余额的情况补充一条规则。如果文档回答不了某个问题，就把它记为待解决问题，而不是自己编一个答案。
4. 再次评估这条需求。结果有改善吗？Autopilot 有没有提出新的问题？
5. 对 **Loan Application Submission** 重复上述步骤，这是未记录规则最多的一条需求。

!!! tip "添加你自己的提示词"
    Autopilot 使用项目 **Prompt Library**（提示词库）中的提示词来评估需求。除了 **Multifaceted Audit**（多维度审核）、**Performance Evaluation**（性能评估）和 **Security Assessment**（安全评估）等预定义提示词之外，你还可以为团队自己的质量规则添加自定义提示词：

    1. 在 Test Manager 中，选择项目左侧菜单中的 **Project Settings**（项目设置），然后选择 **Prompt library**（提示词库）选项卡。
    2. 选择 **Add prompt**（添加提示词）。
    3. 在 **Create prompt**（创建提示词）中填写：
        - **Name**（名称）和 **Description**，让其他人知道什么时候该用它。
        - **Mode of use**（使用模式）：评估类提示词选择 **Evaluate requirement quality**（评估需求质量）。其他模式还包括 **Create tests from requirement**（根据需求创建测试）、**Import test cases**（导入测试用例）和 **Autonomous Exploration**（自主探索）。
        - **Prompt**（提示词）：给 Autopilot 的指令，越具体、越详细越好。
    4. 选择 **Create**（创建）。

    之后，当你评估或重新评估需求时，你的提示词就会出现在预定义提示词旁边。

    <video src="../requirements.images/test-manager-add-custom-prompt.mp4" autoplay loop muted playsinline controls aria-label="在 Test Manager 中添加自定义提示词：Project Settings、Prompt library、Add prompt，填写 Name、Description、Mode of use 和 Prompt，然后点击 Create" style="display: block; width: 100%; margin: 1.5rem auto; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);"></video>

!!! success "需求完成"
    Autopilot 根据设计文档生成了八条需求，大家进行了讨论，并且至少有两条经过了评估、改进和再评估。

!!! info "Autopilot 起草，你来拍板"
    Evaluation Agent 很擅长发现含糊的措辞和遗漏的场景，但它不可能了解你的业务规则。你接受的每一条建议，都是在决定 UiBank 必须做什么，所以应当得到产品负责人的认可。
