资源
{: .eyebrow }

# 📚 资源 { #resources }

**课程期间和课程结束后都值得随手备着的参考资料与链接。**

!!! tip "培训环境"
    请访问 **[{{ training_url }}]({{ training_url }})**，使用租户 **{{ training_tenant }}** 登录。

## 📄 设计文档 { #the-design-document }

整个动手实践都从同一份文档开始：**E2E UiBank Online Banking**。下载后，将 `E2E UiBank Online Banking.docx` 保存到你的工作坊文件夹中。

[下载设计文档（.docx）](resources.assets/E2E%20UiBank%20Online%20Banking.docx){ .md-button .md-button--primary }

[动手实践页面](agentic-testing-hands-on.md#the-design-document)概括了文档中的各个步骤、由这些步骤转化而来的需求，以及测试数据。

## 🎁 讲师参考包 { #trainers-reference-package }

讲师提供的 `DemoUiBankTests` 是一个可直接运行的测试自动化项目，全部八个测试用例都已实现自动化。它已经发布到 `{{ training_folder }}` 文件夹中，所以如果你自己的自动化还没准备好，可以把它关联到你在 Test Manager 中的测试用例，并在[测试集](test-sets.md)中运行。

<div class="feature-grid" markdown>

<div class="feature" markdown>
<span class="f-icon">🎁</span>
<span class="f-title" markdown="span">`DemoUiBankTests`</span>

测试自动化项目，测试用例部分的参考答案

🧪 `T0_LoginAndInitialAccountState` 至 `T7_LogoutAndEvidenceCollection`

📁 `{{ training_folder }}` 文件夹

</div>

</div>

!!! info "是参考，不是捷径"
    请先自己构建测试用例。本课程的重点是亲眼看看 Autopilot 和你的编码智能体如何规划、自动化并运行它们。参考包是在你被卡住时救急用的，也可以在事后用来对照。

## 🔗 实用链接 { #useful-links }

<div class="link-grid" markdown>

<a class="link-card" href="https://github.com/UiPath/skills" target="_blank" rel="noopener"><span class="f-icon">🧩</span><span class="f-title">UiPath/skills</span><span class="f-text" markdown="span">技能仓库。建议读一读 `uipath-test` 和 `uipath-rpa` 的 `SKILL.md`。</span></a>
<a class="link-card" href="https://uibank.uipath.com" target="_blank" rel="noopener"><span class="f-icon">🏦</span><span class="f-title">UiBank</span><span class="f-text" markdown="span">被测的演示银行应用</span></a>
<a class="link-card" href="https://meera-uipath.github.io/software-testing-ilt-guide" target="_blank" rel="noopener"><span class="f-icon">🎓</span><span class="f-title">Test Cloud 与智能体测试 ILT 指南</span><span class="f-text" markdown="span">手把手的 Test Manager 和 Studio 课程：对象存储库、数据驱动测试、发布以及执行测试用例</span></a>
<a class="link-card" href="https://docs.uipath.com/test-manager" target="_blank" rel="noopener"><span class="f-icon">📋</span><span class="f-title">Test Manager 文档</span><span class="f-text" markdown="span">需求、测试用例、测试集、执行，以及 Autopilot for Testers</span></a>

</div>
