# 提交 VIP

### 概述

金星协议 的治理模型允许 XVS 代币持有者提出并投票表决 金星协议Venus 改进提案 (VIP)。以下是创建和提交提案的分步指南。

{% hint style="info" %}
请记住，您需要至少 30 万票的投票权重才能提交提案。
{% endhint %}

### 第一步：访问 金星协议Venus 治理门户

使用您常用的网络浏览器访问 金星协议Venus 治理门户。您可以通过以下网址访问该门户：[https://app.venus.io/governance](https://app.venus.io/governance).

### 第二步：连接您的钱包

要提交提案，你需要连接您的钱包。点击屏幕右上角的“连接钱包”按钮。此时会弹出一个菜单，列出金星协议治理门户支持的各种钱包。从菜单中选择您的钱包，然后按照说明将其连接到门户。

### 第三步：创建提案

钱包连接成功后，您就可以创建提案了。找到屏幕右上角的“创建提案”按钮并点击它。

<figure><img src="../../.gitbook/assets/VIP_create_proposal_3 (1).jpg" alt=""><figcaption></figcaption></figure>

此操作将打开一个模态框，其中包含两个选项——“上传文件”和“手动创建”：

<figure><img src="../../.gitbook/assets/VIP_create_modal_3.png" alt=""><figcaption></figcaption></figure>

### 第四步：上传提案文件

创建提案最快捷的方式是导入 VIP 文件。导入操作使用一个 JSON 文件，其中包含创建 VIP 所需的所有信息，例如提案的标题、类型、操作和参数。

金星协议 提供了一个用于生成 VIP 文件的工具，你可以在[此处](https://github.com/VenusProtocol/vips#create-proposal)找到它。你还可以[在此处](https://github.com/VenusProtocol/venus-protocol-interface/blob/main/src/assets/proposals/vip-123.json)查看一个有效的提案文件示例。请注意，所有字段都将根据其要求和类型进行验证。

#### 步骤 4.1：选择 VIP 文件

点击“上传文件”按钮，即可选择要上传的提案文件。上传完成后，系统将解析并验证文件，界面会报告任何可能存在的错误。

#### 步骤 4.2：确认提案

导入验证成功后，界面将显示所有 VIP 数据供你审核：

<figure><img src="../../.gitbook/assets/VIP_import_confirm_4-2.png" alt=""><figcaption></figcaption></figure>

如果一切无误，请点击弹窗底部的“创建”按钮，确认创建你的 VIP。

### 第五步：手动创建提案

你也可以点击“手动创建”按钮手动创建提案。

#### 第五步 5.1：选择提案类型

点击“手动创建”按钮后，将弹出一个新界面，提示您选择提案类型。请选择与你要提出的变更相关的提案类型。

<figure><img src="../../.gitbook/assets/VIP_select_type_5-1.jpg" alt=""><figcaption></figcaption></figure>

#### 步骤 5.2：输入提案信息

下一步是提供有关您提案的详细信息。这包括提案标题、简要描述以及指向与您的提案相关的链下讨论的链接。请确保您提供的信息清晰简洁，以便其他社区成员能够理解。

<figure><img src="../../.gitbook/assets/VIP_proposal_info_5-2.jpg" alt=""><figcaption></figcaption></figure>

#### 步骤 5.3：设置投票选项

在第三个屏幕中，您可以为投票选项（赞成、反对、弃权）指定描述。

<figure><img src="../../.gitbook/assets/VIP_voting_options_5-3.jpg" alt=""><figcaption></figcaption></figure>

#### 步骤 5.4：指定操作

接下来，添加提案获批后将要执行的操作。操作需要包含合约地址、函数签名和参数，以便正确创建。

<figure><img src="../../.gitbook/assets/VIP_actions_5-4.jpg" alt=""><figcaption></figcaption></figure>

#### 步骤 5.5：确认提案提交

最后，就像 VIP 导入后一样，您可以查看您的提案，确保所有细节准确无误。确认无误后，点击“提交”按钮提交您的提案。您将在已连接的钱包中看到确认提示。确认交易即可完成提案提交流程。

<figure><img src="../../.gitbook/assets/VIP_confirm_5-5.jpg" alt=""><figcaption></figcaption></figure>

恭喜！你已成功提交 金星协议Venus 改进提案。金星协议Venus 社区将审核你的提案并进行投票。请记住，你积极参与 金星协议Venus 协议的治理流程对其持续发展和成功至关重要。