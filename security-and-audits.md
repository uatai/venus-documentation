# 安全与审计

在 金星协议，我们始终致力于为用户提供最高级别的安全保障。在整个智能合约开发生命周期中，我们严格遵循行业最佳实践，以维护平台的完整性。为了进一步加强安全措施，我们与业内知名的审计公司开展合作。这些合作关系使我们能够对协议进行全面的安全评估，从而有效保障用户资金安全。

金星 协议的安全是我们的重中之重。我们的开发团队与第三方审计师和顾问携手合作，投入了大量精力，打造出我们自信认为安全可靠的协议。我们重视透明度，所有合约代码和余额均可公开验证。此外，我们还为报告未发现漏洞的安全研究人员提供漏洞赏金计划，鼓励持续改进和保持警惕。

我们坚信，衡量智能合约安全性的真正标准在于其规模、可见性和持久性。因此，我们敦促用户谨慎行事，并对我们协议的安全性和适用性进行独立评估。

## 审计

### 效率E模式E-Mode

**范围**：BNB 链核心池中的 E-Mode 支持。

* [Certik audit report (2025/09/19)](https://github.com/VenusProtocol/venus-protocol/blob/73fa9f21c321f9e1821a7b187aeca46033ca5484/audits/149_emode_certik_20250919.pdf)
* [Quantstamp audit report (2025/09/03)](https://github.com/VenusProtocol/venus-protocol/blob/73fa9f21c321f9e1821a7b187aeca46033ca5484/audits/150_emode_quantstamp_20250903.pdf)

<details>
<summary>Detailed scope</summary>

- Pull request [#614](https://github.com/VenusProtocol/venus-protocol/pull/614) in the `venus-protocol` repository:
  - contracts/Comptroller/Diamond/facets/FacetBase.sol
  - contracts/Comptroller/Diamond/facets/MarketFacet.sol
  - contracts/Comptroller/Diamond/facets/PolicyFacet.sol
  - contracts/Comptroller/Diamond/facets/RewardFacet.sol
  - contracts/Comptroller/Diamond/facets/SetterFacet.sol
  - contracts/Comptroller/Diamond/interfaces/IFacetBase.sol
  - contracts/Comptroller/Diamond/interfaces/IMarketFacet.sol
  - contracts/Comptroller/Diamond/interfaces/ISetterFacet.sol
  - contracts/Comptroller/Diamond/Diamond.sol
  - contracts/Comptroller/ComptrollerInterface.sol
  - contracts/Comptroller/ComptrollerLensInterface.sol
  - contracts/Comptroller/ComptrollerStorage.sol
  - contracts/Comptroller/Types/PoolMarketId.sol
  - contracts/InterfacesV8.sol
  - contracts/Lens/ComptrollerLens.sol
  - contracts/Lens/VenusLens.sol
  - contracts/Liquidator/Liquidator.sol
  - contracts/Tokens/VAI/VAIController.sol
  - contracts/Tokens/VTokens/VToken.sol
  - contracts/Utils/ErrorReporter.sol

</details>


### 风险管家 V1 和核心资金池控制员接口与独立资金池的兼容性

**范围**：Venus 风险管家合约，与 Chaos Labs 的风险预言机合约兼容。这些管家被授权执行风险参数变更（最初仅增加供应量和借贷上限），无需 VIP。此外，BNB 链上的控制员合约接口已扩展，包含独立资金池控制员合约中定义的功能，从而简化了与两个控制员合约的交互。已在 [VIP-544](https://app.venus.io/#/governance/proposal/544?chainId=56) 中启用。

* [Certik 审计报告 (2025/02/19)](https://github.com/VenusProtocol/governance-contracts/blob/210d1e54f0c9136a805977b41077567b0883a4e0/audits/120_risk_stewards_v1_certik_20250219.pdf)

* [Quantstamp 审计报告 (2025/02/13)](https://github.com/VenusProtocol/governance-contracts/blob/210d1e54f0c9136a805977b41077567b0883a4e0/audits/121_risk_stewards_v1_quantstamp_20250213.pdf)

* [FairyProof 审计报告 ... (2025/02/26)](https://github.com/VenusProtocol/governance-contracts/blob/210d1e54f0c9136a805977b41077567b0883a4e0/audits/122_risk_stewards_v1_fairyproof_20250226.pdf)

<details>

<summary>详细范围</summary>

- 在 `governance-contracts` 仓库中提交的拉取请求 [#115](https://github.com/VenusProtocol/governance-contracts/pull/115)：

- contracts/RiskSteward/RiskStewardReceiver.sol – 该功能的入口点

- contracts/RiskSteward/MarketCapsRiskSteward.sol

- contracts/RiskSteward/IRiskSteward.sol

- contracts/RiskSteward/IRiskStewardReceiver.sol

- 与外部合约的接口：

- contracts/interfaces/ICorePoolComptroller.sol

- contracts/interfaces/IIsolatedPoolsComptroller.sol

- contracts/interfaces/IRiskOracle.sol

- contracts/interfaces/IVToken.sol

- 在 `venus-protocol` 仓库中提交的拉取请求 [#548](https://github.com/VenusProtocol/venus-protocol/pull/548)：

- contracts/Comptroller/Diamond/facets/MarketFacet.sol

- contracts/Comptroller/Diamond/facets/PolicyFacet.sol

- contracts/Comptroller/Diamond/facets/SetterFacet.sol

- contracts/Comptroller/Diamond/interfaces/IMarketFacet.sol

- contracts/Comptroller/Diamond/interfaces/IPolicyFacet.sol

- contracts/Comptroller/Diamond/interfaces/ISetterFacet.sol

</details>

### 原生代币网关升级

**范围**：[NativeTokenGateway 合约](https://github.com/VenusProtocol/venus-periphery/blob/95e157b5b498ab80fe2715ca5ecf64203f6727fb/contracts/Gateway/NativeTokenGateway.sol) 升级，使其与 BNB 链上的核心池兼容。已在 [VIP-543](https://app.venus.io/#/governance/proposal/543?chainId=56) 中启用

- [Certik 审计报告 (2024/09/11)](https://github.com/VenusProtocol/venus-periphery/blob/95e157b5b498ab80fe2715ca5ecf64203f6727fb/audits/152_nativeTokenGateway_certik_20250911.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#8](https://github.com/VenusProtocol/venus-periphery/pull/8)

- contracts/Gateway/Interfaces/IVToken.sol

- contracts/Gateway/INativeTokenGateway.sol

- contracts/Gateway/Interfaces/IWrappedNative.sol

- contracts/Gateway/NativeTokenGateway.sol

</details>

### Venus ERC4626 金库

**范围**：Venus 市场针对独立资金池的 [ERC-4626](https://ethereum.org/en/developers/docs/standards/tokens/erc-4626/) 封装，可与遵循 ERC-4626 标准的外部 DeFi 协议无缝集成。

* [Certik 审计报告 (2025/05/14)](https://github.com/VenusProtocol/isolated-pools/blob/1faa46139aaec06e0eb2e48341bff22cd6c38c6c/audits/129_erc4626_certik_20250514.pdf)

* [Pessimistic 审计报告 (2025/05/02)](https://github.com/VenusProtocol/isolated-pools/blob/1faa46139aaec06e0eb2e48341bff22cd6c38c6c/audits/131_erc4626_pessimistic_20250502.pdf)

* [FairyProof 审计报告 ... (2025/04/14)](https://github.com/VenusProtocol/isolated-pools/blob/1faa46139aaec06e0eb2e48341bff22cd6c38c6c/audits/130_erc4626_fairyproof_20250414.pdf)

<details>

<summary>详细范围</summary>

- 在 `isolated-pools` 代码库中提交了拉取请求 [#497](https://github.com/VenusProtocol/isolated-pools/pull/497)。

- contracts/ERC4626/VenusERC4626.sol

- contracts/ERC4626/VenusERC4626Factory.sol

- contracts/ERC4626/Interfaces/IComptroller.sol

- contracts/ERC4626/Interfaces/IProtocolShareReserve.sol

- contracts/ERC4626/Interfaces/IRewardsDistributor.sol

- `protocol-reserve` 仓库中的拉取请求 [#137](https://github.com/VenusProtocol/protocol-reserve/pull/137)

- contracts/Interfaces/IProtocolShareReserve.sol

</details>

### asBNB 预言机

**范围**：关联预言机，用于获取 BNB 链上 [asBNB](https://bscscan.com/address/0x77734e70b6E88b4d82fE632a168EDf6e700912b6) 代币的价格，首先考虑链上 `asBNB` 到 [`slisBNB`](https://bscscan.com/address/0xB0b84D294e0C75A6abe60171b70edEb2EFd14A1B) 的转换率。

- [Certik 审计报告 (2025/03/20)](https://github.com/VenusProtocol/oracle/blob/e33dd9b60a29d3e69df554136383a6477fa904c5/audits/128_AsBNBOracle_certik_20250320.pdf)

<details>

<summary>详细范围</summary>

- Pull Request [#275](https://github.com/VenusProtocol/oracle/pull/275)

- 文件：

- contracts/oracles/AsBNBOracle.sol

</details>

### zkETH 预言机

**范围**：关联预言机，用于获取价格在 ZKsync 上，[zkETH](https://explorer.zksync.io/address/0xb72207E1FB50f341415999732A20B6D25d8127aa) 代币的价格首先考虑链上 zkETH 到 rzkETH 的转换率。

- [Certik 审计报告 (2025/02/25)](https://github.com/VenusProtocol/oracle/blob/3b5aec61acb7d2c659c70e8fce7501cb49ea74cd/audits/124_oracles_certik_20250225.pdf)

<details>

<summary>详细范围</summary>

- Pull Request [#269](https://github.com/VenusProtocol/oracle/pull/269)

- 文件：

- contracts/oracles/ZkETHOracle.sol

</details>

### ERC4626 预言机

**范围**：关联预言机，用于获取 [ERC4626](https://eips.ethereum.org/EIPS/eip-4626) 代币的价格，并考虑首先计算 ERC4626 代币与其底层代币的链上转换率。

- [Certik 审计报告 (2025/02/06)](https://github.com/VenusProtocol/oracle/blob/b6d581ddac010a8a80ba4c6fe819c756568c4a92/audits/123_erc4626Oracle_certik_20250206.pdf)

<details>

<summary>详细范围</summary>

- Pull Request [#253](https://github.com/VenusProtocol/oracle/pull/253)

- 文件：

- contracts/oracles/ERC4626Oracle.sol

</details>

### PendleOracle 升级

**范围**：升级当前 PendleOracle 合约的实现，使其支持 Pendle 的 `getPtToSyRate()` 函数。这样就可以添加收益代币作为基础，而无需直接使用底层资产。

- [Certik 审计报告 (2024/12/26)](https://github.com/VenusProtocol/oracle/blob/de3c5a9ad4f7259870864dac1b6837e8908d799e/audits/119_pendleOracleUpdate_certik_20241226.pdf)

<details>

<summary>详细范围</summary>

- Pull Request [#240](https://github.com/VenusProtocol/oracle/pull/240)

- 文件：

- contracts/oracles/PendleOracle.sol

- contracts/interfaces/IPendlePtOracle.sol

</details>

### ACMCommandsAggregator

**范围**：`ACMCommandsAggregator` 是一个无需许可的合约，将部署到远程网络。 （除 BNB 链之外的所有网络），以便于在每个网络的 AccessControlManager 中配置（授予和撤销）权限。

- [Certik 审计报告 (2024/10/07)](https://github.com/VenusProtocol/governance-contracts/blob/3a5a2740e86c9137ab17f4f3939c97b145a22803/audits/118_ACMCommandsAggregator_certik_20241007.pdf)

<details>

<summary>详细范围</summary>

- Pull Request [#90](https://github.com/VenusProtocol/governance-contracts/pull/90)

- 文件：

- contracts/Utils/ACMCommandsAggregator.sol

</details>

### 双拐点利率

**范围**：为核心资金池（[此处](https://github.com/VenusProtocol/venus-protocol/blob/main/contracts/InterestRateModels/TwoKinksInterestRateModel.sol)）和独立资金池（[此处](https://github.com/VenusProtocol/isolated-pools/blob/main/contracts/TwoKinksInterestRateModel.sol)）开发新的利率模型，支持两种不同的拐点，因此支持三种不同的斜率。已在 [VIP-385](https://app-alt.venus.io/#/governance/proposal/385) 中启用。

- [Certik 审计报告 (2024/07/31)](https://github.com/VenusProtocol/venus-protocol/blob/8be0034819eef313d6ffe216e5ba0f1152dbdcc0/audits/113_twoKinks_certik_20240731.pdf)

- [Fairyproof 审计报告 (2024/08/04)](https://github.com/VenusProtocol/venus-protocol/blob/8be0034819eef313d6ffe216e5ba0f1152dbdcc0/audits/114_twoKinks_fairyproof_20240804.pdf)

- [Quanstamp 审计报告 ... (2024/08/19)](https://github.com/VenusProtocol/venus-protocol/blob/8be0034819eef313d6ffe216e5ba0f1152dbdcc0/audits/115_twoKinks_quantstamp_20240819.pdf)

<details>

<summary>详细范围</summary>

支持核心池

- Pull Request [#494](https://github.com/VenusProtocol/venus-protocol/pull/494)

- 文件：

- contracts/InterestRateModels/InterestRateModelV8.sol

- contracts/InterestRateModels/TwoKinksInterestRateModel.sol

支持独立池

- Pull Request [#417](https://github.com/VenusProtocol/isolated-pools/pull/417)

- 文件：

- contracts/TwoKinksInterestRateModel.sol

</details>

### 取消市场上市

**范围**：修改 [isolated pools](https://github.com/VenusProtocol/isolated-pools) 和 [core](https://github.com/VenusProtocol/venus-protocol) 合约，以支持取消市场上市。修复核心池中借款上限设置为零时的行为。已在 [VIP-361](https://app-alt.venus.io/#/governance/proposal/361) 中启用。

- [Certik 审计报告 (2024/04/09)](https://github.com/VenusProtocol/venus-protocol/blob/e4c4dfe1b78945ea87dca5b7e0c724b6bd317359/audits/099_unlistMarkets_certik_20240409.pdf)

- [Fairyproof 审计报告 (2024/03/28)](https://github.com/VenusProtocol/venus-protocol/blob/e4c4dfe1b78945ea87dca5b7e0c724b6bd317359/audits/102_unlistMarkets_fairyproof_20240328.pdf)

<详情>

<摘要>详细信息范围</summary>

取消列出市场

- `venus-protocol` 代码库中的拉取请求 [#429](https://github.com/VenusProtocol/venus-protocol/pull/429)：

- 更改：允许治理机制从 Comptroller 合约中逻辑删除市场

- contracts/Comptroller/Diamond/facets/MarketFacet.sol

- contracts/Comptroller/Diamond/facets/PolicyFacet.sol

- `isolated-pools` 代码库中的拉取请求 [#349](https://github.com/VenusProtocol/isolated-pools/pull/349)：

- 更改：允许治理机制从 Comptroller 合约中逻辑删除市场

- 文件：contracts/Comptroller.sol

修复借款上限 0 的逻辑

- 提交了 `venus-protocol` 代码库中的 Pull Request [#438](https://github.com/VenusProtocol/venus-protocol/pull/438)：

- 更改：之前，借用上限为 0 表示无上限。这容易出错。根据新的逻辑，借贷上限为 0 将不允许新的借贷

- contracts/Comptroller/ComptrollerStorage.sol

- contracts/Comptroller/Diamond/facets/PolicyFacet.sol

- contracts/Comptroller/Diamond/facets/SetterFacet.sol

</details>

### 以太坊上 Ether.fi LRT 代币（weETHs 和 weETHk）的预言机

**范围**：以太坊上 [weETHs](https://etherscan.io/token/0x917ceE801a67f933F2e6b33fC0cD1ED2d5909D88) 和 [weETHk](https://etherscan.io/address/0x7223442cad8e9cA474fC40109ab981608F8c4273) 代币的特定预言机底层采用的是由 [Ether.fi](https://www.ether.fi/) 项目提供的“会计”合约。已在 [VIP-355](https://app-alt.venus.io/#/governance/proposal/355) 中启用。

- [Certik 审计报告 (2024/08/23)](https://github.com/VenusProtocol/oracle/blob/93a79c97e867f61652fc063abb5df323acc9bed4/audits/116_WeETHAccountantOracle_certik_20240823.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#213](https://github.com/VenusProtocol/oracle/pull/213)

- contracts/oracles/WeETHAccountantOracle.sol

- contracts/interfaces/IAccountant.sol

</details>

### VBNBAdmin：新增函数 setInterestRateModel

**范围**：更新 VBNBAdmin 合约，将 AccessControlManager 集成到 `setInterestRateModel` 函数中此功能将允许授权更多时间锁（不仅限于普通时间锁）来执行此功能，因此快速通道和关键 VIP 将能够更新 VBNB 市场的利率模型。此功能已在 [VIP-343](https://app-alt.venus.io/#/governance/proposal/343) 中启用。

- [Certik 审计报告 (2024/07/17)](https://github.com/VenusProtocol/venus-protocol/blob/5e4563ab0f2f98a04659e065b6c49acebf00df3b/audits/112_VBNBAdmin_certik_20240717.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#487](https://github.com/VenusProtocol/venus-protocol/pull/487)

- contracts/Admin/VBNBAdmin.sol

- contracts/Admin/VBNBAdminStorage.sol

</details>

### 以太坊上的 sfrxETH 预言机

**范围**：特定代币的预言机[sfrxETH](https://etherscan.io/token/0xac3e018457b222d93114458476f3e3416​​abbe38f) 运行于以太坊上，底层使用由 [FRAX 项目](https://docs.frax.finance/frax-oracle/advanced-concepts#frax-oracles) 提供的 `SfrxEthFraxOracle` 预言机。已在 [VIP-329](https://app.venus.io/#/governance/proposal/329) 中启用。

- [Certik 审计报告 (2024/05/17)](https://github.com/VenusProtocol/oracle/blob/0b221a7bb7d8e04fd8b013806facb93bcb4038b9/audits/110_sfrxETHOracle_certik_20240517.pdf)

- [Quantstamp 审计报告 (2024/05/20)](https://github.com/VenusProtocol/oracle/blob/0b221a7bb7d8e04fd8b013806facb93bcb4038b9/audits/111_sfrxETHOracle_quantstamp_20240530.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#191](https://github.com/VenusProtocol/oracle/pull/191)

- contracts/oracles/SFrxETHOracle.sol

</details>

### 多链治理

**范围**：跨链消息传递，在非 BNB 链上执行 VIP。Venus 集成了 [多链治理](https://github.com/VenusProtocol/governance-contracts/pull/21)。已在 [VIP-330](https://app.venus.io/#/governance/proposal/330) 和 [VIP-331](https://app.venus.io/#/governance/proposal/331) 中启用。

* [Openzeppelin 审计报告 - 2024/01/19](https://github.com/VenusProtocol/governance-contracts/blob/2915ea772d86d9cc63f88fb6e804eaae53193879/audits/084_multichainGovernance_openzeppelin_20240119.pdf)

* [Certik 审计报告 - 2024/02/26](https://github.com/VenusProtocol/governance-contracts/blob/2915ea772d86d9cc63f88fb6e804eaae53193879/audits/085_multichainGovernance_certik_20240226.pdf)

* [Cantina 审计报告 - [2024/04/25](https://github.com/VenusProtocol/governance-contracts/blob/2915ea772d86d9cc63f88fb6e804eaae53193879/audits/105_multichainGovernance_cantina_20240425.pdf)

* [Quantstamp 审计报告 - 2024/04/29](https://github.com/VenusProtocol/governance-contracts/blob/2915ea772d86d9cc63f88fb6e804eaae53193879/audits/106_multichainGovernance_quantstamp_20240429.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#21](https://github.com/VenusProtocol/governance-contracts/pull/21)

- contracts/Cross-chain/BaseOmnichainControllerDest.sol

- contracts/Cross-chain/BaseOmnichainControllerSrc.sol

- contracts/Cross-chain/OmnichainExecutorOwner.sol

- contracts/Cross-chain/OmnichainGovernanceExecutor.sol

- contracts/Cross-chain/OmnichainProposalSender.sol

- contracts/Cross-chain/interfaces/IGovernananceBravoDelegate.sol

- contracts/Cross-chain/interfaces/ITimelock.sol

- contracts/Governance/TimelockV8.sol

>>>>>>> main

</details>

### 基于时间的合约和 XVS 奖励扣押

**范围**：[隔离的]中的更改为了支持区块生成速率不恒定的区块链（例如 Arbitrum 区块链），我们开发了 [pools](https://github.com/VenusProtocol/isolated-pools)、[core](https://github.com/VenusProtocol/venus-protocol) 和 [oracle](https://github.com/VenusProtocol/oracle) 合约。此外，我们还为 Core 池添加了通过 VIP 提取 XVS 奖励的功能。

- [Certik 审计报告 (2024/01/17)](https://github.com/VenusProtocol/isolated-pools/blob/aa1f7ae61b07839231ec16e9c4143905785d7aae/audits/088_timeBased_certik_20240117.pdf)

- [Quantstamp 审计报告 (2024/03/19)](https://github.com/VenusProtocol/isolated-pools/blob/470416836922656783eab52ded54744489e8c345/audits/089_timeBased_quantstamp_20240319.pdf)

- [Fairyproof 审计报告 ...aa1f7ae61b07839231ec16e9c4143905785d7aae/audits/088_timeBased_certik_20240117.pdf) (2024/03/04)](https://github.com/VenusProtocol/isolated-pools/blob/aa1f7ae61b07839231ec16e9c4143905785d7aae/audits/094_timeBased_fairyproof_20240304.pdf)

<details>

<summary>详细范围</summary>

- 在 `isolated-pools` 代码库中提交拉取请求 [#324](https://github.com/VenusProtocol/isolated-pools/pull/324)

- 变更：基于时间戳的独立借贷合约

- contracts/JumpRateModelV2.sol

- contracts/Lens/PoolLens.sol

- contracts/Rewards/RewardsDistributor.sol

- contracts/Rewards/RewardsDistributorStorage.sol

- contracts/Shortfall/Shortfall.sol

- contracts/Shortfall/ShortfallStorage.sol

- contracts/VToken.sol

- contracts/VTokenInterfaces.sol

- contracts/WhitePaperInterestRateModel.sol

- contracts/lib/constants.sol

- 在 `venus-protocol` 代码库中提交的 Pull Request [#418](https://github.com/VenusProtocol/venus-protocol/pull/418)

- 变更：基于时间的 XVSVault

- contracts/XVSVault/TimeManagerV5.sol

- contracts/XVSVault/XVSVault.sol

- contracts/XVSVault/XVSVaultStorage.sol

- 在 `oracle` 代码库中提交的 Pull Request [#128](https://github.com/VenusProtocol/oracle/pull/128)

- 变更：为 Chainlink Oracle 添加 Arbitrum 序列器停机时间验证

- contracts/oracles/SequencerChainlinkOracle.sol

- contracts/oracles/ChainlinkOracle.sol

- 变更：使用可用现金减少储备金

- 已在 `venus-protocol` 代码库中提交拉取请求 [#414](https://github.com/VenusProtocol/venus-protocol/pull/414)

- contracts/Tokens/VTokens/VToken.sol

- 已在 `venus-protocol` 代码库中提交拉取请求 [#337](https://github.com/VenusProtocol/isolated-pools/pull/337)

- contracts/VToken.sol

- 已在 `venus-protocol` 代码库中提交拉取请求 [#417](https://github.com/VenusProtocol/venus-protocol/pull/417)

- 变更：扣押 XVS 奖励

- contracts/Comptroller/Diamond/facets/RewardFacet.sol

- 已在 `venus-protocol` 代码库中提交拉取请求 [#410] https://github.com/VenusProtocol/venus-protocol/pull/410 位于 `venus-protocol` 代码库中

- 变更：动态设置 XVS 和 XVSVToken 的地址

- contracts/Comptroller/ComptrollerStorage.sol

- contracts/Comptroller/Diamond/Diamond.sol

- contracts/Comptroller/Diamond/facets/FacetBase.sol

- contracts/Comptroller/Diamond/facets/RewardFacet.sol

- contracts/Comptroller/Diamond/facets/SetterFacet.sol

</details>

### VAI 控制器

**范围**：`VAIController` 合约，用于修复 VAI 清算期间查封金额的计算方式，计算时需考虑原始 VAI 债务及其产生的利息。已在 [VIP-299](https://app.venus.io/#/governance/proposal/299) 中启用。

- [Certik 审计报告 (2024/04/26)](https://github.com/VenusProtocol/venus-protocol/blob/0000b6b7bb9eaf1d6827993c306b776c371d41b7/audits/107_vaiController_certik_20240426.pdf)

- [Pessimistic 审计报告 (2024/05/02)](https://github.com/VenusProtocol/venus-protocol/blob/c01162eac8a911cd3a45c3d55b91e418e5ec2e6a/audits/109_vaiController_pessimistic_20240502.pdf)

- [Fairyproof 审计报告 ...0000b6b7bb9eaf1d6827993c306b776c371d41b7/audits/107_vaiController_certik_20240426.pdf) (2024/04/18)](https://github.com/VenusProtocol/venus-protocol/blob/0000b6b7bb9eaf1d6827993c306b776c371d41b7/audits/108_vaiController_fairyproof_20240418.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#467](https://github.com/VenusProtocol/venus-protocol/pull/467)

- contracts/Tokens/VAI/VAIController.sol

</details>

### XVS 桥接 - 网状架构

**范围**：启用 BNB 链以外的网络之间的 XVS 转账，例如以太坊主网和 opBNB 主网之间的转账。[详细范围](https://github.com/VenusProtocol/vips/pull/255)。已在 [VIP-292](https://app.venus.io/#/governance/proposal/292) 中启用。

- [Certik 审计报告 (2024/04/19)](https://github.com/VenusProtocol/token-bridge/blob/7e13d370fbb8e9fcd6c8e0fde5943e44e0b64bfa/audits/104_mesh_architecture_certik_20240419.pdf)

### 相关代币预言机

**范围**：一组预言机，用于那些价格与另一种代币价格高度相关的代币。此定义包括流动性质押代币（例如 [wsETH](https://etherscan.io/token/0x7f39c581f595b53c5cb19bd0b3f8da6c935e2ca0)、[weETH](https://etherscan.io/token/0xcd5fe23c85820f7b72d0926fc9b05b43e359b7ee)、[WBETH](https://bscscan.com/address/0xa2e3356610840701bdf5611a53974510ae27e2e1)、[ankrBNB](https://bscscan.com/address/0x52F24a5e03aee338Da5fd9Df68D2b6FAe1178827)）。 [BNBx](https://bscscan.com/address/0x1bdd3Cf7F79cfB8EdbB955f20ad99211551BA275), [slisBNB](https://bscscan.com/address/0xB0b84D294e0C75A6abe60171b70edEb2EFd14A1B), [stkBNB](https://bscscan.com/address/0xc2E9d07F66A89c44062459A47a0D2Dc038E4fb16)), [ERC-4226 代币](https://eips.ethereum.org/EIPS/eip-4626)（类似[sFRAX](https://etherscan.io/token/0xa663b02cf0a4b149d2ad41910cb81e23e1c41c32)、[sfrxETH](https://etherscan.io/token/0xac3e018457b222d93114458476f3e3416​​abbe38f)) 以及任何可在链上转换为其他代币的代币（例如 [Pendle](https://www.pendle.finance) PT 代币）。[VIP-290](https://app.venus.io/#/governance/proposal/290?chainId=56) 中已启用 `WeETHOracle`。 `AnkrBNBOracle`、`BNBxOracle`、`SlisBNBOracle` 和 `StkBNBOracle` 已在 [VIP-293](https://app.venus.io/#/governance/proposal/293?chainId=56) 中启用。

- [Certik 审计报告 (2024/04/12)](https://github.com/VenusProtocol/oracle/blob/5cd52976a4c4d24e11ab34ca3aa5f99837eef593/audits/098_correlated_token_oracles_certik_20240412.pdf)

- [Quantstamp 审计报告 (2024/04/12)](https://github.com/VenusProtocol/oracle/blob/5cd52976a4c4d24e11ab34ca3aa5f99837eef593/audits/100_correlated_token_oracles_quantstamp_20240412.pdf)

- [Fairyproof 审计报告 ... (2024/03/28)](https://github.com/VenusProtocol/oracle/blob/5cd52976a4c4d24e11ab34ca3aa5f99837eef593/audits/101_correlated_token_oracles_fairyproof_20240328.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#165](https://github.com/VenusProtocol/oracle/pull/165)

- contracts/oracles/AnkrBNBOracle.sol

- contracts/oracles/BNBxOracle.sol

- contracts/oracles/OneJumpOracle.sol

- contracts/oracles/PendleOracle.sol

- contracts/oracles/SFraxOracle.sol

- contracts/oracles/SFrxETHOracle.sol

- contracts/oracles/SlisBNBOracle.sol

- contracts/oracles/StkBNBOracle.sol

- contracts/oracles/WBETHOracle.sol

- contracts/oracles/WeETHOracle.sol

- contracts/oracles/WstETHOracle.sol

- contracts/oracles/common/CorrelatedTokenOracle.sol

</details>

### 原生代币网关

**范围**：[NativeTokenGateway 合约](https://github.com/VenusProtocol/isolated-pools//blob/develop/contracts/Gateway/NativeTokenGateway.sol)，该合约促进与底层代币为原生代币封装版本的市场进行交互（借贷、供应、偿还和赎回）（例如以太坊上的 WETH 或 BNB 链上的 BNB）。已在 [VIP-276](https://app.venus.io/#/governance/proposal/276) 中启用。

- [Certik 审计报告 (2024/02/26)](https://github.com/VenusProtocol/isolated-pools/blob/652459fed7269dab84628f70c44d8fa56b34203e/audits/092_nativeTokenGateway_certik_20240226.pdf)

- [Pessimistic 审计报告 (2024/02/29)](https://github.com/VenusProtocol/isolated-pools/blob/652459fed7269dab84628f70c44d8fa56b34203e/audits/095_nativeTokenGateway_pessimistic_20240229.pdf)

- [Quantstamp 审计报告 ... (2024/03/01)](https://github.com/VenusProtocol/isolated-pools/blob/0ec94f4636e51d68197fe6918df096864acd0a23/audits/096_nativeTokenGateway_quantstamp_20240301.pdf)

<details>

<summary>详细范围</summary>

- Pull request [#361](https://github.com/VenusProtocol/isolated-pools/pull/361)

- contracts/Comptroller.sol

- contracts/ComptrollerStorage.sol

- contracts/Gateway/Interfaces/IVtoken.sol

- contracts/Gateway/Interfaces/IWrappedNative.sol

- contracts/Gateway/NativeTokenGateway.sol

- contracts/VToken.sol

- contracts/VTokenInterfaces.sol

- Pull request [#442](https://github.com/VenusProtocol/venus-protocol/pull/442)

- contracts/Tokens/VTokens/VBep20.sol

- contracts/Tokens/VTokens/VToken.sol

- contracts/Comptroller/Diamond/facets/MarketFacet.sol

</details>

### wstETH 的预言机

**范围**：[wstETH 的预言机](https://github.com/VenusProtocol/oracle/blob/develop/contracts/oracles/WstETHOracle.sol)，使用以太坊上 `stETH` 合约提供的汇率 `wstETH/stETH`，假设转换率 `stETH:ETH` 为 1:1，并使用 Resilient Oracles 将 `ETH` 转换为 `USD`。

- [Certik 审计报告 (2024/01/26)](https://github.com/VenusProtocol/oracle/blob/e99feb67f4677168632f5bedd70034fba8dc55db/audits/090_wstETHOracle_certik_20240126.pdf)

- [Quantstamp 审计报告 (2024/02/20)](https://github.com/VenusProtocol/oracle/blob/f34d3114267929bbba26743f0a8591c1b016fb94/audits/093_wstETHOracle_quantstamp_20240220.pdf)

<details>

<summary>详细范围</summary>

- `oracle` 代码库中的拉取请求 [#155](https://github.com/VenusProtocol/oracle/pull/155)

- contracts/oracles/WstETHOracle.sol

</details>

### 代币转换器

**范围**：[代币转换器合约](https://github.com/VenusProtocol/protocol-reserve/pull/9)。这些合约将允许协议根据[代币经济学](https://snapshot.org/#/venus-xvs.eth/proposal/0xc9d270ccecb7b91c75b95b8d9af24fc7c20cd38c0c0c44888ed4e7724f4e7ce9)将产生的收入转换为所需的代币。已在 [VIP-245](https://app.venus.io/#/governance/proposal/245) 和 [VIP-248](https://app.venus.io/#/governance/proposal/248) 中启用。

- Token Converter

- [OpenZeppelin 审计报告 (2023/10/10)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/066_tokenConverter_openzeppelin_20231010.pdf)

- [Certik 审计报告 (2023/11/07)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/074_tokenConverter_certik_20231107.pdf)

- [Peckshield 审计报告 ... [Fairyproof 审计报告 (2023/09/27)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/068_tokenConverter_peckshield_20230927.pdf)

- [Fairyproof 审计报告 (2023/08/28)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/067_tokenConverter_fairyproof_20230828.pdf)

- 私有转换（优化以避免在内部即可完成转换的情况下向第三方支付激励）

- [Certik 审计报告 (2023/11/27)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/081_privateConversions_certik_20231127.pdf)

- [Certik 审计补充 (2024/02/15)](https://github.com/VenusProtocol/protocol-reserve/blob/ba39ce060d0716be1131913e4dd6e93c1444e0c3/audits/081_privateConversions_certik_20240215.pdf)

- [OpenZeppelin 报告 ...f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/081_privateConversions_certik_20240215.pdf) [OpenZeppelin 附录 (2024/01/09)](https://github.com/VenusProtocol/protocol-reserve/blob/f31dc8bb433f1cff6c2124d27742004d82b24c32/audits/082_privateConversions_openzeppelin_20240109.pdf)

- [OpenZeppelin 附录 (2024/02/20)](https://github.com/VenusProtocol/protocol-reserve/blob/ba39ce060d0716be1131913e4dd6e93c1444e0c3/audits/082_privateConversions_openzeppelin_20240220.pdf)

<details>

<summary>详细范围</summary>

- `protocol-reserve` 代码库中的 Pull Request [#9](https://github.com/VenusProtocol/protocol-reserve/pull/9)。

- contracts/TokenConverter/AbstractTokenConverter.sol

- contracts/TokenConverter/IAbstractTokenConverter.sol

- contracts/TokenConverter/RiskFundConverter.sol

- contracts/TokenConverter/XVSVaultConverter.sol

- contracts/ProtocolReserve/RiskFundStorage.sol

- contracts/ProtocolReserve/RiskFundV2.sol

- contracts/ProtocolReserve/XVSVaultTreasury.sol

- contracts/Utils/Constants.sol

- contracts/Utils/Validators.sol

- `protocol-reserve` 代码库中的 Pull Request [#35](https://github.com/VenusProtocol/protocol-reserve/pull/35)。

- contracts/Interfaces/IConverterNetwork.sol

- contracts/TokenConverter/AbstractTokenConverter.sol

- contracts/TokenConverter/ConverterNetwork.sol

- contracts/TokenConverter/IAbstractTokenConverter.sol

- contracts/TokenConverter/RiskFundConverter.sol

- contracts/TokenConverter/SingleTokenConverter.sol

- contracts/Utils/ArrayHelpers.sol

</details>

### XVS 桥接和多链部署

**范围**：[token-bridge](https://github.com/VenusProtocol/token-bridge) 代码库，其中包含允许 XVS 代币从 BNB 桥接到其他 EVM 兼容网络（例如以太坊）的合约。扩展 OFTV2 LayerZero 合约，添加自定义安全规则。XVS 和 TokenController 合约，用于目标链（最初为以太坊主网、Arbitrum One、Polygon zkEVM 和 opBNB）。此外，审计范围还包括：新的 [`VTreasuryV8`](https://github.com/VenusProtocol/venus-protocol/pull/345) 合约，以及对 [Resilient Oracle](https://github.com/VenusProtocol/oracle/pull/124) 和 [Isolated pools](https://github.com/VenusProtocol/isolated-pools/pull/294) 的修改，使其与其他网络兼容。这些修改已在 [VIP-232](https://app.venus.io/#/governance/proposal/232) 中启用。

- [Certik 审计报告 (2023/12/26)](https://github.com/VenusProtocol/token-bridge/blob/323e95fa3c0167cca2fc1d2807e911e0bae54de9/audits/083_multichain_token_bridge_certik_20231226.pdf)

- [Quantstamp 审计报告 (2023/12/19)](https://github.com/VenusProtocol/token-bridge/blob/323e95fa3c0167cca2fc1d2807e911e0bae54de9/audits/064_multichain_token_bridge_quantstamp_20231219.pdf)

- [Peckshield 审计报告](https://github.com/VenusProtocol/token-bridge/blob/323e95fa3c0167cca2fc1d2807e911e0bae54de9/audits/064_multichain_token_bridge_quantstamp_20231219.pdf) （2023/10/20）](https://github.com/VenusProtocol/token-bridge/blob/04b0a8526bb2fa916785c41eefd94b4f84c12819/audits/079_multichain_token_bridge_peckshield_20231020.pdf)

<details>

<summary>详细范围</summary>

- Certik、Quantstamp 和 Peckshield 已审核：

- [token-bridge](https://github.com/VenusProtocol/token-bridge) 代码库

- 分支：`develop`

- 最后提交：`91b640fffb0c374bdb63a0f6e8e756793e892ad6`

- 审核范围内的文件列表：

- contracts/Bridge/BaseXVSProxyOFT.sol

- contracts/Bridge/XVSBridgeAdmin.sol

- contracts/Bridge/XVSProxyOFTDest.sol

- contracts/Bridge/XVSProxyOFTSrc.sol

- contracts/Bridge/token/TokenController.sol

- contracts/Bridge/token/XVS.sol

- contracts/Bridge/interfaces/IXVSProxyOFT.sol

- contracts/Bridge/interfaces/IXVS.sol

- 此外，Peckshield 还审核了以下内容：

- [https://github.com/VenusProtocol/venus-protocol/pull/345](https://github.com/VenusProtocol/venus-protocol/pull/345)

- 这是不同网络中使用的国库合约

- 灵感来源于部署在 BNB 链上的 VTreasury 合约（Solidity 0.5.16，[此处](https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/Governance/VTreasury.sol)）

- 主链：适配 Solidity 0.8.20

- 最后提交：0a058575a48b3b1d55cf257f2ade768b749f0fc6

- 弹性预言机变更

- [https://github.com/VenusProtocol/oracle/pull/124](https://github.com/VenusProtocol/oracle/pull/124)

- 重命名与各链上的原生代币和 VAI 代币相关的变量

- 上次提交：a0a36bcd94e5acd41e137e3cef711484f86eb397

- 除了上述范围之外，Quantstamp 还审核了：

- 隔离池变更

- [https://github.com/VenusProtocol/isolated-pools/pull/294](https://github.com/VenusProtocol/isolated-pools/pull/294)

- 将每年区块数转换为不可变值，以便在部署期间可以针对每条链进行配置

- 上次提交： 5e660bffec987b3d31aba3f11b5c4e35f689f646

- XVSVault

- [https://github.com/VenusProtocol/venus-protocol/tree/develop/contracts/XVSVault](https://github.com/VenusProtocol/venus-protocol/tree/develop/contracts/XVSVault)

- 最后提交：a158f8c335d0cfad71f1d2c27af6b0d92f4abe41

- 协议共享储备

- [https://github.com/VenusProtocol/protocol-reserve/blob/develop/contracts/ProtocolReserve/ProtocolShareReserve.sol](https://github.com/VenusProtocol/protocol-reserve/blob/develop/contracts/ProtocolReserve/ProtocolShareReserve.sol)

- 最后提交：e396119c4442b7811fbeb14ad0851afec1a9d0fa

- 访问控制管理器

- [https://github.com/VenusProtocol/governance-contracts/blob/main/contracts/Governance/AccessControlManager.sol](https://github.com/VenusProtocol/governance-contracts/blob/main/contracts/Governance/AccessControlManager.sol)

- 最后提交： 358bed476af7d7d871bf59e77c9daba22a7c2339

</details>

### 金星主星

**范围**：`Prime` 和 `PrimeLiquidityProvider` 合约，用于管理 Prime 代币的资格和奖励分配。

已在 [VIP-201](https://app.venus.io/#/governance/proposal/201)、[VIP-202](https://app.venus.io/#/governance/proposal/202)、[VIP-203](https://app.venus.io/#/governance/proposal/203)、[VIP-206](https://app.venus.io/#/governance/proposal/206) 和 [VIP-210](https://app.venus.io/#/governance/proposal/210) 中启用。已在 [VIP-225](https://app.venus.io/#/governance/proposal/225) 中更新。

- [OpenZeppelin 审计报告 (2023/10/03)](https://github.com/VenusProtocol/venus-protocol/blob/e02832bb2716bc0a178d910f6698877bf1b191e1/audits/065_prime_openzeppelin_20231003.pdf)

- [Certik 审计报告 (2023/11/13)](https://github.com/VenusProtocol/venus-protocol/blob/2425501070d28c36a73861d9cf6970f641403735/audits/060_prime_certik_20231113.pdf)

- [Peckshield 审计报告 ...e02832bb2716bc0a178d910f6698877bf1b191e1/audits/065_prime_certik_20231113.pdf) [Fairyproof 审计报告 (2023/08/26)](https://github.com/VenusProtocol/venus-protocol/blob/e02832bb2716bc0a178d910f6698877bf1b191e1/audits/055_prime_peckshield_20230826.pdf)

- [Fairyproof 审计报告 (2023/09/10)](https://github.com/VenusProtocol/venus-protocol/blob/e02832bb2716bc0a178d910f6698877bf1b191e1/audits/056_prime_fairyproof_20230910.pdf)

- [Code4rena 竞赛](https://github.com/VenusProtocol/venus-protocol/blob/e02832bb2716bc0a178d910f6698877bf1b191e1/audits/056_prime_fairyproof_20230910.pdf) （2023/09/28）](https://code4rena.com/contests/2023-09-venus-prime)

- [Certik 审计报告（2023/12/19）- Venus Prime 更新](https://github.com/VenusProtocol/venus-protocol/blob/9afe804f18cd02318626aea46686522542aa5e4d/audits/087_prime_certik_20231219.pdf)

- 仅允许 Prime 持有者铸造 VAI

- 支持隔离池

- 支持非恒定区块率的网络（例如，Arbitrum）

<details>

<summary>详细范围</summary>

- 核心池代码库中的拉取请求 [#196](https://github.com/VenusProtocol/venus-protocol/pull/196/)。

- Prime 功能：

- contracts/Tokens/Prime/IPrime.sol

- contracts/Tokens/Prime/Prime.sol

- contracts/Tokens/Prime/PrimeStorage.sol

- contracts/Tokens/Prime/PrimeLiquidityProvider.sol

- Comptroller 集成：

- contracts/Comptroller/ComptrollerStorage.sol

- contracts/Comptroller/Diamond/facets/PolicyFacet.sol

- contracts/Comptroller/Diamond/facets/SetterFacet.sol

- XVSVault 集成：

- contracts/XVSVault/XVSVault.sol

- contracts/XVSVault/XVSVaultStorage.sol

- 库：

- contracts/Tokens/Prime/libs/Scores.sol

- contracts/Tokens/Prime/libs/FixedMath.sol

- contracts/Tokens/Prime/libs/FixedMath0x.sol

- Venus Prime 更新。已在 [VIP-225](https://app.venus.io/#/governance/proposal/225) 中启用。

- Pull request [#407](https://github.com/VenusProtocol/venus-protocol/pull/407)

- contracts/Tokens/Prime/IPrime.sol

- contracts/Tokens/Prime/Interfaces/IPrime.sol

- contracts/Tokens/Prime/Prime.sol

- contracts/Tokens/Prime/PrimeLiquidityProvider.sol

- contracts/Tokens/Prime/PrimeStorage.sol

- contracts/Utils/TimeManager.sol

- contracts/Tokens/VAI/VAIController.sol

- contracts/Tokens/VAI/VAIControllerStorage.sol

- Pull request [#327](https://github.com/VenusProtocol/isolated-pools/pull/327)

- contracts/Comptroller.sol

- contracts/ComptrollerStorage.sol

- contracts/VToken.sol

</details>

### 自动收益分配

**范围**：修改核心池和IL池（包括VBNB市场）的VToken合约，将利息储备自动发送到新的ProtocolShareReserve合约，该合约将根据项目的代币经济模型，按照配置的规则分配收益。已在[VIP-189](https://app.venus.io/#/governance/proposal/189)、[VIP-192](https://app.venus.io/#/governance/proposal/192)、[VIP-193](https://app.venus.io/#/governance/proposal/193)和[VIP-194](https://app.venus.io/#/governance/proposal/194)中启用。

- [Quantstamp 审计报告 (2023/09/13)](https://github.com/VenusProtocol/venus-protocol/blob/9ef8901dfef84a11338751881fd10a2d36c576ad/audits/058_automatic_income_allocation_quantstamp_20230913.pdf)

- [Certik 审计报告 (2023/09/12)](https://github.com/VenusProtocol/venus-protocol/blob/90f913fd345c24c60efa613ab5ab7e633b7aa07a/audits/059_automatic_income_allocation_certik_20230912.pdf)

- [Peckshield 审计报告](https://github.com/VenusProtocol/venus-protocol/blob/9ef8901dfef84a11338751881fd10a2d36c576ad/audits/058 ... [Fairyproof 审计报告 (2023/08/12)](https://github.com/VenusProtocol/venus-protocol/blob/90f913fd345c24c60efa613ab5ab7e633b7aa07a/audits/054_automatic_income_allocation_peckshield_20230812.pdf)

- [Fairyproof 审计报告 (2023/08/03)](https://github.com/VenusProtocol/venus-protocol/blob/90f913fd345c24c60efa613ab5ab7e633b7aa07a/audits/050_automatic_income_allocation_fairyproof_20230803.pdf)

<详情>

<摘要>详细范围</摘要>

-核心池 - 利息储备：

- Pull request：https://github.com/VenusProtocol/venus-protocol/pull/262

- 文件：

- contracts/Tokens/VTokens/VToken.sol

- contracts/Tokens/VTokenInterfaces.sol

- contracts/Utils/ErrorReporter.sol

- 收取 BNB 收益：

- Pull request：https://github.com/VenusProtocol/venus-protocol/pull/289

- 文件：

- contracts/Admin/VBNBAdmin.sol

- contracts/Admin/VBNBAdminStorage.sol

- 隔离池 - 清算和利息储备：

- Pull request：https://github.com/VenusProtocol/isolated-pools/pull/207

- 文件：

- contracts/VToken.sol

- contracts/VTokenInterfaces.sol

- 分配收取的收益 - `ProtocolShareReserve` 合约

- 分支仓库 https://github.com/VenusProtocol/protocol-reserve 中的 `develop` 分支。需要关注的最后一个提交：dfb653d2e3fe163a248bbd9f8951cd6b96b06390

- 文件：

- contracts/ProtocolReserve/ProtocolShareReserve.sol

- contracts/Interfaces/IIncomeDestination.sol

- contracts/Interfaces/IPrime.sol

- contracts/Interfaces/IProtocolShareReserve.sol

- contracts/Interfaces/IVToken.sol

- contracts/Interfaces/ComptrollerInterface.sol

- contracts/Interfaces/PoolRegistryInterface.sol

</details>

### 钻石型控制器

**范围**：升级核心池中的控制器合约，实现钻石型模式。已在 [VIP-174](https://app.venus.io/#/governance/proposal/174) 中启用。

- [Fairyproof 审计报告 (2023/06/25)](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/040_diamondComptroller_fairyproof_20230625.pdf)

- [Peckshield 审计报告 (2023/07/28)](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/042_diamondComptroller_peckshield_20230718.pdf)

- [Certik 审计报告](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/042_diamondComptroller_peckshield_20230718.pdf) [OpenZeppelin 审计报告 (2023/08/03)](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/044_diamondComptroller_certik_20230803.pdf)

- [OpenZeppelin 审计报告 (2023/08/17)](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/049_diamondComptroller_openzeppelin_20230817.pdf)

- [Quantstamp 审计报告 ... (2023/09/20)](https://github.com/VenusProtocol/venus-protocol/blob/8553387f2277be152883b4ee22211b77a8cbe5f6/audits/047_diamondComptroller_quantstamp_20230919.pdf)

<details>

<summary>详细范围</summary>

**待审计代码**：https://github.com/VenusProtocol/venus-protocol/pull/224

**上次提交**：331394866b0b78ea3b65efe03931acd582d0382e

审计范围内的文件：

- `contracts/Comptroller/ComptrollerStorage.sol`

- `contracts/Comptroller/Diamond/Diamond.sol`

- `contracts/Comptroller/Diamond/facets/FacetBase.sol`

- `contracts/Comptroller/Diamond/facets/MarketFacet.sol`

- `contracts/Comptroller/Diamond/facets/PolicyFacet.sol`

- `contracts/Comptroller/Diamond/facets/RewardFacet.sol`

- `contracts/Comptroller/Diamond/facets/SetterFacet.sol`

- `contracts/Comptroller/Diamond/facets/XVSRewardsHelper.sol`

- `contracts/Comptroller/Diamond/interfaces/IDiamondCut.sol`

- `contracts/Comptroller/Diamond/interfaces/IMarketFacet.sol`

- `contracts/Comptroller/Diamond/interfaces/IPolicyFacet.sol`

- `contracts/Comptroller/Diamond/interfaces/IRewardFacet.sol`

- `contracts/Comptroller/Diamond/interfaces/ISetterFacet.sol`

- `contracts/Lens/ComptrollerLens.sol`

- `contracts/Lens/SnapshotLens.sol`

</details>

### BUSDLiquidator

**Scope**: Contract to forcibly liquidate BUSD positions after enabling the ["forced liquidations" feature](./guides/market-interaction/liquidation.md#forced-liquidations) in the BUSD market, in the [VIP-191](https://app.venus.io/#/governance/proposal/191)

* [Peckshield audit report (2023/10/20)](https://github.com/VenusProtocol/venus-protocol/blob/b9dff61b16c4002db4cc01d3f25db160209a3d8d/audits/077_busdLiquidator_peckshield_20231020.pdf)
<details>

<summary>详细范围</summary>

**待审计代码**：https://github.com/VenusProtocol/venus-protocol/pull/362

**上次提交**：592b022723740c6b7b066445f407f12253d85637

</details>

### 隔离池中的强制清算

**范围**：升级隔离池中的 Comptroller 合约，添加[“强制清算”功能](./guides/market-interaction/liquidation.md#forced-liquidations)，该功能已在[VIP-186](https://app.venus.io/#/governance/proposal/186)上启用

* [Certik 审计报告](https://app.venus.io/#/governance/proposal/186) (2023/10/16)](https://github.com/VenusProtocol/isolated-pools/blob/41a96ca24b0e32b8087ea7b916ae2864cbf1a05f/audits/078_forcedLiquidations_certik_20231016.pdf)

### 核心池中的强制清算

**范围**：升级核心池中的 Comptroller 合约，添加[“强制清算”功能](./guides/market-interaction/liquidation.md#forced-liquidations)，该功能已在[VIP-172](https://app.venus.io/#/governance/proposal/172)上启用

* [Certik 审计报告](https://github.com/VenusProtocol/isolated-pools/blob/41a96ca24b0e32b8087ea7b916ae2864cbf1a05f/audits/078_forcedLiquidations_certik_20231016.pdf) （2023/09/16）](https://github.com/VenusProtocol/venus-protocol/blob/80cf9b36ea900d71c5e97a5b1d5e2706ecefb9c3/audits/072_forcedLiquidations_certik_20230916.pdf)

* [Peckshield 审计报告（2023/09/16）](https://github.com/VenusProtocol/venus-protocol/blob/80cf9b36ea900d71c5e97a5b1d5e2706ecefb9c3/audits/073_forcedLiquidations_peckshield_20230916.pdf)

### 风险基金和资金缺口处理

**范围**：`风险基金`、`资金缺口`和在 [VIP-170](https://app.venus.io/#/governance/proposal/170) 中启用的 [isolated-pools 代码库](https://github.com/VenusProtocol/isolated-pools) 中的 `ProtocolShareReserve` 合约。

这些合约在 [VIP-134](https://app.venus.io/#/governance/proposal/134) 中启动 Isolated Pools 之前进行的审计范围内。这些合约进行了一些升级，并针对这些变更进行了新一轮审计。

* [Certik 审计报告 - 2023/08/24](https://github.com/VenusProtocol/isolated-pools/blob/1116c02c253e82cb0483afc47fb1fa104152601e/audits/061_riskFundShortfall_certik_20230824.pdf)

* [Peckshield 审计报告 - 2023/08/25](https://github.com/VenusProtocol/isolated-pools/blob/1116c02c253e82cb0483afc47fb1fa104152601e/audits/062_riskFundShortfall_peckshield_20230825.pdf)

### 挂钩稳定性模块 (PSM)

**范围**：挂钩VAI/USDT 的稳定性模块合约（https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/PegStability/PegStability.sol）已在 [VIP-157](https://app.venus.io/#/governance/proposal/157) 上启用

* [Quantstamp 审计报告 - 2023/08/07](https://github.com/VenusProtocol/venus-protocol/blob/90dfde3af29470938032c88ad7f9b31b3a4c503b/audits/057_psm_quantstamp_20230807.pdf)

* [Certik 审计报告 - 2023/05/24](https://github.com/VenusProtocol/venus-protocol/blob/90dfde3af29470938032c88ad7f9b31b3a4c503b/audits/021_psm_certik_20230524.pdf)

* [Peckshield 审计报告 - 2023/04/26](https://github.com/VenusProtocol/venus-protocol/blob/90dfde3af29470938032c88ad7f9b31b3a4c503b/audits/022_psm_peckshield_20230426.pdf)

* [Hacken 审计报告 - 2023/06/26](https://github.com/VenusProtocol/venus-protocol/blob/90dfde3af29470938032c88ad7f9b31b3a4c503b/audits/028_psm_hacken_20230626.pdf)

### Oracle 升级 (2023/07/24)

**范围**：升级在 [VIP-145](https://app.venus.io/governance/proposal/145) 上启用的弹性价格馈送。

* [Peckshield 审计报告 - 2023/07/12](https://github.com/VenusProtocol/oracle/blob/fb02cdd3865fb5c34e0cd65cbeda02f87841371a/audits/045_getPrice_peckshield_20230712.pdf)

* [Certik 审计报告 - 2023/07/17](https://github.com/VenusProtocol/oracle/blob/fb02cdd3865fb5c34e0cd65cbeda02f87841371a/audits/043_getPrice_certik_20230717.pdf)

### 预言机

**范围**：在 [VIP-123](https://app.venus.io/governance/proposal/123) 上启用新的弹性价格信息流。

* [OpenZeppeling 审计报告 - 2023/06/06](https://github.com/VenusProtocol/oracle/blob/6f7a3d8769c28881661953e7ee3299b1d5b31e17/audits/026_oracles_openzeppelin_20230606.pdf)

* [Peckshield 审计报告 - 2023/04/24](https://github.com/VenusProtocol/oracle/blob/6f7a3d8769c28881661953e7ee3299b1d5b31e17/audits/013_oracles_peckshield_20230424.pdf)

* [Certik 审计报告 - 2023/05/22](https://github.com/VenusProtocol/oracle/blob/6f7a3d8769c28881661953e7ee3299b1d5b31e17/audits/024_oracles_certik_20230522.pdf)

* [Hacken 审计报告 - 2023/04/26](https://github.com/VenusProtocol/oracle/blob/6f7a3d8769c28881661953e7ee3299b1d5b31e17/audits/016_oracles_hacken_20230426.pdf)

* [HashEx 漏洞报告 - 2024/02/01](https://github.com/VenusProtocol/oracle/blob/567b057fd010a0359651db5604defec35a378cf1/audits/097_twap_hashex_20240201.pdf)。不存在风险，因为 Venus 协议完全不使用 TWAP 预言机。为了避免任何混淆，`TwapOracle` 已[从代码库中移除](https://github.com/VenusProtocol/oracle/pull/167)。

### Vaults

**范围**：升级 XVSVault、VAIVault 和 VRTVault，已在 [VIP-127](https://app.venus.io/governance/proposal/127) 上启用。

* [Quantstamp 审计报告 - 2023/05/19](https://github.com/VenusProtocol/venus-protocol/blob/cb91c322f9d267cac11f532924b07a4b1991be64/audits/031_vaults_quantstamp_20230519.pdf)

* [Peckshield 审计报告 1 - 2023/03/22](https://github.com/VenusProtocol/venus-protocol/blob/cb91c322f9d267cac11f532924b07a4b1991be64/audits/012_vaults_peckshield_20230322.pdf)

* [Peckshield 审计报告 2 - [2023/04/19](https://github.com/VenusProtocol/venus-protocol/blob/cb91c322f9d267cac11f532924b07a4b1991be64/audits/018_vaults_peckshield_20230419.pdf)

* [Fairyproof 审计报告 - 2023/05/17](https://github.com/VenusProtocol/venus-protocol/blob/cb91c322f9d267cac11f532924b07a4b1991be64/audits/025_vaults_fairyproof_20230517.pdf)

* [Certik 审计报告 - 2023/06/04](https://github.com/VenusProtocol/venus-protocol/blob/f01158edba6ecade4d8bf72d109d80e1f0c8f792/audits/038_vaults_certik_20230604.pdf)

### 隔离池

**范围**：隔离池，首次在 [VIP-134](https://app.venus.io/governance/proposal/134) 中启用。

* [Certik 审计报告](https://github.com/VenusProtocol/isolated-pools/blob/1d60500e28d4912601bac461870c754dd9e72341/audits/036_isolatedPools_certik_20230619.pdf)

* [Certik 审计报告（奖励分配器）](https://github.com/VenusProtocol/isolated-pools/blob/95b1c8906774e5d849dd1e00ba7c608c679f8977/audits/051_rewardsDistributor_certik_20230610.pdf)

* [Peckshield 审计报告](https://github.com/VenusProtocol/isolated-pools/blob/1d60500e28d4912601bac461870c754dd9e72341/audits/036_isolatedPools_certik_20230619.pdf) 1](https://github.com/VenusProtocol/isolated-pools/blob/c801e898e034e313e885c5d486ed27c15e7e2abf/audits/003_isolatedPools_peckshield_20230112.pdf)

* [Peckshield 审计报告 2](https://github.com/VenusProtocol/isolated-pools/blob/1d60500e28d4912601bac461870c754dd9e72341/audits/037_isolatedPools_peckshield_20230625.pdf)

* [Hacken 审计报告](https://github.com/VenusProtocol/isolated-pools/blob/c801e898e034e313e885c5d486ed27c15e7e2abf/audits/016_isolatedPools_hacken_20230426.pdf)

* [Code4rena 竞赛 - 2023/05/15](https://code4rena.com/contests/2023-05-venus-protocol-isolated-pools)

### 清算人合约中的自动收益分配

**范围**：将[自动收益分配](./whats-new/automatic-income-allocation.md)集成到BNB链核心池使用的[清算人合约](https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/Liquidator/Liquidator.sol)中。

* [OpenZeppelin 审计报告（2023年7月20日）](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/048_liquidator_openzeppelin_20230720.pdf)

* [Quantstamp 审计报告（2023年7月17日）](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/046_liquidator_quantstamp_20230717.pdf)

* [Certik 审计报告（2023年7月4日）](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/041_liquidator_certik_20230704.pdf)

* [Peckshield 审计报告](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/041_liquidator_certik_20230704.pdf) (2023年7月5日)](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/039_liquidator_peckshield_20230705.pdf)

<details>

<summary>详细范围</summary>

- 在 `venus-protocol` 代码库中提交拉取请求 [#241](https://github.com/VenusProtocol/venus-protocol/pull/241)。

- contracts/Liquidator/Liquidator.sol

- contracts/Liquidator/LiquidatorStorage.sol

</details>

### 交换路由器

**范围**：SwapRouter 合约，已在 [VIP-131](https://app.venus.io/governance/proposal/131) 上启用。

* [OpenZeppelin 审计报告 - 2023/06/16](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/027_swapRouter_openzeppelin_20230616.pdf)

* [Certik 审计报告 - 2023/05/30](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/030_swapRouter_certik_20230530.pdf)

* [Peckshield 审计报告 - 2023/04/19](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/014_swapRouter_peckshield_20230419.pdf)

* [Hacken 审计报告 - 2023年6月28日](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/029_swapRouter_hacken_20230628.pdf)

### VToken

**范围**：Venus平台的委托借贷。升级BUSD、USDC、USDT、BTCB和ETH市场，以降低2022年9月BNB桥事件给Venus平台带来的风险。已在[VIP-99](https://app.venus.io/governance/proposal/99)上执行。

* [Peckshield审计报告 - 2023年2月27日](https://github.com/VenusProtocol/venus-protocol/blob/develop/audits/009_vtoken_peckshield_20230227.pdf)
