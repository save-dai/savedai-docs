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

-   **parameter**: `amount`, the number underlying tokens to lend in order to receive and hold corresponding asset tokens
-   **returns**: the number of asset tokens received

{% hint style="info" %}
This function is called `hold` so that it is appropriate both for interest-bearing assets (which are typically acquired by depositing an underlying token such as DAI or USDC in an interest-generating protocol) as well as for non-interest-bearing assets such as WETH or UNI who's value a saver may way to protect with insurance.
{% endhint %}

### **`getCostOfAsset`**

Calculates the amount of underlying tokens needed to receive and hold a certain `amount` of asset tokens

```javascript
function getCostOfAsset(uint256 amount) external returns (uint256)
```

-   **parameter**: `amount`, the number of asset tokens for which the underlying token cost will be calculated
-   **returns**: the number of underlying tokens needed to receive and hold a certain `amount` of asset tokens

{% hint style="info" %}
This function will typically only apply to interest-bearing assets, where the cost is the amount of underlying token \(such as DAI or USDC\) needed to deposit into the interest-generating protocol in order to receive the `amount` of interest-bearing tokens.
{% endhint %}

### **`withdraw`**

Withdraws underlying tokens in exchange for the asset tokens.

```javascript
function withdraw(uint256 amount) external returns (uint256)
```

-   **parameter**: `amount`, the number of asset tokens to redeem in exchange for the underlying tokens
-   **returns**: the amount of underlying tokens withdrawn

### **`withdrawReward`**

Withdraws rewards or governance tokens that have been yielded from the adapter's lending protocol \(e.g., `COMP` tokens yielded from lending to the Compound protocol via the `CompoundAdapter`\).

```javascript
function withdrawReward() external returns (uint256)
```

-   **returns**: the number of rewards or governance tokens withdrawn

### **`getRewardsBalance`**

Returns the balance of rewards or governance tokens that have been yielded from the adapter's lending protocol \(e.g., `COMP` tokens yielded from lending to the Compound protocol via the `CompoundAdapter`\).

```javascript
function getRewardsBalance() external returns (uint256)
```

-   **returns**: the balance of rewards or governance tokens that have accrued

### **`transfer`**

Handles transferring the asset tokens from a [rewards farmer](../rewards-farmer.md) proxy to a recipient's rewards farmer proxy in the event a SaveToken holder wishes to `transfer` their SaveTokens.

```javascript
function transfer(address recipient, uint256 amount) external returns (bool)
```

-   **parameter**: `recipient`, The address receiving the asset tokens in their [rewards farmer](../rewards-farmer.md) proxy
-   **parameter**: `amount`, The number of asset tokens to transfer
-   **returns**: true if executed successfully

### **`transferFrom`**

Handles transferring the asset tokens from a [rewards farmer](../rewards-farmer.md) proxy to a recipient's rewards farmer proxy in the event a SaveToken holder wishes to `transferFrom` their SaveTokens

```javascript
function transferFrom(address sender, address recipient, uint256 amount)
        external returns (bool)
```

-   **parameter**: `sender`, The address sending the asset tokens from their [rewards farmer](../rewards-farmer.md) proxy
-   **parameter**: `recipient`, The address receiving the asset tokens in their [rewards farmer](../rewards-farmer.md) proxy
-   **parameter**: `amount`, The number of asset tokens to transfer
-   **returns**: true if executed successfully
