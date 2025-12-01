# 利率模型

### 概述

Venus Protocol 使用两种不同的模型为市场提供浮动利率：跳跃利率模型和白皮书利率模型。每个市场都采用其中一种模型运行，并在市场启动时设定特定的风险参数。值得注意的是，社区可以通过治理流程更新这些参数。此外，部分市场采用稳定利率，该机制在 Venus V4 中引入。

#### **跳跃利率模型**

跳跃利率模型使用以下公式计算利率：

借款利率：

$$

borrow\_rate(u) = b + a_1 \cdot kink + a_1 \cdot \min(0, u-kink) + a_2 \cdot \max(0, u-kink)

$$

供给利率：

$$

supply\_rate(u) = borrow\_rate(u) \cdot us \cdot (1 - reserve\_factor)

$$

其中，

$$

us = \frac{borrows}{cash + borrows - reserves + badDebt}

$$

当利用率处于两个不同的范围内时，借款利率采用不同的公式：

如果 `u < kink`：

$$

borrow\_rate(u) = a_1 \cdot u + b

$$

如果 `u > kink`：

$$

borrow\_rate(u) = a_1 \cdot kink + a_2 \cdot (u-kink) + b

$$

**模型参数**

* `a1`：可变利率斜率1。

* `a2`：可变利率斜率2。

* `b`：每个区块的基准利率（`baseRatePerYear / blocksPerYear`）。

* `kink`：最优利用率，即可变利率斜率从斜率1变为斜率2时的利用率。

* `reserve_factor`：从协议中提取的利息收入的一部分，即不分配给供应商的部分。

利用率 (`u`) 定义为：

$$

utilization\_rate = \frac{(borrows + bad\_debt)}{(cash + borrows + bad\_debt - reserves)}
$$

其中：

* `borrows`：市场上的借款金额，以基础资产计，不包括坏账。

* `cash`：市场在特定时间点持有的基础资产总额。

* `reserves`：市场持有但无法供借款人或供应商使用的基础资产金额，用于协议代币经济模型定义的各种用途。

* `bad_debt`：清算人尽可能偿还债务并将抵押品减少到最低限度后，剩余债务被标记为坏账。坏账不计息。

#### 白皮书利率模型

白皮书利率模型更为简洁，其中借款利率与利用率呈线性关系：

对于借款利率：

$$

borrow\_rate (u) = a \cdot u + b

$$

对于供给利率：

$$

supply\_rate(u) = borrow\_rate(u) \cdot us \cdot (1 - reserve\_factor)

$$

其中，

$$

us = \frac{borrows}{cash + borrows - reserves + badDebt}

$$