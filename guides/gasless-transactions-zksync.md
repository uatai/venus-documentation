本指南将引导你完成在 ZKsync 上使用 金星 协议的步骤，无需使用 ETH 支付 Gas 费用，这得益于 [Zyfi Paymaster](https://www.zyfi.org/) 的集成。所有交易都将由 Zyfi Paymaster 赞助，因此你可以专注于使用该协议，而无需担心 Gas 费用。

## 分步指南

### 步骤 1：在 金星 上连接到 ZKsync

1. 打开 [金星应用app](https://app.venus.io) 并连接你的钱包。

2. 确保你已连接到 ZKsync 网络。如果未连接，请将钱包的网络切换到 ZKsync。

<figure><img src="../.gitbook/assets/gasless-zksync-network-selection.png" alt="选择 ZKsync 网络"><figcaption>选择 ZKsync 网络</figcaption></figure>

### 步骤 2：与 金星 协议交互

在本示例中，我们将批准使用 ZK 市场作为抵押品。

1. 导航至 金星 上的 ZK 市场。

2. 点击“抵押品”以启用将此市场用作抵押品。

<figure><img src="../.gitbook/assets/gasless-zksync-features.png" alt="与 ZKsync 上的任何功能交互"><figcaption>与 ZKsync 上的任何功能交互</figcaption></figure>

### 步骤 3：签署交易

1. 系统将提示你**签署消息**，而不是发送典型的交易。此步骤授权 Zyfi 代表你支付交易的 gas 费用。

2. 在你的钱包中签署消息。交易的 gas 费用将由 Zyfi Paymaster 支付，因此你的钱包**无需持有 ETH**。

3. 签署完成后，Zyfi 将处理交易，并通过其金库支付 gas 费用，并将交易发送到 ZKsync 区块链。

<figure><img src="../.gitbook/assets/gasless-zksync-rabby.png" alt="使用 Rabby 签署消息，而不是发送交易"><figcaption>使用 Rabby 签署消息，而不是发送交易</figcaption></figure>

<figure><img src="../.gitbook/assets/gasless-zksync-metamask.png" alt="使用 Metamask 签署消息，而不是发送交易"><figcaption>使用 Metamask 签署消息，而不是发送交易</figcaption></figure>

### 查看交易

你可以在 [ZKsync Explorer](https://explorer.zksync.io/) 上验证交易。交易将显示 Zyfi 作为支付方，用于支付 gas 费用。