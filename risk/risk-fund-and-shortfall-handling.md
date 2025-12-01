# 风险基金和资金缺口处理

### **概述**

金星协议 通过隔离资金池管理高波动性代币的风险。每个资金池（隔离资金池和核心资金池）都关联着一个风险基金，该基金会从资金池的收入（利息和清算奖励）中抽取一定比例的 USDT 作为资金，以防止资金池破产。具体比例由项目的[代币经济学](../governance/tokenomics.md)定义。风险基金还用于在没有清算人的情况下破产时弥补坏账。

### 风险基金

风险基金涉及三个主要合约：

* `ProtocolShareReserve`

* `RiskFund`

* `ReserveHelpers`

这三个合约旨在持有从利息储备和清算奖励中积累的资金，并将一部分发送到协议金库，剩余部分发送到 `RiskFund` 合约。当在 vToken 合约中调用 `reduceReserves()` 时，所有累积的清算费用和利息储备都会被发送到 `ProtocolShareReserve` 合约。资金转移到 `ProtocolShareReserve` 后，任何人都可以调用 `releaseFunds()` 将 50% 的资金转移到 `protocolIncome` 地址，另外 50% 的资金转移到 `riskFund` 合约。进入 `riskFund` 合约后，代币可以通过 PancakeSwap 对兑换为可转换基础资产，授权账户可以更新该基础资产。代币转换为 `convertibleBaseAsset` 后，可以在 `Shortfall` 合约中使用，用于拍卖资金池的不良债务。请注意，正如每个资金池都是独立的一样，每个资金池的风险基金也是独立的：只有与某个资金池关联的风险基金才能用于拍卖该资金池的不良债务。

### 资金缺口

当在隔离资金池市场中检测到借款人资金缺口（以美元计价的借款总额大于以美元计价的供应总额）时，Venus 将停止计息，注销借款人的余额，并追踪坏账。

`Shortfall` 是一种拍卖合约，旨在拍卖 `RiskFund` 中积累的 `convertibleBaseAsset`。拍卖 `convertibleBaseAsset` 的目的是为了换取用户偿还资金池的坏账。一旦资金池的坏账达到最低值（参见 `Shortfall.minimumPoolBadDebt()`），任何人都可以发起拍卖。该值由授权账户设置并可更改。如果资金池的坏账超过风险基金加上 10% 的激励，则拍卖的获胜者将由偿还资金池坏账比例最高的人决定。拍卖获胜者需偿还坏账的竞标比例，以换取全部风险基金。否则，如果风险基金足以覆盖资金池的坏账加上 10% 的激励，则拍卖获胜者由愿意偿还资金池全部坏账且接受风险基金比例最小的竞标者决定。

`Shortfall` 合约中的主要可配置参数（通过 VIP）及其初始值如下：

* `minimumPoolBadDebt` - 资金池中允许发起拍卖的最低美元坏账额。初始值设置为 1,000 美元。

* `waitForFirstBidder` - 等待第一个竞标者的区块数。初始值设置为 100 个区块。

* `nextBidderBlockLimit` - 等待下一个竞标者的时间。初始值设置为 100 个区块。

* `incentiveBps` - 给予拍卖参与者的激励。初始值设置为 1000 个基点或 10%

{% hint style="info" %}

**可用性**：

* `Shortfall` 合约仅适用于隔离池中的市场。

* 核心池中的市场目前不追踪不良债务，因此无法自动减少。

* 核心池中产生的、应分配给风险基金的资金，暂时发送到 [Venus Treasury](https://bscscan.com/address/0xf322942f644a996a617bd29c16bd7d231d9f35e9) 合约。随着[自动收益分配](../whats-new/automatic-income-allocation.md)功能的发布，这部分收益将发送到`ProtocolShareReserve`合约，并根据项目的[代币经济学](../governance/tokenomics.md)进行分配。

* 与核心池相关的资金，累积在`RiskFund`合约中，将用于通过VIP偿还核心池的坏账。

{% endhint %}
