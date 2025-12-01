# 弹性价格预言机

### 概述

在之前的版本中，金星协议 完全依赖 Chainlink 价格预言机来获取价格。这种依赖虽然通常可靠，但也造成了单点故障。如果没有辅助验证机制，错误或过时的价格可能会带来诸如不必要的清算或过度借贷等风险。

鉴于这些风险，金星协议 V4 引入了弹性价格预言机，这是一个更强大的系统，能够从多个数据源提取数据进行交叉验证。弹性预言机配备了一种算法，用于验证两个或多个数据源之间的价格一致性，从而在主要数据源不可靠或失效的情况下提供保障。

此外，改进后的预言机基础设施支持实时集成新的价格预言机，并允许为每个代币启用和禁用价格预言机。

### 主要特性

#### 弹性价格源

弹性价格源以更强大、更可靠的解决方案取代了 Comptroller 合约中使用的单一价格提供商。这一新组件不仅从各种链上数据源获取资产价格，还包含一个回退机制，以保护协议免受预言机故障的影响。目前，该功能集成了 Chainlink、RedStone、Pyth Network 和 Binance 预言机，未来可能会添加更多预言机。

#### 治理配置

金星协议 治理团队可以通过 金星 改进提案 (VIP) 对弹性价格源系统进行配置。这些配置包括预言机的暂停和恢复功能、价格源配置以及固定价格设置等。

### 安全措施

在实施弹性价格预言机的过程中，我们采取了多项安全措施，以确保 金星 协议的安全性和持续性：

* **价格持续性：** 我们在模拟环境中验证了升级前后的资产价格，以确保价格一致性。

* **测试网部署：** 预言机已在 金星 协议测试网环境中部署和测试。

* **审计：** 代码已通过 OpenZeppelin、Peckshield、Certik 和 Hacken 的审计。

<figure><img src="../.gitbook/assets/17b75928-d6a2-4207-9a0b-89d1d41690d4.png" alt=""><figcaption></figcaption></figure>

### 相关代币预言机

对于类似 Liquid Staked Tokens (LST) 的关联代币，最佳实践建议预言机首先使用智能合约报价来获取关联资产之间的汇率，然后将其乘以第二个代币的美元市场价格，从而完成计算。

在 Venus 中，我们为每种 LST 资产使用专用预言机来计算价格，具体步骤如下：

* 将 LST 转换为底层代币（使用 LST 合约提供的汇率）

* 使用基于市场价格的“传统”预言机，将上一步计算出的底层代币转换为美元

Venus 中当前相关的代币预言机列表如下：

