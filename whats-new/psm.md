# 锚定稳定模块

## 概述

锚定稳定模块 (PSM) 是 金星协议 的关键组件，旨在将 VAI 稳定币的价值维持在 1 美元。其功能类似于 MakerDAO 为 DAI 提供的系统。PSM 合约使用两种稳定币：VAI（目标稳定币）和 USDT（用于帮助维持锚定）。

## 功能

**兑换功能**：

* 用户可以使用 1 VAI = 1 美元的固定汇率兑换 VAI 和 USDT。

* 如果 PSM 中有足够的 USDT，用户可以向 PSM 发送 VAI 并接收 USDT。

* 如果 PSM 的 VAI 发行量未达到上限，用户可以向 PSM 发送 USDT 并接收 VAI。

**无稳定费**

通过 PSM 发行的 VAI 不产生任何利息或稳定费。

**可配置参数**：

PSM 合约有三个可配置变量，可通过 Venus 改进提案 (VIP) 设置：

* `feeIn`：用户向 PSM 发送 USDT 时收取的手续费。

* `feeOut`：用户向 PSM 发送 VAI 时收取的手续费。

* `maxMintedVAI`：PSM 可分发的 VAI 最大数量。超过此限制的转换将被撤销。

**费用发送至金库**：每次操作收取的手续费将发送至 金星协议 金库合约。

**与预言机价格集成**：PSM 会考虑稳定币的美元价值，以准确地将 VAI 与其价值挂钩。

## 转换函数

### 函数 `swapStableForVAI`

此函数允许用户将配对的稳定币 (USDT) 兑换为 VAI。

**预期参数**：

* `receiver`：接收 VAI 的用户地址。

* `amount`：发送方希望兑换的稳定币 (USDT) 数量。

收到的稳定币将由 PSM 持有，并且 `feeIn` 指定的手续费将发送到国库合约。

此函数返回已转账给接收方的 VAI 数量。

### 函数 `swapVAIForStable`

此函数允许用户将 VAI 兑换为配对的稳定币 (USDT)。

**预期参数**：

* `receiver`：接收稳定币的用户地址。

* `amount`：用户预期收到的稳定币 (USDT) 数量。

收到的 VAI 将被销毁，并且 `feeOut` 指定的手续费将发送到国库合约。

此函数返回从发送方转出的 VAI 金额（已销毁金额 + 手续费）。

## 预览功能

PSM 还提供预览功能，帮助用户预估转换操作的结果：

### `previewSwapVAIForStable(uint256 stableTknAmount)`

返回发送方为接收指定数量的稳定币而转移的 VAI 数量（已销毁 + 手续费）。

### `previewSwapStableForVAI(uint256 stableTknAmount)`

返回接收方在执行 `swapVAIForStable` 函数并使用指定数量的稳定币后将收到的 VAI 数量。

## 集成预言机价格

<figure><img src="../.gitbook/assets/psm.png" alt="金星锚定稳定模块考虑的美元价格"><figcaption></figcaption></figure>

为了保护 VAI 的价值并考虑配对稳定币的美元价值，PSM 集成了 Resilient Oracle。以下规则适用：

**swapVAIForStable**（用户发送 VAI 并接收 USDT）

* 如果配对稳定币的预言机价格低于 1 美元，则兑换率为 1 个稳定币 = 1 美元。

{% hint style="info" %}
**例如，如果 1 USDT = 0.90 美元**

* 输入：用户希望收到 1 USDT。

* 计算：考虑的转换率为 max(1, 0.9) => 1 USDT = 1 美元 = 1 VAI。

* 用户需要发送 1 VAI（1 USDT * 1 美元/USDT）+ 手续费。

* 假设 feeOut = 10%，则 0.10 VAI 将发送到金库，1 VAI 将被销毁，最终用户提供的 VAI 总数为 1.1 VAI。

* 手续费的计算基于待销毁的“本金”VAI 金额（1 VAI = 1 美元）。

{% endhint %}

* 如果配对稳定币的预言机价格高于 1 美元，则转换率为 1 稳定币 = 预言机价格。

{% hint style="info" %}
**例如，如果 1 USDT = 1.1 美元**

* 输入：用户希望收到 10 USDT。

* 计算：考虑的兑换率为 max(1, 1.1) => 1 USDT = 1.1 美元 = 1.1 VAI。

* 用户需要发送 11 VAI（10 USDT * 1.1 美元/USDT）+ 手续费。

* 假设 feeOut = 10%，则 1.1 VAI 将发送到金库，10 VAI 将被销毁，最终用户提供的 VAI 总数为 12.1 VAI。

* 手续费的计算基于待销毁的“本金”VAI 金额（11 VAI = 11 美元）。

{% endhint %}

**swapStableForVAI**（用户发送 USDT 并接收 VAI）

* 如果配对稳定币的预言机价格低于 1 美元，则兑换率为 1 个稳定币 = 预言机价格。

{% hint style="info" %}
**For example if 1 USDT = $0.90**

* 输入：用户希望向 PSM 发送 10 USDT。

* 计算：考虑的兑换率为 min(1, 0.9) => 10 USDT = 9 美元 = 9 VAI。

* 用户将收到 9 VAI (10 USDT * 0.9) - 手续费。

* 假设 feeIn = 10%，则 0.9 VAI 将发送到金库，8.1 VAI 将发送给用户。

* 手续费的计算基于“本金”VAI 金额 (9 VAI = 9 美元)。

{% endhint %}

* 如果配对稳定币的预言机价格高于 1 美元，则兑换率为 1 个稳定币 = 1 美元。

{% hint style="info" %}

**例如，如果 1 USDT = 1.1 美元**

* 1 USDT = 1.1 美元（根据我们的预言机计算的汇率）

* 输入：用户希望向 PSM 发送 10 USDT。

* 计算：使用的汇率为 min(1, 1.1) => 10 USDT = 10 美元 = 10 VAI。

* 用户将收到 10 VAI (10 USDT * 1.0) - 手续费。

* 假设 feeIn = 10%，则 1 VAI 将发送到金库，9 VAI 将发送给用户。

* 手续费的计算基于“本金”VAI 金额 (10 VAI = 10 美元)。
{% endhint %}

{% hint style="warning" %}
本文档旨在方便用户使用，并未涵盖锚定稳定性模块的技术实现细节。有关技术信息，开发人员和智能合约审计人员可以参考[智能合约代码]。(https://github.com/VenusProtocol/venus-protocol/blob/develop/contracts/PegStability/PegStability.sol).
{% endhint %}
