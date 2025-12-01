# 合约概览

Venus Protocol 合约分为以下几个代码库：

* [isolated-pools](https://github.com/VenusProtocol/isolated-pools)：包含独立借贷的核心合约，包括资金供应、借贷、清算、资金池和市场部署以及利率模型的逻辑。

* [oracle](https://github.com/VenusProtocol/oracle)：此代码库包含我们支持的预言机的合约，以及验证这些预言机返回价格的逻辑。

* [venus-protocol](https://github.com/VenusProtocol/venus-protocol)：核心协议位于此代码库中。它包含核心资金池借贷的核心逻辑。

* [governance-contracts](https://github.com/VenusProtocol/governance-contracts): 用于提议、投票和执行变更的合约保存在 `governance-contracts` 代码库中。

* [token-bridge](https://github.com/VenusProtocol/token-bridge): 用于将 XVS 连接到不同网络的合约。

## 隔离池合约

隔离池合约分为两类：

* 池合约

* 风险管理合约

### 池合约

池合约可分为四类：

* 配置合约

* 逻辑合约

* 其他合约

#### 配置合约

配置合约用于部署、配置和管理池。

[**PoolRegistry**](reference-isolated-pools/pool-registry/pool-registry.md)

创建和管理资金池由 [PoolRegistry](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/Pool/PoolRegistry.sol) 完成。它可以向资金池添加市场、更新资金池元数据并返回资金池信息。

#### 逻辑合约

[**Comptroller**](reference-isolated-pools/comptroller/comptroller.md)

[Comptroller](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/Comptroller.sol) 合约是每个借贷资金池的核心合约。它包含资金池借贷活动的核心功能，例如资产的提供和借入以及清算。资金池的配置值，例如清算激励、关闭因子和抵押因子，也可以从控制者处设置和获取。账户流动性和持仓信息也可以从控制者处获取。

[**vToken**](reference-isolated-pools/vtoken/vtoken.md)

[vToken](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/VToken.sol) 在隔离借贷中扮演着与核心资金池中的 vToken 相同的角色。它们代表用户提供给协议的代币，并且可以被兑换（销毁）为这些代币。

#### 其他合约

隔离资金池使用其他合约，例如 lens、rewards 等。

[**RewardsDistributor**](reference-isolated-pools/rewards/rewards-distributor.md)

用户通过借贷活动获得奖励代币。 [奖励分配器](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/Rewards/RewardsDistributor.sol) 使用可配置的费率管理这些分配。

[**池透镜**](reference-isolated-pools/lens/pool-lens.md)

为了简化池数据的查询，Isolated Pools 包含一个 [透镜](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/Lens/PoolLens.sol)，用于查询和格式化池数据。这些调用可能会消耗大量 gas，因此通常情况下，不应在交易中使用此合约。

#### 风险管理

[**风险基金**](reference-isolated-pools/risk-fund-and-shortfall/risk-fund.md)

借贷本身存在借款人无法偿还贷款的固有风险，这会威胁到协议的偿付能力。Venus 通过[风险基金](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/RiskFund/RiskFund.sol)来降低这种风险。协议收入的一部分会随着累积转移到风险基金中。当发现坏账时，该基金可以进行拍卖，用于偿还坏账。

[**Shortfall**](reference-isolated-pools/risk-fund-and-shortfall/shortfall.md)

当坏账被拍卖时，[Shortfall](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/Shortfall/Shortfall.sol)合约负责执行拍卖并向中标者支付款项。

[**ProtocolShareReserve**](reference-isolated-pools/risk-fund-and-shortfall/protocol-share-reserve.md)

[ProtocolShareReserve](https://github.com/VenusProtocol/protocol-reserve/blob/main/contracts/ProtocolReserve/ProtocolShareReserve.sol)充当一个金库，每个隔离池都可以将其收益转移到该金库中。

## 预言机合约

[**ResilientOracle**](reference-oracle/resilient-oracle.md)

Venus Protocol 实现了辅助预言机、主预言机和枢轴预言机，从而创建了一种验证和回退策略，避免因依赖单一价格来源而导致的单点故障。[ResilientOracle](https://github.com/VenusProtocol/oracle/blob/main/contracts/ResilientOracle.sol) 合约负责获取和验证给定 vToken 的价格，并管理特定 vToken 使用的预言机。

### 预言机

[**ChainlinkOracle**](reference-oracle/oracles/chainlink-oracle.md)

[ChainLinkOracle](https://github.com/VenusProtocol/oracle/blob/main/contracts/oracles/ChainlinkOracle.sol) 是主预言机。如果某个代币不受 Chainlink 支持，则价格将从辅助预言机获取。

[**RedstoneOracle**](https://redstone.finance/)

[RedstoneOracle](https://docs.redstone.finance/docs/smart-contract-devs/get-started/redstone-classic) 在经典模型（Chainlink 兼容接口）中用作枢轴预言机，以验证主预言机和备用预言机返回的价格。

[**BinanceOracle**](reference-oracle/oracles/binance-oracle.md)

[BinanceOracle](https://github.com/VenusProtocol/oracle/blob/main/contracts/oracles/BinanceOracle.sol) 合约负责从币安预言机获取代币价格。它用作辅助预言机。

[**PythOracle**](链接已失效)

[PythOracle](https://github.com/VenusProtocol/oracle/blob/main/contracts/oracles/PythOracle.sol) 用作枢轴预言机，用于验证主预言机和辅助预言机返回的价格。

## Venus Protocol

Venus Protocol 合约可分为以下几类：

* 借贷

* 代币

* 金库

* Lens

### 借贷合约

[**Comptroller**](reference-core-pool/comptroller/Diamond/Diamond.md)

核心池的核心是控制器。最新版本是 [Comptroller](https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/Comptroller/Diamond/Diamond.sol)。控制器负责上架市场、管理用户在市场中的持仓、清算以及发放奖励。它包含用于设置市场配置变量（例如抵押因子、平仓因子和清算激励）的 setter 和 getter。借贷操作可以通过控制器全局暂停，也可以针对特定市场暂停。

[**JumpRateModel**](reference-core-pool/interest-rate-models/jump-model.md)

每个市场都部署了一个利率模型。 [JumpRateModel](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/InterestRateModels/JumpRateModel.sol) 使用线性曲线根据资产的供求关系确定利率，直至达到拐点，之后利率将急剧上升。

[**WhitePaperInterestRateModel**](reference-core-pool/interest-rate-models/white-paper-interest-rate-model.md)

另一个可与市场结合使用的利率模型是[WhitePaperInterestRateModel](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/InterestRateModels/WhitePaperInterestRateModel.sol)。它与 JumpRateModel 类似，区别在于它不包含拐点，而是采用固定基准利率。

[**清算人**](reference-core-pool/liquidator.md)

当借款人资不抵债时，可能会被清算。[清算人](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Liquidator/Liquidator.sol)负责处理此过程。借款人被清算后，被扣押的金额将在清算人和[金库](reference-core-pool/vtreasury.md)之间分配。

[**虚拟金库**](reference-core-pool/vtreasury.md)

协议所赚取的收入存放在[虚拟金库](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Governance/VTreasury.sol)中。

### 代币合约

[**XVS**](../tokens/xvs.md)

XVS 是 Venus 生态系统中的重要代币，因为它为 Venus 的治理提供支持。[XVS](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Tokens/XVS/XVS.sol) 代币合约定义了一种可锁定的 BEP20 代币，并提供了投票和投票委托等附加功能。要进行投票，用户必须先将其 XVS 锁定在金库中。

[**VAI**](../tokens/vai.md)

[VAI](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Tokens/VAI/VAI.sol) 是 Venus 的稳定币，可以抵押发行。用户铸造 VAI 时需支付一定的费用，该费用基于 VAI 的未偿供应量和价格，以维持其价值为 1 美元。[VAIController](https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/Tokens/VAI/VAIController.sol) 控制用户可铸造的 VAI 数量，该数量取决于用户提供的抵押品及其流动性。

[**vToken**](reference-core-pool/vtoken.md)

当用户向协议提供代币时，系统会铸造 vToken 来表示其供应量。 [VToken](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Tokens/VTokens/VBep20.sol) 合约包含支持资产借贷活动（包括借贷和清算）的方法。

### 金库合约

**XVS 金库**

XVS 可以锁定在 [XVSVault](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/XVSVault/XVSVault.sol) 中以赚取 XVS 并启用投票功能。每个锁定的 XVS 都会为锁定地址提供一票，可用于投票或委托投票。

**VAI 金库**

在 [VAIVault](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Vault/VAIVault.sol) 中质押的 VAI 可赚取 XVS。质押奖励每日累积。

#### 其他合同

**ComptrollerLens**

[ComptrollerLens](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Lens/ComptrollerLens.sol) 包含用于获取账户流动性以及可用于偿还特定金额的代币数量的方法。

**SnapshotLens**

[SnapshotLens](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Lens/SnapshotLens.sol) 包含用于获取特定市场或账户活跃的所有市场中账户详细信息的方法。

**VenusLens**

协议级数据通过 [VenusLens](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/Lens/VenusLens.sol) 提供。它包含与 XVS 分发、治理和市场相关的 getter 方法。

### 治理合约

主要有三个治理合约：

* GovernorBravoDelegate

* AccessControlManager

* Timelock

**GovernorBravoDelegate**

治理提案的核心逻辑位于 [GovernorBraveDelegate](https://github.com/VenusProtocol/governance-contracts/blob/main/contracts/Governance/GovernorBravoDelegate.sol) 合约中。它支持提交提案、推动提案通过时间限制阶段、取消和执行提案以及投票逻辑。投票阈值和时间限制均在此合约中设置。

**访问控制管理器**

为了增强协议的安全性，Venus Protocol 使用 [访问控制管理器](https://github.com/VenusProtocol/governance-contracts/blob/main/contracts/Governance/AccessControlManager.sol) 合约来授予账户调用合约中特定函数的权限。该合约负责授予和撤销这些权限。它还提供了一个 getter 方法来检查某个地址是否被允许调用特定函数。

**时间锁** 提案一旦成功提交，其执行将由 [时间锁](https://github.com/VenusProtocol/governance-contracts/blob/main/contracts/Governance/Timelock.sol) 合约管理。时间锁可以将提案放入执行队列并执行提案。它还允许取消提案。
