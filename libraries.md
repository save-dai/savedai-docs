---
description: >-
    We use libraries to handle storage for the different SaveTokens that are
    created. This makes the SaveToken protocol modular in that all adapters can be
    reused to create any type of SaveToken.
---

# Libraries

Given the modular nature of [adapters](./adapters/README.md), each can be reused by any SaveToken that is created. For instance, if we deploy an `AaveAdapter` to be used by the `SaveDAI_Aave_Cover_Expires_1_Sep_2022` that same `AaveAdapter` could be reused by another type of SaveToken \(e.g., `SaveDAI_Aave_Opyn_Expires_1_Dec_2021`\).

This both enables anyone to bootstrap and build resources for a community of SaveToken savers, as well as reduce the costs associated with deploying contracts \(as each adapter need only be deployed once\).

### StorageLib

This library is used to store all of the primary attributes associated with any given SaveToken that is created. These attributes are set and stored as an object in the `SAVETOKEN_STORAGE_POSITION` where they can be referenced by the SaveToken contract.

```text
struct SaveTokenStorage {
    mapping(bytes4 => bool) supportedInterfaces;
    address underlyingToken;
    address assetAdapter;
    address insuranceAdapter;
    address assetToken;
    address insuranceToken;
    address uniswapFactory;
    address saveToken;
    address admin;
    IERC20 underlyingInstance;
    mapping(address => uint256) assetBalances;
    mapping(address => uint256) insuranceBalances;
}
```

The StorageLib also makes available getter functions that can be used by the asset and insurance adapters to retrieve attributes from each SaveToken object.

### RewardsLib

This library is used to support any SaveToken that uses an asset token protocol, via an asset adapter, in which rewards or governance tokens are accrued. These attributes are set and stored as an object in the `SAVETOKEN_REWARDS` where they can be referenced by the SaveToken contract.

```text
struct RewardsStorage {
    mapping (address => address) farmerProxy; // maps user to their farmer proxy
    address logicContract; // farmer logic contract address
}
```

The RewardsLib also makes available setter and getter functions that can be used by the SaveToken contract and asset adapters. For asset token protocols where rewards or governance tokens accrue, the RewardsLib is used to set and retrieve the [rewards farmer](./rewards-farmer) `logicContract` address as well as the `farmerProxy` mapping which maps a saver's address to their corresponding rewards farmer proxy address.

### PausableLib

This library is used in the Pausable contract - which the SaveToken contract inherits from - to `pause`, `unpause`, as well as get the `paused` state of the SaveToken contract. This information is stored, accessed, and updated in `SAVETOKEN_PAUSABLE`.

```text
struct PausableStorage {
    bool paused; // admin address
}
```

### ERC20StorageLib

This library is used in the SaveToken and ERC20 contracts to store ERC20 attributes associated with a SaveToken. This information is stored, accessed, and updated in `SAVETOKEN_ERC20`.

```text
struct ERC20Storage {
    string name;
    string symbol;
    uint8 decimals;
    mapping(address => uint256) balances;
    mapping(address => mapping(address => uint256)) allowances;
    uint256 totalSupply;
}
```

The ERC20StorageLib is used to set and get ERC20 metadata including `name`, `symbol`, and `decimals` as well as `balances`, `allowances`, and `totalSupply`.
