# VAI 单位审计师

这是 VAI 单位审计师的代理合同。

# Solidity API

### \_setPendingImplementation

* Admin Functions \*\*

```solidity
function _setPendingImplementation(address newPendingImplementation) public returns (uint256)
```

---

### \_acceptImplementation

接受新的 comptroller 实现。msg.sender 必须处于 pendingImplementation 状态。

```solidity
function _acceptImplementation() public returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint 0 表示成功，否则表示失败（详情请参阅 ErrorReporter.sol） |

---

### \_setPendingAdmin

开始管理员权限转移。newPendingAdmin 必须调用 `_acceptAdmin` 来完成转移。

```solidity
function _setPendingAdmin(address newPendingAdmin) public returns (uint256)
```

#### Parameters

| Name | Type | Description |
| ---- | ---- | ----------- |
| newPendingAdmin | address | 新增待处理管理员。 |

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint 0 表示成功，否则表示失败（详情请参阅 ErrorReporter.sol） |

---

### \_acceptAdmin

接受管理员权限转移。msg.sender 必须为 pendingAdmin。

```solidity
function _acceptAdmin() public returns (uint256)
```

#### Return Values

| Name | Type | Description |
| ---- | ---- | ----------- |
| \[0] | uint256 | uint 0 表示成功，否则表示失败（详情请参阅 ErrorReporter.sol） |

---
