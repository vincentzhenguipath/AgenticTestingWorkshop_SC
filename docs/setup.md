课程开始前
{: .eyebrow }

# 🧰 环境准备 { #setup }

**工作坊开始前需要安装的所有内容都在这里。请从上到下依次完成——每一节都会先自行验证，再进入下一步。**

!!! info "请在课程开始前完成"
    在一台全新的电脑上，环境准备大约需要 45 分钟，而且有些下载文件比较大。请提前搞定，把课堂时间留给动手实践。

!!! tip "培训环境"
    请访问 **[{{ training_url }}]({{ training_url }})**，使用租户 **{{ training_tenant }}** 登录。

## 📦 1. 前提条件 { #1-prerequisites }

**Node.js（LTS）**——UiPath CLI（命令行）的运行依赖。

1. 从 **[nodejs.org](https://nodejs.org)** 下载 LTS 版本
2. 运行 `node --version` 和 `npm --version` 进行验证

!!! tip "npm 版本必须为 11.x.x"
    如果 `npm --version` 返回的是其他版本，请升级：

    === "Windows"
        ```bash
        npm install --global npm@11
        ```

    === "Mac"
        ```bash
        npm install -g npm@11
        ```

**安装了 UiPath 扩展的 Google Chrome**——测试用例会在 Chrome 中操作 UiBank。

1. 如果还没有，请先安装 **[Google Chrome](https://www.google.com/chrome/)**
2. 从 Chrome 网上应用店安装 **UiPath Browser Automation** 扩展，或者在 Studio 中通过 **Home** > **Tools** > **UiPath Extensions** > **Chrome**（主页 > 工具 > UiPath 扩展 > Chrome）安装
3. 在 Chrome 中打开 `chrome://extensions`，确认该扩展已 **enabled**（启用）

**.NET SDK 8.0**——构建和运行 UiPath Studio 项目所必需。

1. 从 **[dotnet.microsoft.com/download/dotnet/8.0](https://dotnet.microsoft.com/download/dotnet/8.0)** 下载；Mac 用户也可以通过 Homebrew 安装：
   ```bash
   brew install --cask dotnet-sdk
   ```
2. 运行 `dotnet --list-sdks` 验证——输出中应能看到 `8.x.x`

!!! tip "Windows——确保 .NET 已加入 PATH"
    如果安装后系统无法识别 `dotnet`，请在 PowerShell 中手动将其加入 PATH：
    ```bash
    $env:Path = "C:\Program Files\dotnet;$env:Path"
    dotnet --list-sdks
    ```

**UiPath Studio**——用于运行和调试生成的测试用例；当编码智能体无法捕获 UI 目标时，也可以用 **Indicate**（指定）手动捕获。目前仅支持 Windows，Mac 版本即将推出。

1. 从 **[uipath.com/start-trial](https://www.uipath.com/start-trial)** 下载
2. 使用你的 UiPath 账号登录，并确认 Studio 能正常启动

**Git**——UiPath skills（UiPath 技能）市场所必需。先试方法 1；如果不行，再用方法 2。

=== "方法 1：winget（最快）"

    1. 打开终端并运行：
       ```bash
       winget install --id Git.Git -e --source winget
       ```
    2. 如果提示接受条款，输入 `Y` 并按回车。
    3. 等出现 "Successfully installed" 后，关闭窗口。

=== "方法 2：下载安装程序"

    1. 访问 **[git-scm.com/download/win](https://git-scm.com/download/win)**——64 位安装程序应该会自动开始下载。
    2. 运行下载的文件（例如 `Git-2.xx.x-64-bit.exe`）。如果 Windows 请求管理员权限，点击 Yes（是）。
    3. 一路接受所有默认设置。在 **"Adjusting your PATH environment"**（调整 PATH 环境变量）界面，确保选中的是中间那个选项：*"Git from the command line and also from 3rd-party software"*——这也是默认选项。
    4. 完成后点击 Finish（完成）。

!!! warning "两种方法都必须做"
    PATH 的修改只会在新打开的窗口中生效。请关闭所有已打开的终端，然后打开一个新的命令提示符进行验证：
    ```bash
    git --version
    ```
    你应该会看到类似 `git version 2.45.1.windows.1` 的输出。

## 🤖 2. 安装编码智能体 { #2-install-a-coding-agent }

任选一个——装多个也没问题：

=== "Claude Code"

    ```bash
    npm install -g @anthropic-ai/claude-code
    ```

    验证：`claude --version`

    !!! tip "Claude Code 安装出错？"
        如果安装因脚本权限错误而失败，请运行：
        ```bash
        npm config set allow-scripts=@anthropic-ai/claude-code --location=user
        ```
        然后重新运行安装命令：
        ```bash
        npm install -g @anthropic-ai/claude-code
        ```

    !!! tip "Mac 上遇到 npm 权限错误？"
        通常是因为在没有写权限的情况下进行了全局安装。把 npm 指向一个你自己拥有的文件夹：
        ```bash
        mkdir -p ~/.npm-global
        npm config set prefix ~/.npm-global
        echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
        source ~/.zshrc
        ```

=== "Codex"

    ```bash
    npm install -g @openai/codex
    ```

    验证：`codex --version`

    !!! tip "Mac 上遇到 npm 权限错误？"
        通常是因为在没有写权限的情况下进行了全局安装。把 npm 指向一个你自己拥有的文件夹：
        ```bash
        mkdir -p ~/.npm-global
        npm config set prefix ~/.npm-global
        echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
        source ~/.zshrc
        ```

=== "Cursor"

    Cursor 既有编辑器版本，也有终端智能体版本。两个都装上——你会在编辑器里查看生成的文件，在终端里运行智能体。

    1. 从 **[cursor.com/downloads](https://cursor.com/downloads)** 下载并安装 **Cursor** 编辑器，然后登录。
    2. 安装 **Cursor CLI**：

        Mac：

        ```bash
        curl https://cursor.com/install -fsS | bash
        ```

        Windows（PowerShell）：

        ```powershell
        irm 'https://cursor.com/install?win32=true' | iex
        ```

    3. 打开一个新终端并登录：

        ```bash
        cursor-agent login
        ```

    验证：`cursor-agent --version`

    !!! tip "找不到 `cursor-agent`？"
        安装程序会把 CLI 放在 `~/.local/bin` 中。请打开一个新终端，或者把该文件夹加入 `PATH`。

## ⌨️ 3. 安装 UiPath CLI { #3-install-the-uipath-cli }

```bash
npm install -g @uipath/cli@latest
```

验证：`uip --version`——应显示 `1.195.1` 或更高版本。

## 🧩 4. 将 UiPath Skills 安装到编码智能体中 { #4-install-uipath-skills-into-your-coding-agent }

=== "Claude Code"

    ```bash
    # 1. 添加市场（只需一次）
    claude plugin marketplace add https://github.com/UiPath/skills
    # 2. 从市场安装插件
    claude plugin install uipath@uipath-marketplace
    uip skills install
    ```

=== "Codex"

    ```bash
    # 1. 添加市场（只需一次）
    codex plugin marketplace add UiPath/skills --ref main
    uip skills install
    ```

=== "Cursor"

    Cursor 从你打开的项目中读取技能，所以要在项目文件夹内安装：

    ```bash
    uip skills install --agent cursor --local
    ```

    在工作坊文件夹中运行该命令后，技能会被放到 `workshop/.cursor/skills/` 下。课程中每用到一个新的项目文件夹，都要在其中重新运行一次这条命令。

你应该会看到类似下面的输出：

```json
{
  "Result": "Success",
  "Code": "SkillsInstall",
  "Data": {
    "RootDir": "/Users/YourUser",
    "Skills": [
      "uipath-admin",
      "uipath-agents",
      "uipath-aops",
      "uipath-api-workflow",
      "uipath-automation-discovery",
      "uipath-automationhub",
      "uipath-connector-builder",
      "uipath-feedback",
      "uipath-functions",
      "uipath-governance",
      "uipath-human-in-the-loop",
      "uipath-insights",
      "uipath-ixp",
      "uipath-maestro-bpmn",
      "uipath-maestro-case",
      "uipath-maestro-flow",
      "uipath-mcp-servers",
      "uipath-planner",
      "uipath-platform",
      "uipath-process-mining",
      "uipath-review",
      "uipath-rpa",
      "uipath-solution",
      "uipath-tasks",
      "uipath-test",
      "uipath-troubleshoot"
    ],
    "Agents": [
      "claude",
      "codex",
      "cursor"
    ],
    "Installed": 78,
    "Shadowed": [],
    "Conflicts": []
  }
}
```

`Agents` 列出了已安装技能的编码智能体。随着 UiPath 不断新增技能，技能列表也会变长，所以你看到的可能比示例更多。

请确认输出中包含以下三个技能——动手实践环节要靠它们：

- `uipath-test`——Test Manager：需求、测试用例、测试集、执行、报告
- `uipath-rpa`——Studio 测试自动化项目和 XAML 测试用例
- `uipath-platform`——Orchestrator：包、文件夹、凭据资产

!!! info "每个技能到底懂些什么"
    完整的技能目录以及技能如何被发现，请参阅[智能体测试与编码智能体](what-is-a-coding-agent.md)。

## 🔐 5. 登录你的租户 { #5-authenticate-with-your-tenant }

本工作坊运行在 **{{ env_label }}** 上，这里提供最新的 Autopilot for Testers 和 Autopilot for Developers 功能。把 CLI 指向这里：

```bash
uip login --authority {{ training_authority }} --organization {{ training_org }} -t {{ training_tenant }}
```

验证你连接的是正确的位置：

```bash
uip login status --output json
```

然后在浏览器中打开 **[{{ training_url }}]({{ training_url }})**，进入一次 **Test Manager**，确认能看到 **Projects**（项目）页面。如果看不到，请在课程开始前请讲师为你开通访问权限。

## 🔗 6. 将 Studio 连接到培训租户 { #6-connect-studio-to-the-training-tenant }

Studio 中的 Autopilot 使用的是 Studio 当前登录的租户。请让 Studio 登录到与 CLI 相同的位置：

1. 打开 **Studio**。如果你已登录到其他环境（例如 `cloud.uipath.com`），请先退出登录。
2. 重新登录之前，把云端 URL 改为 `{{ training_authority }}`。在 **UiPath Assistant** 中，它位于 **Preferences** > **Orchestrator Settings**（首选项 > Orchestrator 设置）下的 **Service URL**（服务 URL）。
3. 登录后，选择组织 **{{ training_org }}** 和租户 **{{ training_tenant }}**。
4. 确认 Studio 中可以使用 **Autopilot** 面板。如果没有，请在课程开始前联系讲师——动手实践就是从它开始的。

!!! warning "所有工具使用同一个环境"
    Studio、`uip` CLI 和浏览器都必须指向 **{{ training_url }}**。只要其中一个还停留在其他环境，Autopilot 就会把需求保存到一个编码智能体看不到的项目里。

## 🏦 7. 注册你的 UiBank 测试用户 { #7-register-your-uibank-test-user }

测试用例会以一个已注册的 UiBank 用户身份登录。现在就创建你的账号，让测试有账号可用。

1. 访问 **[uibank.uipath.com/register-account](https://uibank.uipath.com/register-account)**。
2. 填写表单：名、中间名、姓、性别、邮箱、用户名和密码。请使用一个你在其他地方都没用过的密码——UiBank 是一个公开的演示网站。
3. 注册后，在 **[uibank.uipath.com/login](https://uibank.uipath.com/login)** 登录，确认账号可用。

测试永远不会把你的密码存放在项目中，而是从 Orchestrator 的 **credential asset**（凭据资产）中读取。创建一个空的工作坊文件夹，在其中启动编码智能体（参见[第 9 节](#9-start-a-session)），然后输入以下提示词：

```text
Create a credential asset named {YourName}_UiBankCredential in the
{{ training_folder }} folder on the {{ training_tenant }} tenant, with my UiBank username.
Ask me for the password interactively — don't put it in a command I can see
in my shell history.
```

更喜欢手动操作？在 **Orchestrator** 中打开 `{{ training_folder }}` 文件夹，进入 **Assets**（资产），添加一个同名的 **Credential**（凭据）资产。

!!! warning "记下你的 UiBank 邮箱"
    动手实践中你会把它用作 `var_LoanEmail`——第 6 步的个人资料检查会将它与 UiBank 显示的邮箱进行比对。

## 📄 8. 下载设计文档 { #8-download-the-design-document }

将[设计文档](resources.md#the-design-document)下载到你的工作坊文件夹中。目录结构应如下所示：

```text
workshop/
└── E2E UiBank Online Banking.docx   ← 设计文档
```

你会在课程开始时创建自己的 Test Manager 项目和 Studio 项目。

## ▶️ 9. 启动会话 { #9-start-a-session }

```bash
cd workshop && claude
# 或
cd workshop && codex
# 或
cd workshop && cursor-agent
```

想用 Cursor 编辑器而不是终端？在 Cursor 中打开 `workshop` 文件夹，使用 **Agent**（智能体）聊天——它能看到同样的技能。

技能会在会话启动时自动被发现。让智能体在 Test Manager 中创建一个测试用例，它就会自动加载合适的技能。

!!! success "环境准备完成"
    Node.js、.NET、已登录 {{ training_tenant }} 的 Studio、安装了 UiPath 扩展的 Chrome、Git、编码智能体、`uip` CLI、UiPath skills、已登录的租户、UiBank 测试用户，以及设计文档——全部就位。开始测点东西吧！
