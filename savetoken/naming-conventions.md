---
description: The following provides insight into the naming conventions behind SaveTokens
---

# Naming Conventions

### **SaveToken Names**

The SaveToken protocol makes it easy to create a SaveToken that wraps any interest-bearing **asset token** with any **insurance** **token** by depositing any given **underlying token** \(e.g., DAI, USDC, USDT, etc\).

The SaveToken protocol is meant to be as flexible as possible. Naming conventions are meant to highlight the different variations of SaveTokens including their asset and insurance token pairings as well as the insurance coverage expiration dates.

The convention is as follows:

{ **Save**UnderlyingToken }_{_ Asset Token Protocol _}_{ Insurance Token Protocol }\_ { Coverage Expiration Date }

In the example `SaveDAI` SaveToken below:

-   `DAI` is the underlying token deposited to mint SaveDAI
-   Aave is the asset token protocol used to obtain the interest-bearing `aDAI` asset
-   Cover is the insurance token protocol used to obtain `CLAIM` tokens and protect the underlying `aDAI` asset
-   The coverage from the `CLAIM` tokens expires on September 1st, 2022.

| SaveToken                             | Underlying | Interest-Bearing Token | Insurance Token |
| :------------------------------------ | :--------- | :--------------------- | :-------------- |
| SaveDAI_Aave_Cover_Expires_1_Sep_2022 | DAI        | aDAI                   | CLAIM           |

### **SaveToken Symbols**

Similarly, the convention used for SaveToken symbols is as follows:

{ **Save**UnderlyingToken }\_{ Coverage Expiration Date }

In the example `SaveDAI` SaveToken:

| SaveToken                             | Symbol          |
| :------------------------------------ | :-------------- |
| SaveDAI_Aave_Cover_Expires_1_Sep_2022 | SaveDAI_SEP2022 |