* `AnkrBNBOracle`它返回 [ankrBNB](https://bscscan.com/address/0x52F24a5e03aee338Da5fd9Df68D2b6FAe1178827) 代币的美元价格，使用 ankrBNB 合约提供的汇率，在链上将 ankrBNB 转换为 BNB。

* `BNBxOracle`。它返回 [BNBx](https://bscscan.com/address/0x1bdd3Cf7F79cfB8EdbB955f20ad99211551BA275) 代币的美元价格，使用 [stake manager](https://bscscan.com/address/0x3b961e83400D51e6E1AF5c450d3C7d7b80588d28) 合约提供的汇率，在链上将 BNBx 转换为 BNB。 * `eBTCAccountantOracle`（`EtherfiAccountantOracle` 的实例）。它返回 [eBTC](https://etherscan.io/token/0x657e8C867D8B37dCC18fA4Caead9C45EB088C642) 代币的美元价格，使用 [Accountant](https://etherscan.io/address/0x1b293DC39F94157fA0D1D36d7e0090C8B8B8c13F) 合约中的汇率，在链上将 eBTC 转换为 WBTC。

* `PendleOracle`。它返回 PT Pendle 代币的美元价格，使用 Pendle 市场合约，在链上将 PT 代币转换为其底层代币。

* `SFraxOracle`。它返回 [sFRAX](https://etherscan.io/token/0xa663b02cf0a4b149d2ad41910cb81e23e1c41c32) 代币的美元价格，使用 sFRAX 合约提供的汇率在链上将 sFRAX 转换为 FRAX。

* `SlisBNBOracle`。它返回 [slisBNB](https://bscscan.com/address/0xB0b84D294e0C75A6abe60171b70edEb2EFd14A1B) 代币的美元价格，使用 [stake manager](https://bscscan.com/address/0x1adB950d8bB3dA4bE104211D5AB038628e477fE6) 合约提供的汇率，在链上将 slisBNB 转换为 BNB。

* `AsBNBOracle`。它返回 [asBNB](https://bscscan.com/address/0x77734e70b6E88b4d82fE632a168EDf6e700912b6) 代币的美元价格，使用 [asBNB 铸造者](https://bscscan.com/address/0x2F31ab8950c50080E77999fa456372f276952fD8) 合约提供的汇率，在链上将 asBNB 转换为 slisBNB。

* `StkBNBOracle`。它返回 [stkBNB](https://bscscan.com/address/0xc2E9d07F66A89c44062459A47a0D2Dc038E4fb16) 代币的美元价格，使用 [stake pool](https://bscscan.com/address/0xC228CefDF841dEfDbD5B3a18dFD414cC0dbfa0D8) 合约中的汇率，在链上将 stkBNB 转换为 BNB。

* `WBETHOracle`。它返回 [WBETH](https://bscscan.com/address/0xa2e3356610840701bdf5611a53974510ae27e2e1) 代币的美元价格，使用 WBETH 合约中的汇率，在链上将 WBETH 转换为 BNB。 * `WeETHOracle`。它返回 [weETH](https://etherscan.io/token/0xcd5fe23c85820f7b72d0926fc9b05b43e359b7ee) 代币的美元价格，使用 [流动性池](https://etherscan.io/address/0x308861A430be4cce5502d0A12724771Fc6DaF216) 合约中的汇率，将 weETH 在链上转换为 eETH，并假设 1 eETH = 1 ETH。

* `WeETHsOracle`（`WeETHAccountantOracle` 的实例）。它返回 [weETHs](https://etherscan.io/token/0x917ceE801a67f933F2e6b33fC0cD1ED2d5909D88) 代币的美元价格，使用 [Accountant](https://etherscan.io/address/0xbe16605B22a7faCEf247363312121670DFe5afBE) 合约中的汇率，将链上的 weETHs 转换为 WETH。

* `WstETHOracle`。它返回 [wstETH](https://etherscan.io/token/0x7f39c581f595b53c5cb19bd0b3f8da6c935e2ca0) 代币的美元价格，使用 [stETH](https://etherscan.io/token/0xae7ab96520de3a18e5e111b5eaab095312d7fe84) 合约中的汇率，将 wstETH 链上转换为 stETH，并假设 1 stETH = 1 ETH。

{% hint style="warning" %}

**关于流动性质押代币的假设**

`WeETHOracle` 和 `WstETHOracle` 假设流动性质押代币 (LST) 与基础资产之间的价格比率为 1:1（例如，1 ETH = 1 stETH）。这种方法的主要风险在于智能合约漏洞和交易对手风险，这些风险可能会影响LST的赎回流程。在交易对手风险较大的情况下，尤其是在底层代币无法用LST赎回的情况下，直接智能合约定价可能变得不可靠。以下是我们缓解此类情况的计划：

* 我们将为每个LST代币部署两个链上预言机：

* 第一个预言机将基于LST代币与底层资产1:1的比例假设返回价格。

* 第二个预言机将基于二级市场数据（例如使用Chainlink）返回价格。

* 默认情况下，

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | AAVE | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | ADA | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | asBNB | [AsBNBOracle](https://bscscan.com/address/0x52375ACab348Fa3979503EB9ADB11D74560dEe99) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | BCH | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | BETH (Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - |
| Core | BNB | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | BTCB | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | BUSD (Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | [Price fixed to $1](https://app.venus.io/#/governance/proposal/226?chainId=56) |
| Core | CAKE | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | DAI | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | DOGE | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | DOT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | ETH | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | FDUSD | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | FIL | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | LINK | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | lisUSD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Core | LTC | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | MATIC (Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | Price feed from [$POL](https://data.chain.link/feeds/bsc/mainnet/pol-usd) |
| Core | PT-sUSDE-26JUN2025 (Paused) | [PendleOracle-PT-sUSDe-26JUN2025](https://bscscan.com/address/0x176ca46D7DcB4e001b8ee5F12d0fcd6D279214f4) | - | - | |
| Core | SOL | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | SolvBTC | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | sUSDe | [sUSDeOneJumpRedstoneOracle](https://bscscan.com/address/0x2B2895104f958E1EC042E6Ba5cbfeCbAD3C5beDb) | [sUSDeOneJumpChainlinkOracle](https://bscscan.com/address/0xA67F01322AF8EBa444D788Ee398775b446de51a0) | [sUSDeOneJumpChainlinkOracle](https://bscscan.com/address/0xA67F01322AF8EBa444D788Ee398775b446de51a0) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | SXP(Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| Core | THE | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | TRX | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | - | Upper bound: 1.01. Lower bound: 0.99 |
| Core | TRXOLD(Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | - | Upper bound: 1.01. Lower bound: 0.99 |
| Core | TUSD | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | TUSDOLD (Paused) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| Core | TWT | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Core | UNI | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | USDC | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | USDe | [USDTChainlinkOracle](https://bscscan.com/address/0x22Dc2BAEa32E95AB07C2F5B8F63336CbF61aB6b8) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | Upper bound: 1.06. Lower bound: 0.94 |
| Core | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | USD1 | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | |
| Core | VAI | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | WBETH | [WBETHOracle](https://bscscan.com/address/0x49938fc72262c126eb5D4BdF6430C55189AEB2BA) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | XRP | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Core | xSolvBTC | [xSolvBTCOneJumpRedstoneOracle](https://bscscan.com/address/0xf5534f78Df9b610B19A63956d498d00CFaD8B9D3) | - | - | |
| Core | XVS | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | Upper bound: 1.05. Lower bound: 0.95 |
| Stablecoins | lisUSD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Stablecoins | USDD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Stablecoins | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Stablecoins | EURA | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| DeFi | BSW | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| DeFi | ALPACA | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| DeFi | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| DeFi | USDD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| DeFi | ANKR | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| DeFi | ankrBNB | [AnkrBNBOracle](https://bscscan.com/address/0x4512e9579734f7B8730f0a05Cd0D92DC33EB2675) | - | - | |
| DeFi | TWT | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| DeFi | PLANET | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| GameFi | RACA | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| GameFi | FLOKI | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| GameFi | USDD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| GameFi | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked BNB | ankrBNB | [AnkrBNBOracle](https://bscscan.com/address/0x4512e9579734f7B8730f0a05Cd0D92DC33EB2675) | - | |
| Liquid Staked BNB | asBNB | [AsBNBOracle](https://bscscan.com/address/0x652B90D1d45a7cD5BE82c5Fb61a4A00bA126dde5) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - |Upper bound: 1.05. Lower bound: 0.95|
| Liquid Staked BNB | BNBx | [BNBxOracle](https://bscscan.com/address/0xC2E2b6f9CdE2BFA5Ba5fda2Dd113CAcD781bdb31) | - | - | |
| Liquid Staked BNB | PT-clisBNB-24APR2025 | [PendleOracle-PT-clisBNB-25APR2025](https://bscscan.com/address/0xEa7a92D12196A325C76ED26DBd36629d7EC46459) | - | |
| Liquid Staked BNB | stkBNB | [StkBNBOracle](https://bscscan.com/address/0xdBAFD16c5eA8C29D1e94a5c26b31bFAC94331Ac6) | - | |
| Liquid Staked BNB | slisBNB | [SlisBNBOracle](https://bscscan.com/address/0xDDE6446E66c786afF4cd3D183a908bCDa57DF9c1) | - | - | |
| Liquid Staked BNB | WBNB | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| Meme | BabyDoge | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Meme | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Tron | BTT | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Tron | TRX | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| Tron | WIN | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | - | - | |
| Tron | USDD | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | - | - | |
| Tron | USDT | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | ETH | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Binance](https://bscscan.com/address/0x594810b741d136f1960141C0d8Fb4a91bE78A820) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | weETH | [weETHOneJumpRedstoneOracle](https://bscscan.com/address/0xb661102c399630420A4B9fa0a5cF57161e5452F5) | [weETHOneJumpChainlinkOracle](https://bscscan.com/address/0x3b3241698692906310A65ACA199701843404E175) | [weETHOneJumpChainlinkOracle](https://bscscan.com/address/0x3b3241698692906310A65ACA199701843404E175) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | wstETH | [wstETHOneJumpChainlinkOracle](https://bscscan.com/address/0x3C9850633e8Cb5ac5c3Da833C947E7c91EED15C4) | [wstETHOneJumpRedstoneOracle](https://bscscan.com/address/0x90dd7ae1137cC072F7740Ee0b264f2351515B98A) | [wstETHOneJumpRedstoneOracle](https://bscscan.com/address/0x90dd7ae1137cC072F7740Ee0b264f2351515B98A) | Upper bound: 1.01. Lower bound: 0.99 |
| BTC | BTCB | [RedStone](https://bscscan.com/address/0x8455EFA4D7Ff63b8BFD96AdD889483Ea7d39B70a) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | [Chainlink](https://bscscan.com/address/0x1B2103441A0A108daD8848D8F5d790e4D402921F) | Upper bound: 1.01. Lower bound: 0.99 |
| BTC | PT-SolvBTC.BBN-27MAR2025 | [PendleOracle-PT-SolvBTC.BBN-27MAR2025](https://bscscan.com/address/0xE11965a3513F537d91D73d9976FBe8c0969Bb252) | - | - | |

#### Ethereum

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | crvUSD | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | DAI | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | TUSD | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | USDC | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | USDT | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | WBTC | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | WETH | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | FRAX | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | LBTC | [LBTCOneJumpRedStoneOracle](https://etherscan.io/address/0x54B033D102db7DD734E0Ad649463E90fFA78D853) | - | - | |
| Core | EIGEN | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | sFRAX | [SFraxOracle](https://etherscan.io/address/0x1aDCE75BB3164bBf6060a4f44262df5414473110) | - | - | |
| Core | eBTC | [eBTCAccountantOracle](https://etherscan.io/address/0x04d6096A6F089047C7af6E4644D18fB766B8d4cE) | - | - | |
| Core | USDS | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | sUSDS | [sUSDS-ERC4646Oracle](https://etherscan.io/address/0xEC3865a8a5DCb8C507781DA17A38b754E3d01C50) | - | - | |
| Core | BAL | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Core | yvUSDC-1 | [yvUSDC-1-ERC4646Oracle](https://etherscan.io/address/0x49C6858B3ce4F3829b716fD3FafCa6Cb4Ccb7843) | - | - | |
| Core | yvUSDS-1 | [yvUSDS-1-ERC4646Oracle](https://etherscan.io/address/0x50f97063b4097D4e81C4DD9c3278258A04DF15aA) | - | - | |
| Core | yvUSDT-1 | [yvUSDT-1-ERC4646Oracle](https://etherscan.io/address/0xE113AE8D80Fb6dfB3221e0A396e297Aa42813d0A) | - | - | |
| Core | yvWETH-1 | [yvWETH-1-ERC4646Oracle](https://etherscan.io/address/0x641817dE6c0E4f763C393AaD182E6C946e1a2e2b) | - | - | |
| Core | sUSDe | [sUSDe-ERC4626Oracle](https://etherscan.io/address/0xaE847E81ff6dD2bdFB1fD563ccB4f848c74D2B70) | - | - | |
| Core | USDe | [RedStone](https://etherscan.io/address/0x0FC8001B2c9Ec90352A46093130e284de5889C86) | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | tBTC | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Curve | crvUSD | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Curve | CRV | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Ethena | PT-sUSDE-27MAR2025 | [PendleOracle-PT-sUSDe-27MAR2025](https://etherscan.io/address/0x51B83bbbdCa078b2497C41c9f54616D1aDBEF86F) | - | - | |
| Ethena | PT-USDe-27MAR2025 | [PendleOracle-PT-USDe-27MAR2025](https://etherscan.io/address/0x4CD93DcD2E11835D06a45F7eF9F7225C249Bb6Db) | - | - | |
| Ethena | sUSDe | [sUSDe-ERC4626Oracle](https://etherscan.io/address/0xaE847E81ff6dD2bdFB1fD563ccB4f848c74D2B70) | - | - | |
| Ethena | USDC | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Ethena | USDe | [RedStone](https://etherscan.io/address/0x0FC8001B2c9Ec90352A46093130e284de5889C86) | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | ezETH | [ezETHOneJumpRedstoneOracle](https://etherscan.io/address/0xA6efeF98D9C4E9FF8193f80FbABF92AD92D50500) | [ezETHOneJumpChainlinkOracle](https://etherscan.io/address/0x84FAe9909Fa1F259CB23Fa14FCdd1a35A0FE7EB8) | [ezETHOneJumpChainlinkOracle](https://etherscan.io/address/0x84FAe9909Fa1F259CB23Fa14FCdd1a35A0FE7EB8) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | PTweETH-26DEC2024 | [PendleOracle-PT-weETH-26DEC2024](https://etherscan.io/address/0xB89C0F93442C269271cB4e9Acd10E81D3fC237Ba) | - | - | |
| Liquid Staked ETH | pufETH | [pufETHOneJumpRedstoneOracle](https://etherscan.io/address/0xAaE18CEBDF55bbbbf5C70c334Ee81D918be728Bc) | - | - | |
| Liquid Staked ETH | rsETH | [rsETHOneJumpRedstoneOracle](https://etherscan.io/address/0x6AC694f2D118a35e1984AE590B916108F4f9337F) | [rsETHOneJumpChainlinkOracle](https://etherscan.io/address/0xc68A156b08C5C5C2e9c27B32A09977F3FA50FFE0) | [rsETHOneJumpChainlinkOracle](https://etherscan.io/address/0xc68A156b08C5C5C2e9c27B32A09977F3FA50FFE0) | Upper bound: 1.01. Lower bound: 0.99 |
| Liquid Staked ETH | sfrxETH | [SFrxETHOracle](https://etherscan.io/address/0x5E06A5f48692E4Fff376fDfCA9E4C0183AAADCD1) | - | - | |
| Liquid Staked ETH | WETH | [Chainlink](https://etherscan.io/address/0x94c3A2d6B7B2c051aDa041282aec5B0752F8A1F2) | - | - | |
| Liquid Staked ETH | wstETH | [WstETHOracle\_Equivalence](https://etherscan.io/address/0x6b51Ee3aF70b350AaADc05f418502b330c5Aad7c) | - | - | Assume 1:1 for ETH:stETH |
| Liquid Staked ETH | weETH | [WeETHOracle\_Equivalence](https://etherscan.io/address/0xaB663D4a701229DFF407Eb4B45007921029072e9) | - | - | Assume 1:1 for ETH:eETH |
| Liquid Staked ETH | weETHs | [WeETHAccountantOracle](https://etherscan.io/address/0x47F7A7f3486b08A019E0c10Af969ADC4B6E415Cd) | - | - | |

#### opBNB mainnet

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | BTCB | [Binance](https://opbnbscan.com/address/0xB09EC9B628d04E1287216Aa3e2432291f50F9588) | - | - | |
| Core | ETH | [Binance](https://opbnbscan.com/address/0xB09EC9B628d04E1287216Aa3e2432291f50F9588) | - | - | |
| Core | FDUSD | [Binance](https://opbnbscan.com/address/0xB09EC9B628d04E1287216Aa3e2432291f50F9588) | - | - | |
| Core | USDT | [Binance](https://opbnbscan.com/address/0xB09EC9B628d04E1287216Aa3e2432291f50F9588) | - | - | |
| Core | WBNB | [Binance](https://opbnbscan.com/address/0xB09EC9B628d04E1287216Aa3e2432291f50F9588) | - | - | |

#### Arbitrum One

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | WBTC | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | WETH | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | USDC | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | USDT | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | gmWETH-USDC | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | gmBTC-USDC | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Core | ARB | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |
| Liquid Staked ETH | weETH |  [weETHOneJumpChainlinkOracle](https://arbiscan.io/address/0x0afD33490fBcF537ede00F9Cc4607230bBf65774) | - | - | |
| Liquid Staked ETH | wstETH |  [wstETHOneJumpChainlinkOracle](https://arbiscan.io/address/0x17a5596DF05c7bfB2280D5B9cCcDAf711e957Ed4) | - | - | |
| Liquid Staked ETH | WETH | [SequencerChainlinkOracle](https://arbiscan.io/address/0x9cd9fcc7e3deda360de7c080590aad377ac9f113) | - | - | |

#### ZKsync Mainnet

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | WBTC | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | - | - | |
| Core | WETH | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | - | - | |
| Core | USDC | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | - | - | |
| Core | USDC\_E | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | - | - | |
| Core | USDT | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | - | - | |
| Core | ZK | [RedStoneOracle](https://explorer.zksync.io/address/0xFa1e65e714CDfefDC9729130496AB5b5f3708fdA) | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | [ChainlinkOracle](https://explorer.zksync.io/address/0x4FC29E1d3fFFbDfbf822F09d20A5BE97e59F66E5) | Upper bound: 1.01. Lower bound: 0.99 |
| Core | wstETH | [wstETHOneJumpChainlinkOracle](https://explorer.zksync.io/address/0x2DAaeb94E19145BA7633cAB2C38c76fD8c493198) | - | - | |
| Core | wUSDM | [wUSDM-ERC4626Oracle](https://explorer.zksync.io/address/0x22cE94e302c8C80a6C2dCfa9Da6c5286e9f28692) | - | - | |
| Core | zkETH | [ZkETHOracle](https://explorer.zksync.io/address/0x407dE1229BCBD2Ec876d063F3F93c4D8a38bd81a) | - | - | Assume 1:1 for WETH:rzkETH |

#### Optimism Mainnet

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | WBTC | [SequencerChainlinkOracle](https://optimistic.etherscan.io/address/0x1076e5A60F1aC98e6f361813138275F1179BEb52) | - | - | |
| Core | WETH | [SequencerChainlinkOracle](https://optimistic.etherscan.io/address/0x1076e5A60F1aC98e6f361813138275F1179BEb52) | - | - | |
| Core | USDC | [SequencerChainlinkOracle](https://optimistic.etherscan.io/address/0x1076e5A60F1aC98e6f361813138275F1179BEb52) | - | - | |
| Core | USDT | [SequencerChainlinkOracle](https://optimistic.etherscan.io/address/0x1076e5A60F1aC98e6f361813138275F1179BEb52) | - | - | |
| Core | OP | [SequencerChainlinkOracle](https://optimistic.etherscan.io/address/0x1076e5A60F1aC98e6f361813138275F1179BEb52) | - | - | |

#### Base Mainnet

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | cbBTC | [ChainlinkOracle](https://basescan.org/address/0x6F2eA73597955DB37d7C06e1319F0dC7C7455dEb) | - | - | |
| Core | WETH | [ChainlinkOracle](https://basescan.org/address/0x6F2eA73597955DB37d7C06e1319F0dC7C7455dEb) | - | - | |
| Core | USDC | [ChainlinkOracle](https://basescan.org/address/0x6F2eA73597955DB37d7C06e1319F0dC7C7455dEb) | - | - | |
| Core | wsuperOETHb | [wsuperOETHb-ERC4626Oracle](https://basescan.org/address/0xcd1d2C99642165440c2CC023AFa2092b487f033e) | - | - | |
| Core | wstETH | [wstETHOneJumpChainlinkOracle](https://basescan.org/address/0xDDD4F0836c8016E11fC6741A4886E97B3c3d20C1) | - | - | |

#### Unichain Mainnet

| Pool | Market | MAIN oracle | PIVOT oracle | FALLBACK oracle | Notes |
|---|---|---|---|---|---|
| Core | WBTC | [RedStone](https://uniscan.xyz/address/0x4d41a36D04D97785bcEA57b057C412b278e6Edcc) | - | - | |
| Core | WETH | [RedStone](https://uniscan.xyz/address/0x4d41a36D04D97785bcEA57b057C412b278e6Edcc) | - | - | |
| Core | USDC | [RedStone](https://uniscan.xyz/address/0x4d41a36D04D97785bcEA57b057C412b278e6Edcc) | - | - | |
| Core | USD₮0 | [RedStone](https://uniscan.xyz/address/0x4d41a36D04D97785bcEA57b057C412b278e6Edcc) | - | - | |
| Core | UNI | [RedStone](https://uniscan.xyz/address/0x4d41a36D04D97785bcEA57b057C412b278e6Edcc) | - | - | |
| Core | weETH | [weETHOneJumpOracle](https://uniscan.xyz/address/0xF9ECA470E2458Fe2B6FcAe660bEd1e2C0FB87E01) | - | - | |
| Core | wstETH | [wstETHOneJumpOracle](https://uniscan.xyz/address/0x3938D6414c261C6F450f1bD059DF9af2BBfb603D) | - | - | |

### Further Reading

For more detailed information, refer to the following resources:

#### Audit reports

* [Resilient Price Oracle](../security-and-audits.md#oracles)
* [Resilient Price Oracle upgrade](../security-and-audits.md#oracles-upgrade-2023-07-24)
* [WstETH oracle](../security-and-audits.md#oracle-for-wsteth)
* [Correlated token oracles](../security-and-audits.md#correlated-token-oracles)

#### References

* [Repository](https://github.com/VenusProtocol/oracle)
* [Community post about Venus V4, introducing Resilient Price Feeds](https://community.venus.io/t/proposing-venus-v4/3188#price-feed-redundancy-6)
* [Venus Stars blog post about Binance Oracle](https://venusstars.io/community/index.php/2023/05/09/venus-enhances-resilience-binance-oracle-feeds/)
