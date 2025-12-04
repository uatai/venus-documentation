---

金星 协议 API，提供对已索引协议数据的访问。

---

# API

金星 协议 API 提供两类端点：

**市场数据 -** 与借贷市场相关的端点

**活动 -** 与用户与市场互动相关的端点

**治理 -** 提供有关提案和投票活动的信息的端点

## 基本 URL

该 API 无需身份验证即可在测试网和主网上使用。

主网：[https://api.venus.io](https://api.venus.io/api/governance/venus)

测试网：[https://testnetapi.venus.io](https://testnetapi.venus.io/api/transactions/)

## 版本控制

端点使用 `accept-version` 标头进行版本控制。此标头的值可以是 `stable` 或 `next`。默认情况下返回 `stable` 版本。当有 `next` 版本可用时，`stable` 版本号会添加一个 `Warning - 299` 标头，其中包含重大变更信息。要接收此新版本，可以将 `accept-version` 标头设置为 `next`。

当最新的 `next` 版本成为稳定版本，而之前的稳定版本被弃用时，`accept-version` 的两个值都将返回最新版本。此时使用 `next` 标头会添加一个 `Warning - 299` 标头，提醒客户端移除 `accept-version: next`，以避免将来接收意外变更。

#### 版本控制流程

以下步骤描述了端点升级到新版本的过程：

1. `next` 版本可用，可通过 `accept-version: next` 标头访问。`Warning - 299` 标头会添加到稳定版本，其中包含重大变更的详细信息。

2. 客户端将有充足的时间升级到下一个版本。

3. 之前的稳定版本将被弃用，下一个版本将成为稳定版本。使用 `accept-version: next` 标头会发出警告，提示移除该标头或使用稳定版本。

4. 客户端移除 `accept-version: next` 标头，以避免接收意外更改。

5. 该端点现已准备好发布新版本。

### 资金池端点

{% swagger src="../.gitbook/assets/swagger.json" path="/pools" method="get" %}

[swagger.json](../.gitbook/assets/swagger.json)

{% endswagger %}

### 市场端点

{% swagger src="../.gitbook/assets/swagger.json" path="/markets" method="get" %}

[swagger.json](../.gitbook/assets/swagger.json)

{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/markets/history" method="get" %}

[swagger.json](../.gitbook/assets/swagger.json)

{% endswagger %}

### 治理端点

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/proposals/{proposalId}/voteSummary" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/voters/{address}/summary" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/voters/{address}/history" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/voters" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/proposals" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/proposals/votes" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

{% swagger src="../.gitbook/assets/swagger.json" path="/governance/proposals/{proposalId}" method="get" %}
[swagger.json](../.gitbook/assets/swagger.json)
{% endswagger %}

