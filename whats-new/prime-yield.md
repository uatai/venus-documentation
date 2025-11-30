---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 金星协议高级会员Venus Prime

### **概述**

金星协议 隆重推出 金星协议高级会员Venus Prime，一项旨在提升用户参与度和促进协议发展的革命性激励计划。作为 金星协议代币经济学 v3.1 的重要组成部分，金星协议高级会员Venus Prime 旨在提升奖励并促进 $XVS 质押，重点关注 USDT、USDC、BTC 和 ETH 等市场。

### **金星协议高级会员Venus Prime 要点**

金星协议高级会员Venus Prime 的独特之处在于其自给自足的奖励系统。奖励并非来自外部来源，而是源自协议的收益，从而打造一个可持续发展的持续增长型计划。

符合条件的 $XVS 持有者将获得一枚独特的、不可转让的 Soulbound 代币，该代币可提升在特定市场的奖励。

**金星协议高级会员Prime代币：**

金星协议高级会员Venus Prime通过两种独特的金星协议高级会员Prime代币鼓励用户参与：

1. **可撤销金星协议高级会员Prime代币：**

* 用户需要连续90天质押至少1000个XVS。

* 90天后，用户可以铸造自己的金星协议高级会员Prime代币。

* 如果用户决定提取XVS，且其余额低于1000，则其金星协议高级会员Prime代币将被自动撤销。

* 在BNB链上，可撤销Prime代币的数量上限为500个。[来源](https://app.venus.io/#/governance/proposal/201)。可通过VIP进行更改。

2. **不可撤销的“OG”Prime代币（第二阶段）：**
   * _待定_

<figure><img src="../.gitbook/assets/6e01c33d-ac9e-41d6-9542-fc2f3b0ecb90.png" alt=""><figcaption></figcaption></figure>

### **预期影响及上线**

金星协议高级会员Venus Prime 旨在激励用户进行更大额的质押，并促进用户多元化参与。预计这将显著提升 XVS 的质押量、总锁定价值 (TVL) 以及市场增长。

金星协议高级会员Venus Prime 致力于提升用户忠诚度，并推动协议的整体发展。通过鼓励长期质押、抑制过早提现以及激励更大额的质押，金星协议高级会员Venus Prime 为用户参与度和流动性开辟了新的道路，助力 金星协议的成功。

立即质押您的 $XVS 代币，即可参与金星协议高级会员 Venus Prime，体验 DeFi 领域激动人心的新项目。

### 技术奖励详情

**奖励公式：柯布-道格拉斯函数**

$$
Rewards_{i,m} = \Gamma_m \times \mu \times \frac{\tau_{i}^\alpha \times \sigma_{i,m}^{1-\alpha}}{\sum_{j,m} \tau_{j}^\alpha \times \sigma_{j,m}^{1-\alpha}}
$$

地址:

* $$Rewards_{i,m}$$ = Rewards for user $$i$$ in market $$m$$
* $$\Gamma_m$$ = Protocol Reserve Revenue for market $$m$$
* $$μ$$ = Proportion to be distributed as rewards
* $$α$$ = Protocol stake and supply & borrow amplification weight
* $$τ_{i}​$$ = XVS staked amount for user $$i$$
* $$\sigma_i$$ = Sum of **qualified** supply and borrow balance for user $$i$$
* $$∑_{j,m}​$$ = Sum for all users $$j$$ in markets $$m$$

**符合条件的 XVS 质押：**

$$
\tau_i = \begin{cases} \min(100000, \tau_i) & \text{if } \tau_i \geq 1000 \\ 0 & \text{otherwise} \end{cases}
$$

**合格的供应和借款：**

$$
\begin{align*} \sigma_{i,m} &= \min(\tau_i \times borrowMultiplier_m, borrowedAmount_{i,m}) \\ &+ \min(\tau_i \times supplyMultiplier_m, suppliedAmount_{i,m}) \end{align*}
$$

_注意：合格供应量和借款金额将受到限制，由质押的 XVS 限额和市场乘数决定。_

### 用户奖励示例：

**模型参数**

* $$α$$ = 0.5
* $${\sum_{j,BTC} \tau_{j}^\alpha \times \sigma_{j,BTC}^{1-\alpha}}$$ = 744,164
* $$\Gamma_{BTC}$$ = 8 BTC
* $$\mu$$ = 0.2
* BTC Supply Multiplier = 2
* XVS Price = $4.0

**用户参数**

| 用户参数         | 代币价值      | 美元价值 |
| --------------- | ----------- | --------- |
| 已质押 XVS       | 1,200       | $4,800    |
| BTC 供应         | 0.097       | $2,500    |

**合格的 已质押 XVS**

$$\tau_i=min(100000,\text{ } 1200)$$

**合格的供应和借贷**

$$\sigma_{i,\text{BTC}} = \textit{min}(\text{\$9600}, \text{\$2500})$$

**用户奖励**

$$Rewards_{i, BTC} = 8\times 0.2\times \dfrac{1,200^{0.5}\times 2,500^{0.5}}{744,164}$$

$$Rewards_{i, BTC} = \ 0.00372$$

$$\text{User APY Increase} = \dfrac{0.00372}{0.097} = 3.88\%$$

**预期收益函数**

只要质押金额和市场参与度在下方“技术奖励详情”部分概述的限制范围内，金星高级会员Venus Prime 计划中的奖励就会随着用户增加其 XVS 质押金额而自动增加。

<figure><img src="../.gitbook/assets/apy_graph_transparent_2500_corrected_labels.png" alt=""><figcaption><p><em>请注意，奖励会根据市场总参与度和 XVS 质押数量而有所不同，如上文公式和示例所示。</em></p></figcaption></figure>

上图展示了 XVS 质押数量增加与市场奖励之间的关系，假设 BTC 供应市场参与度保持在 2500 美元不变。这有助于直观地了解质押数量的增加如何影响年化收益率 (APY)。
