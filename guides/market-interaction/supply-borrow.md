# 资产买卖

本指南将重点介绍如何使用 金星协议 赚取利息和借入资产。如果您想更深入地了解其底层技术原理，请参阅 金星协议 白皮书（https://github.com/VenusProtocol/venus-protocol-documentation/blob/main/whitepapers/Venus-whitepaper-v4.pdf）。

在 MetaMask（https://metamask.io）或其他支持的钱包应用上创建 Web3 钱包后，打开 金星 应用（https://app.venus.io）。界面会提示您连接 Web3 钱包。将钱包连接到 金星协议 后，你就可以授权交易、查看余额以及执行其他重要操作。

成功连接钱包后，你将可以访问 金星协议 界面的所有功能。在“仪表盘”菜单中，您可以找到所有交易市场。点击其中一个市场，会弹出一个新窗口，方便您与所选市场进行交互。请确保您位于“供应”或“借贷”选项卡下，具体取决于您想要执行的操作。

## 供应资产以赚取利息

1. 将你的 MetaMask Web3 钱包或其他支持的钱包应用程序连接到 金星 应用程序 ([https://app.venus.io](https://app.venus.io))。

2. 导航至“仪表盘”菜单，选择您要供应的资产。例如，如果你想供应 TRX，请点击 TRX 市场。

3. 启用该资产。你的钱包会收到交易确认信息。请注意，交易会产生少量 Gas 费，因此请确保您的钱包中有一些本地代币（例如，BNB 链需要 BNB，以太坊链需要 ETH）。

4. 指定你要供应的数量。所选资产将直接从你的钱包转移到 金星 协议，并立即赚取利息。此利息将自动添加到您的供应余额中。

## 管理您的借贷限额

你在 金星协议 上的借贷限额取决于您提供的资产。以下步骤将指导您如何管理借贷限额：

1. 导航至“账户”部分。

2. 在这里，你可以找到每个资产池的借贷限额，该限额以您提供的资产总价值的百分比表示。

3. 要调整此限额，你可以提供更多资产或偿还部分未偿还贷款。

## 在 金星协议 上借入资产

提供资产后，您可以在借贷限额内借入其他资产：

1. 从“仪表盘”菜单中，选择您要借入的资产。

2. 输入您要借入的金额并确认交易。

## 挖矿获取 $XVS 代币

除了通过提供资产赚取利息外，您还可以挖矿获取 $XVS 代币：

1. 在“金库”部分，您可以质押您的 XVS 或 VAI 代币以赚取 XVS 代币。

2. 点击“质押”。系统会提示您在钱包中确认交易。

## 借贷示例

假设你向 金星 提供 1000 个 TRX，vTRX/TRX 汇率为 0.0204。您将获得约 49,019 个 vTRX 作为回报 (1000 / 0.0204)。如果一年后 vTRX/TRX 汇率上涨至 0.0215，您的 49,019 个 vTRX 将增值至 1021.5 个 TRX (49,019 * 0.0215)，增值 21.5 个 TRX。

请记住，这些 vToken 代表你在 金星协议 中的抵押品。如果您有未结清的贷款，切勿交易或转移这些 vToken，因为它们是维持您的借款限额所必需的。

## WETH

ETH 是以太坊区块链的原生代币，例如用于支付 gas 费用。WETH 是一种 [ERC-20](https://ethereum.org/developers/docs/standards/tokens/erc-20) 代币，代表 ETH。大多数 Web3 应用（包括 Venus）都兼容 ERC-20 代币，因此需要将 ETH 转换为 WETH。

ETH 到 WETH 和 WETH 到 ETH 的转换始终在 WETH 代币本身中可用，兑换率始终为 `1:1`：

* 如果您包装 1 个 ETH，您将获得 1 个 WETH。

* 如果您解包 1 个 WETH，您将获得 1 个 ETH。

您只需支付执行 Wrap/Unwrap 交易所需的 Gas 费。每个以太坊网络（包括 L2 层）都有其自身的 WETH 代币（完整列表请参见 CoinMarketCap 上的链接：[CoinMarketCap](https://coinmarketcap.com/currencies/weth/))）。

使用 Uniswap 可以轻松地从 ETH 获取 WETH。例如，在以太坊主网上，操作步骤如下：

1. 访问 [Uniswap 以太坊 ETH Wrap 页面](https://app.uniswap.org/swap?chain=mainnet&inputCurrency=ETH&outputCurrency=0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)。

2. 连接您的钱包。

3. 输入您要 Wrap 的 ETH 数量。

4. 点击“Wrap”。

5. 在您的 Web3 钱包中查看并确认交易。

6. 记得将 WETH 代币添加到您的 Web3 钱包中，以便查看您的 WETH 余额。

<figure><img width="75%" src="../../.gitbook/assets/wrap_eth_uniswap.png" alt="Wrap ETH at Uniswap"><figcaption>在 Uniswap 上封装 ETH</figcaption></figure>

要解包 WETH 代币（获得 ETH），您还可以使用 [Uniswap](https://app.uniswap.org/swap?chain=mainnet&inputCurrency=0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2&outputCurrency=ETH)，只需切换输入和输出货币即可。

<figure><img width="75%" src="../../.gitbook/assets/unwrap_eth_uniswap.png" alt="Unwrap ETH at Uniswap"><figcaption>在 Uniswap 上解封 ETH</figcaption></figure>