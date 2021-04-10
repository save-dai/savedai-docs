---
description: >-
  The logic contract that the SaveTokenFactory uses to generate new SaveTokens
  with new interest-bearing and insurance token pairings.
---

# SaveTokens

SaveTokens are tokens that wrap together an equivalent amount of a interest-bearing and insurance tokens to create what we call a "self-insured asset".

The SaveToken smart contract allows for the following core functionality:

## `mint` <a id="90aa"></a>

`mint` is the function called when a saver deposits into a type of SaveToken.

```javascript
function mint(uint256 amount) external returns (uint256)
```

* **parameter**: `amount`, the number of SaveTokens to mint
* **returns**: the number of SaveTokens minted
* **emits**: `Mint`, an event for indexing the number of SaveTokens minted
* **outcome**: mints SaveTokens, which are owned by `msg.sender`

#### How **`mint`** works

1. Determines the cost of the interest-bearing asset tokens
2. Determines the cost of the insurance tokens
3. Transfers the total amount of the underlying token \(e.g., DAI, USDC, etc\) necessary to mint the `amount` of SaveTokens
4. Obtains the `assetTokens` and the `insuranceTokens` necessary to mint the `amount` of SaveTokens
5. Mints the `amount` of SaveTokens for `msg.sender`
6. Updates balances 

{% hint style="info" %}
The `amount` passed to `mint` may not always equal the final `amount` of SaveTokens minted. This is expected; it's due to very tiny discrepancies in the ways different interest-bearing asset and insurance token protocols round the amounts to mint. The difference is negligible \(tiny fractions of a cent\).
{% endhint %}

## **`withdrawForUnderlyingAsset`** <a id="eea4"></a>

`withdrawForUnderlyingAsset` allows users to unbundle their SaveTokens for their underlying asset

```javascript
function withdrawForUnderlying(uint256 amount) external
```

* **parameter**: `amount`, the number of SaveTokens to unbundle
* **emits**: `WithdrawForUnderlyingAsset`, an event for indexing the number of SaveTokens unbundled
* **outcome**: Transfers underlying tokens returned to the `msg.sender`

#### How `withdrawForUnderlyingAsset` works

1. Withdraws the underlying token in exchange for the interest-bearing asset token from the corresponding asset adapter \(provided when first deployed in the SaveToken's constructor\)
2. Exchanges the insurance token from the corresponding insurance adapter \(provided when first deployed in the SaveToken's constructor\) for the underlying token
3. Transfers the underlying token balance to `msg.sender`
4. Updates balances
5. Burns the `amount` of SaveTokens equal to the `amount` of tokens that were unbundled

## **`exerciseInsurance`** <a id="eea4"></a>

`exerciseInsurance` allows users to exercise their insurance

```javascript
function exerciseInsurance(uint256 amount) external
```

* **parameter**: `amount`, the number of SaveTokens on which to exercise insurance
* **emits**: `ExerciseInsurance`, an event for indexing the number of SaveTokens in which insurance was exercised
* **outcome**: Transfers underlying balance returned from insurance protocol to `msg.sender`

#### How `exerciseInsurance` works

1. Through the SaveToken's corresponding insurance adapter \(provided when first deployed in the SaveToken's constructor\), the SaveToken contract will exercise its insurance tokens on the user's behalf
2.  Upon receiving the balance returned from exercising insurance, the SaveToken contract will transfer the balance to `msg.sender`
3. Updates balances
4. Burns the `amount` of SaveTokens equal to the `amount` of insurance tokens that were exercised

## **`withdrawReward`** <a id="eea4"></a>

`withdrawReward` allows users to withdraw all of the rewards tokens they've yielded through the corresponding interest-bearing asset protocol

```javascript
function withdrawReward() external returns (uint256)
```

* **emits**: `WithdrawReward`, an event for indexing the number of reward tokens withdrawn
* **returns:** The `amount` of reward tokens withdrawn
* **outcome**: Transfers all rewards tokens yielded to `msg.sender`

#### How `withdrawReward` works

1. Through the SaveToken's corresponding asset adapter \(provided when first deployed in the SaveToken's constructor\), the SaveToken contract will withdraw all of the rewards tokens they've yielded
2. The asset adapter, using a Rewards Farmer proxy \(i.e., a contract where asset tokens are held in order to accumulate a protocol's rewards or governance tokens\), will claim the rewards tokens and transfer them to `msg.sender`

