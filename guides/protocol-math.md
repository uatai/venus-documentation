# 协议数学

### 概述

金星 协议下的合约采用名为 Exponential.sol 的系统。该系统利用指数数学以高精度表示分数。

该系统中的大多数数字都以尾数表示，尾数是一个无符号整数，其缩放因子为 1 * 10^18。这种缩放确保了基本数学运算能够以极高的精度进行。

### vToken 和底层小数

价格和汇率根据每种资产独特的小数缩放进行调整。vToken 是 BEP-20 代币，其小数位数为 8 位。但是，其底层代币可能具有不同的小数缩放，这由名为“decimals”的公共成员指示。

更多详情，请参阅相应的代币合约地址。

{% content-ref url="../deployed-contracts/markets.md" %}

[core-pool.md](../deployed-contracts/markets.md)

{% endcontent-ref %}

### 汇率解读

vToken 的汇率​​根据 vToken 与其基础资产之间的小数位数差进行调整。

$$

oneVTokenInUnderlying = \frac{exchangeRateCurrent}{1 \times 10^{(18 + underlyingDecimals - vTokenDecimals)}}

$$

以下示例演示如何使用 Web3.js JavaScript 库确定一个 vBUSD 的 BUSD 价值。

```javascript
const vTokenDecimals = 8; // all vTokens have 8 decimal places
const underlying = new web3.eth.Contract(bep20Abi, busdAddress);
const vToken = new web3.eth.Contract(vTokenAbi, vBusdAddress);
const underlyingDecimals = await underlying.methods.decimals().call();
const exchangeRateCurrent = await vToken.methods.exchangeRateCurrent().call();
const mantissa = 18 + parseInt(underlyingDecimals) - vTokenDecimals;
const oneVTokenInUnderlying = exchangeRateCurrent / Math.pow(10, mantissa);
console.log('1 vBUSD can be redeemed for', oneVTokenInUnderlying, 'BUSD');
```

由于 BNB 没有底层合约，因此在使用 vBNB 时，您必须将“underlyingDecimals”设置为 18。

要计算可以使用 vToken 赎回的底层代币数量，您应该将 vToken 的总数乘以之前计算的“oneVTokenInUnderlying”值。

$$

underlyingTokens = vTokenAmount \times oneVTokenInUnderlying

$$

### 计算应计利息

当借入资产与供应资产的比率发生变化时，每个市场的利率都会在相应的区块中更新。利率变化的幅度取决于该市场使用的利率模型智能合约以及上述比率的变化程度。

要查看应用于每个市场的当前利率模型的可视化信息，请参阅 [Venus app](https://app.venus.io) 中的市场页面。

当任何钱包与市场的 vToken 合约交互时，市场中供应商和借款人的利息就会累积。这种交互可以是以下任何功能：铸币、赎回、借款或还款。成功执行这些功能中的任何一个都会触发 `accrueInterest` 方法，从而将利息添加到市场中每个供应商和借款人的基础余额中。利息不仅在当前区块累积，而且在之前由于未与 vToken 合约交互而未触发 `accrueInterest` 方法的任何区块中也会累积。利息仅在 vToken 合约上调用了上述方法之一的区块中累积。

让我们来看一个供应利息累积的例子：Alice 向 Venus 协议供应 1 个 BNB。在她供应时，`supplyRatePerBlock` 为 37893605 Wei，相当于每个区块 0.000000000037893605 BNB。在接下来的 3 个区块中，vBNB 合约未发生任何交互。在第 4 个区块，Bob 借入了一些 BNB。因此，Alice 的基础余额更新为 1.000000000151574420 BNB（通过将 37893605 Wei 乘以 4 个区块，再加上最初的 1 BNB 计算得出）。从此时起，Alice 的基础 BNB 余额的累计利息将基于更新后的 1.000000000151574420 BNB 值，而不是最初的 1 BNB。需要注意的是，`supplyRatePerBlock` 的值可能会随时改变。

### 使用每区块利率计算年收益率 (APY)

在每个市场中，无论是供应还是借款，都可以使用 `supplyRatePerBlock`（用于计算供应年收益率）或 `borrowRatePerBlock`（用于计算借款年收益率）值来计算年收益率 (APY)。这些利率可用于以下公式（假设按日复利计算）：

```javascript

Rate = vToken.supplyRatePerBlock(); // 整数

利率 = 37893566

BNB 尾数 = 1 * 10 ^ 18（BNB 有 18 位小数）

每日区块数 = 80 * 60 * 24（基于 BNB 链每分钟产生 80 个区块）

每年天数 = 365

年化收益率 (APY) = (((利率 / BNB 尾数) * 每日区块数) + 1) ^ (每年天数 - 1) * 100

```

以下是使用 Web3.js JavaScript 计算供应量和借贷年化收益率的示例：

```javascript
const ethMantissa = 1e18;
const blocksPerDay = 80 * 60 * 24;
const daysPerYear = 365;

const vToken = new web3.eth.Contract(vBnbAbi, vBnbAddress);
const supplyRatePerBlock = await vToken.methods.supplyRatePerBlock().call();
const borrowRatePerBlock = await vToken.methods.borrowRatePerBlock().call();
const supplyApy = Math.pow(((supplyRatePerBlock / bnbMantissa) * blocksPerDay) + 1, daysPerYear - 1) * 100;
const borrowApy = Math.pow(((borrowRatePerBlock / bnbMantissa) * blocksPerDay) + 1, daysPerYear - 1) * 100;
console.log(`Supply APY for BNB ${supplyApy} %`);
console.log(`Borrow APY for BNB ${borrowApy} %`);
```
