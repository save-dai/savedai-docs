---
description: >-
  The IAsset interface makes it easy for developers to build custom support for
  any asset token protocol.
---

# IAsset

All asset adapters must inherit from and adhere to the **`IAsset`** interface.

```javascript
interface IAsset { 
    function hold(uint256 amount) external returns (uint256);
    function getCostOfAsset(uint256 amount) external returns (uint256);
    function withdraw(uint256 amount) external returns (uint256);
    function withdrawReward() external returns (uint256);
    function getRewardsBalance() external returns (uint256);
    function transfer(address recipient, uint256 amount) external returns (bool);
    function transferFrom(address sender, address recipient, uint256 amount)
        external returns (bool);
}
```

### **`hold`** 

Gets the interest-bearing, asset tokens

```javascript
function hold(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the number underlying tokens to lend in order to receive and hold corresponding asset tokens
* **returns**: the number of asset tokens received

### **`getCostOfAsset`** 

Calculates the amount of underlying tokens needed to receive and hold a certain `amount` of asset tokens

```javascript
function getCostOfAsset(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the number of asset tokens for which the underlying token cost will be calculated
* **returns**: the number of underlying tokens needed to receive and hold a certain `amount` of asset tokens

### **`withdraw`** 

Withdraws underlying tokens in exchange for the asset tokens

```javascript
function withdraw(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the number of asset tokens to redeem in exchange for the underlying tokens
* **returns**: the amount of underlying tokens withdrawn

### **`withdrawReward`** 

Withdraws rewards or governance tokens that have been yielded from the adapter's lending protocol \(e.g., `COMP` tokens yielded from lending to the Compound protocol via the `CompoundAdapter`\)

```javascript
function withdrawReward() external returns (uint256)
```

* **returns**: the number of rewards or governance tokens withdrawn

### **`getRewardsBalance`** 

Returns the balance of rewards or governance tokens that have been yielded from the adapter's lending protocol \(e.g., `COMP` tokens yielded from lending to the Compound protocol via the `CompoundAdapter`\)

```javascript
function getRewardsBalance() external returns (uint256)
```

* **returns**: the balance of rewards or governance tokens that have accrued

### **`transfer`** 

Handles transferring the asset tokens from a [rewards farmer](https://app.gitbook.com/@savedai-admin/s/savedai/~/drafts/-MYdxk4C5bx07OXJ6r41/rewards-farmer) proxy to a recipient's rewards farmer proxy in the event a SaveToken holder wishes to `transfer` their SaveTokens

```javascript
function transfer(address recipient, uint256 amount) external returns (bool)
```

* **parameter**: `recipient`, The address receiving the asset tokens in their [rewards farmer](https://app.gitbook.com/@savedai-admin/s/savedai/~/drafts/-MYdxk4C5bx07OXJ6r41/rewards-farmer) proxy
* **parameter**: `amount`, The number of asset tokens to transfer
* **returns**: true if executed successfully

### **`transferFrom`** 

Handles transferring the asset tokens from a [rewards farmer](https://app.gitbook.com/@savedai-admin/s/savedai/~/drafts/-MYdxk4C5bx07OXJ6r41/rewards-farmer) proxy to a recipient's rewards farmer proxy in the event a SaveToken holder wishes to `transferFrom` their SaveTokens

```javascript
function transferFrom(address sender, address recipient, uint256 amount)
        external returns (bool)
```

* **parameter**: `sender`, The address sending the asset tokens from their [rewards farmer](https://app.gitbook.com/@savedai-admin/s/savedai/~/drafts/-MYdxk4C5bx07OXJ6r41/rewards-farmer) proxy
* **parameter**: `recipient`, The address receiving the asset tokens in their [rewards farmer](https://app.gitbook.com/@savedai-admin/s/savedai/~/drafts/-MYdxk4C5bx07OXJ6r41/rewards-farmer) proxy
* **parameter**: `amount`, The number of asset tokens to transfer
* **returns**: true if executed successfully

