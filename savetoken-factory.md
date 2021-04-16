---
description: >-
  The factory contract that is used to generate new SaveTokens by referencing
  the SaveToken implementation contract
---

# SaveToken Factory

The SaveTokenFactory creates new, unique SaveTokens for savers with that will wrap both asset and insurance tokens.

## `createSaveToken` <a id="90aa"></a>

`createSaveToken` is the function called in order to create a new SaveToken

```javascript
function createSaveToken(
    address underlyingToken,    
    address assetAdapter,    
    address assetToken,    
    address insuranceAdapter,    
    address insuranceToken,    
    address exchangeFactory,    
    address farmerAddress,    
    string memory name,    
    string memory symbol,    
    uint8 decimals
) public returns (address)

```

* **parameter:** `underlyingToken` The underlying token address
* **parameter:** `assetAdapter` The address of the Asset adapter a token will use
* **parameter:** `assetToken` The address for the asset token
* **parameter:** `insuranceAdapter` The address of the Insurance adapter a token will use
* **parameter:** `insuranceToken` The address for the insurance token
* **parameter:** `exchangeFactory` The address for the exchange factory
* **parameter:** `farmerAddress` The address for the SaveToken farmer
* **returns**: the address of the newly generated SaveToken contract
* **emits**: `SaveTokenCreated`, an event for indexing the address of the newly created SaveToken
* **outcome:** generates new SaveToken contract with a new asset and insurance token pairing

#### How `createSaveToken` works

1. Accepts all arguments necessary to create a new SaveToken
2. Generates a new SaveToken contract with the attributes provided
3. Pushes the address of the new SaveToken to the `saveTokens` array for future reference

