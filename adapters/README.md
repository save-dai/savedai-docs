---
description: >-
  Adapters are used to extend the SaveToken protocol. They make it possible for
  the SaveToken protocol to support any asset or insurance token protocols.
---

# Adapters

### Why Adapters

Adapters are used to extend the SaveToken protocol. They make it possible for the SaveToken protocol to support any asset or insurance token protocols.

### How do Adapters work

All adapters must inherit from and adhere to the **`IAsset`** and **`IInsurance`** interfaces. Each adapter's implementation must be developed to support the corresponding asset or insurance token interface. 

For instance, the `AaveAdapter` has been implemented to enable lending on [Aave's](https://aave.com/) liquidity protocol. In other words, a SaveToken can be created that uses the `AaveAdapter` to interface with Aave's liquidity protocol as means to obtain and `hold` interest-bearing `aTokens`.

Similarly, the `CoverAdapter` has been implemented to provide coverage through [Cover's](https://www.coverprotocol.com/) insurance protocol. In other words, a SaveToken can be created that uses the `CoverAdapter` to interface with Cover's insurance protocol as means to `buyInsurance` \(i.e., `CLAIM` tokens\). 

Adapters make it easy for developers to extend support for the SaveToken protocol. As new asset and insurance token protocols come to market, they can easily be integrated to work with the SaveToken protocol.

### DelegateCall

The SaveToken contract uses [`delegatecall`](https://docs.soliditylang.org/en/v0.8.3/introduction-to-smart-contracts.html?highlight=delegatecall#delegatecall-callcode-and-libraries)  to call functions in the asset and insurance adapters. The code in the adapters is then executed in the context of the calling contract and `msg.sender` and `msg.value` do not change their values

This means that the SaveToken contract can dynamically load code from any asset or insurance adapter address at runtime. Storage, current address and balance still refer to the SaveToken contract, only the code is taken from the adapter addresses. This makes asset and insurance adapters reusable and enables anyone to create s SaveToken that pairs any asset or insurance token they'd like.











  










