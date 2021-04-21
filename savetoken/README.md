---
description: >-
    The logic (aka implementation) contract that the SaveTokenFactory uses to generate new SaveTokens with new interest-bearing asset and insurance token pairings.
---

# SaveTokens

SaveTokens are tokens that wrap together an interest-bearing asset and a commensurate amount of insurance tokens to create what we call a "self-insured asset".

The SaveTokenFactory contract is a clone factory, which deploys clones of the SaveToken logic (aka implementation) contract.

The SaveToken smart contract provides an interface to the [Adapter](../adapters/README.md) contracts that execute actions on the interest-generating protocol and the insurance protocol used in a given SaveToken flavor. This interface allows for the following core functionality:

## `mint` <a id="90aa"></a>

`mint` is the function called when a saver deposits into a type of SaveToken.

```javascript
function mint(uint256 amount) external returns (uint256)
```

-   **parameter**: `amount`, the number of SaveTokens to mint
-   **returns**: the number of SaveTokens minted
-   **emits**: `Mint`, an event for indexing the number of SaveTokens minted
-   **outcome**: mints SaveTokens, which are owned by `msg.sender`

#### How **`mint`** works

1. Determines the cost of the interest-bearing asset tokens
2. Determines the cost of the insurance tokens
3. Transfers the total amount of the underlying token \(e.g., DAI, USDC, etc\) necessary to mint the `amount` of SaveTokens
4. Obtains the `assetTokens` and the `insuranceTokens` necessary to mint the `amount` of SaveTokens via the corresponding asset adapter \(as registered in the SaveToken contract\).
5. Mints the `amount` of SaveTokens for `msg.sender`
6. Updates balances

{% hint style="warning" %}
The caller of `mint` must first `approve` the SaveToken contract to transfer their underlying token \(e.g., DAI, USDC, etc.\). {% endhint %}

{% hint style="info" %}
The `amount` passed to `mint` may not always equal the final `amount` of SaveTokens minted. This is expected; it's due to very tiny discrepancies in the ways different interest-bearing asset and insurance token protocols round the amounts to mint. The difference is negligible \(tiny fractions of a cent\).
{% endhint %}

## **`withdrawForUnderlyingAsset`** <a id="eea4"></a>

`withdrawForUnderlyingAsset` allows users to unbundle their SaveTokens and receive the underlying asset in return.

```javascript
function withdrawForUnderlying(uint256 amount) external
```

-   **parameter**: `amount`, the number of SaveTokens to unbundle
-   **emits**: `WithdrawForUnderlyingAsset`, an event for indexing the number of SaveTokens unbundled
-   **outcome**: Transfers underlying tokens returned to the `msg.sender`

#### How `withdrawForUnderlyingAsset` works

1. Withdraws the underlying token in exchange for the interest-bearing asset token via the corresponding asset adapter \(as registered in the SaveToken contract\)
2. Exchanges the insurance token via the corresponding insurance adapter \(as registered in the SaveToken contract\) for the underlying token
3. Transfers the underlying token balance to `msg.sender`
4. Updates balances
5. Burns the `amount` of SaveTokens equal to the `amount` of tokens that were unbundled

## **`exerciseInsurance`** <a id="eea4"></a>

`exerciseInsurance` allows users to exercise (aka make a claim on) their insurance, e.g. in case of an adverse financial event or a hack that reduces the value of the interest-bearing asset.

```javascript
function exerciseInsurance(uint256 amount) external
```

-   **parameter**: `amount`, the number of SaveTokens on which to exercise insurance
-   **emits**: `ExerciseInsurance`, an event for indexing the number of SaveTokens in which insurance was exercised
-   **outcome**: Transfers underlying balance returned from insurance protocol to `msg.sender`

#### How `exerciseInsurance` works

1. The SaveToken contract will exercise its insurance tokens or make an insurance claim via the SaveToken's corresponding insurance adapter \(as registered in the SaveToken contract\) on the user's behalf
2. Upon receiving the balance returned from exercising insurance, the SaveToken contract will transfer the balance to `msg.sender`
3. Updates balances
4. Burns the `amount` of SaveTokens equal to the `amount` of insurance tokens that were exercised

## **`withdrawReward`** <a id="eea4"></a>

`withdrawReward` allows users to withdraw all of the rewards tokens they've yielded through the corresponding interest-bearing asset protocol

```javascript
function withdrawReward() external returns (uint256)
```

-   **emits**: `WithdrawReward`, an event for indexing the number of reward tokens withdrawn
-   **returns:** The `amount` of reward tokens withdrawn
-   **outcome**: Transfers all rewards tokens yielded to `msg.sender`

#### How `withdrawReward` works

1. Via the SaveToken's corresponding asset adapter \(as registered in the SaveToken contract\), the SaveToken contract will withdraw all of the rewards tokens they've yielded
2. The asset adapter, using a [Rewards Farmer proxy](../rewards-farmer.md), will claim the rewards tokens and transfer them to `msg.sender`
