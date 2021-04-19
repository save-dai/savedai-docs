---
description: >-
  Adapters are used to extend the SaveToken protocol. They make it possible for
  the SaveToken protocol to support any asset or insurance token protocols.
---

# Adapters

All adapters must inherit from and adhere to the **`IAsset`** and **`IInsurance`** interfaces. Each adapter's implementation must be developed to support the corresponding asset or insurance token interface. 

For instance, the `AaveAdapter` has been implemented to enable lending on [Aave's](https://aave.com/) liquidity protocol. In other words, a SaveToken can be created that uses the `AaveAdapter` to interface with Aave's liquidity protocol as means to obtain and `hold` interest-bearing `aTokens`.

Similarly, the `CoverAdapter` has been implemented to provide coverage through [Cover's](https://www.coverprotocol.com/) insurance protocol. In other words, a SaveToken can be created that uses the `CoverAdapter` to interface with Cover's insurance protocol as means to `buyInsurance` \(i.e., `CLAIM` tokens\). 

Adapters make it easy for developers to extend support for the SaveToken protocol. As new asset and insurance token protocols come to market, they can easily be integrated to work with the SaveToken protocol.







  










