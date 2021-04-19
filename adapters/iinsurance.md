---
description: >-
  The IInsurance interface makes it easy for developers to build custom support
  for any insurnace token protocol.
---

# IInsurance

All insurance adapters must inherit from and adhere to the **`IInsurance`** interface.

```javascript
interface IInsurance {
    function buyInsurance(uint256 amount) external returns (uint256);
    function sellInsurance(uint256 amount) external returns (uint256);
    function getCostOfInsurance(uint256 amount) external view returns (uint256);
    function isActive() external returns (bool);
}
```

### **`buyInsurance`**

Purchases the insurance tokens with the underlying token \(e.g., DAI\)

```javascript
function buyInsurance(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the amount of underlying tokens used to buy insurance
* **returns**: the amount of insurance tokens received

### **`sellInsurance`**

Sells the insurance tokens in return for the underlying token \(e.g., DAI\)

```javascript
function sellInsurance(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the amount of insurance tokens that will be sold for the underlying token
* **returns**: the amount of underling tokens received following the sale

### **`getCostOfInsurance`**

Calculates the cost of premiums to be paid in order to obtain coverage

```javascript
function getCostOfInsurance(uint256 amount) external view returns (uint256)
```

* **parameter**: `amount`, the amount of insurance tokens for which the cost of premiums is determined
* **returns**: the amount of the underling tokens needed to pay for the `amount` of insurance tokens provided

### **`isActive`**

Checks the expiration status of the insurance token

```javascript
function isActive() external returns (bool)
```

* **returns**: Returns true if insurance token has NOT expired

