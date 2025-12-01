
174 / 5,000
# VAI Comptroller

这是 VAIUnitroller 代理的实现合约

# Solidity API

### INITIAL\_VAI\_MINT\_INDEX

用于利息计算的初始指数

```solidity
uint256 INITIAL_VAI_MINT_INDEX
```

---

### CORE\_POOL\_ID

poolId for core Pool

```solidity
uint96 CORE_POOL_ID
```

---

### mintVAI

mintVAI 函数会从协议中铸造 VAI 并将其转入用户账户，同时增加用户的借贷余额。

铸造的 VAI 数量必须小于用户的账户流动性和铸造 VAI 的限额。

```solidity
function mintVAI(uint256 mintVAIAmount) external returns (uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| mintVAIAmount | uint256 | 待铸造的VAI数量。 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 成功返回 0，否则返回错误代码 |

---

### 偿还 VAI

偿还功能会将 VAI 利息转入协议，并将剩余部分销毁，
从而减少借款人的借款余额。在偿还 VAI 之前，用户必须先授权

VAIController 访问其 VAI 余额。

```solidity
function repayVAI(uint256 amount) external returns (uint256, uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| amount | uint256 | 需偿还的VAI金额。 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 错误代码（0=成功，否则为失败，请参阅 ErrorReporter.sol） |
| \[1] | uint256 | 实际还款金额 |

---

### 代还 VAI

代还功能会将 VAI 利息转入协议，并将剩余部分销毁，

从而减少借款人的借款余额。借入的 VAI 由其他用户（可能是借款人本人）偿还。

在偿还 VAI 之前，付款人必须先授权 VAIController 访问其 VAI 余额。

```solidity
function repayVAIBehalf(address borrower, uint256 amount) external returns (uint256, uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| borrower | address | 用于偿还债务的账户。 |
| amount | uint256 | 需偿还的VAI金额。 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 错误代码（0=成功，否则为失败，请参阅 ErrorReporter.sol） |
| \[1] | uint256 | 实际还款金额 |

---

### 清算 VAI

发卡人清算 VAI 铸币者的抵押品。查获的抵押品将移交给清算人。

```solidity
function liquidateVAI(address borrower, uint256 repayAmount, contract VTokenInterface vTokenCollateral) external returns (uint256, uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| borrower | address | 借款人将被清算 |
| repayAmount | uint256 | 需要偿还的借入资产金额 |
| vTokenCollateral | 合约 VTokenInterface | 用于从借款人处扣押抵押品的市场 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 错误代码（0=成功，否则为失败，请参阅 ErrorReporter.sol） |
| \[1] | uint256 | 实际还款金额 |

---

### \_setComptroller

设置新的财务主管

```solidity
function _setComptroller(contract ComptrollerInterface comptroller_) external returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint256 0=成功，否则为失败（详情请参阅 ErrorReporter.sol） |

---

### 设置 Prime 代币

设置高级用户 Prime 代币合约地址

```solidity
function setPrimeToken(address prime_) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| prime\_ | address | 主代币合约的新地址 |

---

### 设置 VAI 代币

设置 VAI 代币合约地址

```solidity
function setVAIToken(address vai_) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| vai\_ | address | VAI代币合约的新地址 |

---

### 仅限 Prime 高级会员持有者铸造权限

仅限 Prime 高级会员持有者开启铸造权限模式

```solidity
function toggleOnlyPrimeHolderMint() external returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint256 0=成功，否则为失败（详情请参阅 ErrorReporter.sol） |

---

```solidity
struct AccountAmountLocalVars {
  uint256 oErr;
  enum CarefulMath.MathError mErr;
  uint256 sumSupply;
  uint256 marketSupply;
  uint256 sumBorrowPlusEffects;
  uint256 vTokenBalance;
  uint256 borrowBalance;
  uint256 exchangeRateMantissa;
  uint256 oraclePriceMantissa;
  struct ExponentialNoError.Exp exchangeRate;
  struct ExponentialNoError.Exp oraclePrice;
  struct ExponentialNoError.Exp tokensToDenom;
}
```

### 获取可铸造 VAI 数量

该函数根据用户的账户流动性和 VAI 铸造率，返回用户可铸造的 VAI 数量。

如果 mintEnabledOnlyForPrimeHolder 为真，则只有 Prime 持有者才能铸造 VAI。

```solidity
function getMintableVAI(address minter) public view returns (uint256, uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| minter | address | 用于检查可铸造 VAI 的账户 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 错误代码（0=成功，否则为失败，详情请参阅 ErrorReporter.sol） |
| \[1] | uint256 | 可铸造数量（精确到小数点后18位） |

---

### \_setTreasuryData

更新国库数据

```solidity
function _setTreasuryData(address newTreasuryGuardian, address newTreasuryAddress, uint256 newTreasuryPercent) external returns (uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newTreasuryGuardian | address | 新财国库点地址 |
| newTreasuryAddress | address | 新国库地址 |
| newTreasuryPercent | uint256 | 新的VAI铸币费用百分比（该VAI将上缴国库） |

---

### 获取 VAI 还款利率

根据 VAI 价格获取 VAI 年利率

```solidity
function getVAIRepayRate() public view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint256 年度VAI利率 |

---

### 获取每区块的VAIRepayRatePerBlock利率

获取每区块的利率

```solidity
function getVAIRepayRatePerBlock() public view returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint256 每个区块利率 |

---

### 获取 VAI 矿商的最新利率指数

获取 VAI 矿商的最新利率指数

```solidity
function getVAIMinterInterestIndex(address minter) public view returns (uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| minter | address | VAI铸造者地址 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint256 返回铸造者的利率指数 |

---

### 获取 VAI 还款额

获取用户当前需要偿还的 VAI 总额

```solidity
function getVAIRepayAmount(address account) public view returns (uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| account | address | VAI借款人的地址 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | (uint256) 用户需要偿还的VAI总额 |

---

### 获取 VAI 还款金额

计算用户需要偿还的 VAI 金额

```solidity
function getVAICalculateRepayAmount(address borrower, uint256 repayAmount) public view returns (uint256, uint256, uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| borrower | address | VAI借款人的地址 |
| repayAmount | uint256 | 返还的VAI金额 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | 待销毁的VAI量 |
| \[1] | uint256 | 用户需要支付的VAI金额（按当前利率计算） |
| \[2] | uint256 | 用户需支付的过去利息金额（VAI）。 |

---

### 计提 VAI 利息

对已发行的 VAI 计提利息

```solidity
function accrueVAIInterest() public
```

---

### 设置访问控制

设置此合约的访问控制地址。

```solidity
function setAccessControl(address newAccessControlAddress) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newAccessControlAddress | address |访问控制的新地址 |

---

### 设置基准利率

设置 VAI 借款基准利率

```solidity
function setBaseRate(uint256 newBaseRateMantissa) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newBaseRateMantissa | uint256 | 基本利率乘以 10\*\*1 |

---

### 设置浮动利率

设置 VAI 借款浮动利率

```solidity
function setFloatRate(uint256 newFloatRateMantissa) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newFloatRateMantissa | uint256 | VAI浮动利率乘以10\*\*18 |

---

### 设置接收方

设置 VAI 稳定费接收方地址

```solidity
function setReceiver(address newReceiver) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newReceiver | address | VAI费用接收方的地址 |

---

### setMintCap

设置 VAI 铸造上限

```solidity
function setMintCap(uint256 _mintCap) external
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| \_mintCap | uint256 | 可铸造的VAI数量 |

---

### 获取 VAI 地址

返回 VAI 令牌的地址

```solidity
function getVAIAddress() public view virtual returns (address)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | address | VAI的地址 |

---
