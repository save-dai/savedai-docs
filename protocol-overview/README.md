# Protocol Overview

SaveDAI is an ERC20 token that wraps together an equivalent amount of cDAI and ocDAI to create what we call a "self-insured asset".

The saveDAI smart contract does three main things:

1. Mint saveDAI
2. Exercise the insurance portion of saveDAI
3. Withdraw saveDAI

## `mint` <a id="90aa"></a>

`mint` is the function called when a saver deposits into saveDAI.

```javascript
function mint(uint256 _amount) external returns (uint256)
```

* **parameter**: `_amount`, the number of saveDAI tokens to mint
* **returns**: the number of saveDAI tokens minted
* **emits**: `Mint`, an event reporting the number of saveDAI tokens minted
* **outcome**: mints saveDAI tokens, which are owned by `msg.sender`

#### How `mint` works

1. Calculates the amount `assetCost` of DAI required to obtain`assetAmount ≈ _amount` of cDAI and transfers it from `msg.sender` to the saveDAI contract
2. Obtains an amount `assetAmount` of cDAI by depositing `assetCost` into Compound
3. Calculates the amount `oTokenCost`of DAI required to purchase `oTokenAmount = assetAmount` ocDAI on uniswap and transfers it from `msg.sender` to the saveDAI contract
4. Purchases `oTokenAmount` ocDAI from uniswap via a `tokenToTokenSwapInput` for `oTokenCost` amount of DAI.
5. Mints `amount = TokenAmount = assetAmount` saveDAI tokens

Despite the fact that a saveDAI token representing a saver’s claim on cDAI and ocDAI — the saveDAI contract does not have any mappings outside of the standard ERC20 mappings. We can do this because of the unit equivalence of cDAI and ocDAI; since a single ocDAI token acts as insurance for a single cDAI token, savers will always need an equivalent amount of cDAI and ocDAI. It therefore makes most sense for `1 saveDAI` token to represent `1 cDAI` and `1 ocDAI`.

{% hint style="info" %}
The `_amount` passed to `mint` may not always equal the final `amount` of saveDAI tokens minted. This is expected; it's due to the way the Compound cDAI contract rounds the amount of cDAI to mint in return for the deposited DAI. The difference is negligible \(a tiny fraction of a cent\), but it does force the saveDAI contract to handle it by first calculating `assetAmount` and then using that value to find the `oTokenCost` for the same amount of `ocDAI`.
{% endhint %}

## **`exerciseInsurance`** <a id="eea4"></a>

`exerciseInsurance` is the function you call when your cDAI’s value has fallen below the insured amount — whether because of a hack on DAI, a Compound governance failure, or something else. \(It’s called “exercise” because ocDAI is technically a put option; in the Opyn protocol, making an insurance claim amounts to exercising that option.\)

```javascript
function exerciseInsurance(uint256 _amount, address payable[] memory vaultsToExerciseFrom) public
```

* **parameter**: `_amount`, the number of saveDAI tokens for which to exercise insurance
* **parameter**: `vaultsToExerciseFrom`, the ocDAI vault\(s\) from which to extract the ETH payout
* **emits**: `ExerciseInsurance`, an event reporting the `_amount` of saveDAI insurance exercised, the amount of `EthReturned`, and the address of the user who is exercising their insurance
* **outcome**: `_amount` saveDAI tokens are burned, `_amount` of both cDAI and ocDAI are transferred to the Opyn protocol, and an ETH insurance payout of is transferred to `msg.sender`

#### How `exerciseInsurance` works

1. Checks if the ocDAI has expired—remember, the current series of ocDAI is an option that expires on February 10, 2021. If it’s expired, the function reverts.
2. Records the saveDAI contract’s ETH balance, `balanceBefore`
3. [`exercise`](https://opyn.gitbook.io/opyn/otoken#exercise) the `_amount` ocDAI options within the Opyn protocol, asking for ETH from `vaultsToExerciseFrom`. This Opyn protocol function also transfers `_amount` ocDAI and cDAI to the Opyn contract to initiative the claim for ETH.
4. Records the saveDAI contract’s ETH balance and subtracts `balanceBefore` to find the amount of ETH received as insurance payout, `EthReturned`. Steps 2 and 4 and needed  because the Opyn `exercise` function doesn’t return the amount of ETH transferred.
5. Transfers `EthReturned` to `msg.sender`
6. Burns `_amount` of `msg.sender`'s saveDAI tokens

## Withdraw

Users may want to withdraw their saveDAI deposit for a number of reasons, including:

* using their DAI deposit for something other than growing their savings
* selling the insurance component of saveDAI \(e.g. if the ocDAI market price is attractive\)
* wanting to manage the interest-bearing and insurance components of saveDAI separately
* etc.

saveDAI allows users to withdraw their deposit in three ways.

### `withdrawForAssetandOTokens`

`withdrawForAssetandOTokens` transfers both the cDAI and ocDAI to the user.

```javascript
function withdrawForAssetandOTokens(uint256 _amount) public
```

* **parameter**: `_amount` of saveDAI tokens to unbundle and withdraw
* **emits**: `WithdrawForAssetandOTokens`, an event reporting the `_amount` of saveDAI tokens unbundled and the address that unbundled them
* **outcome**: `_amount` of saveDAI tokens are burned and the components — cDAI and ocDAI — are transferred to `msg.sender`

#### How `withdrawForAssetandOTokens` works

The first step is to check if the ocDAI has expired, which determines exactly what `withdrawForAssetandOTokens` will do.

**If ocDAI has expired…**

1. Transfers `_amount` of cDAI to `msg.sender`
2. Burns `_amount` of `msg.sender`'s saveDAI tokens

{% hint style="info" %}
Note: since each version of saveDAI only uses a single series of ocDAI, once that series expires there’s no reason to clean up expired ocDAI tokens by burning them.
{% endhint %}

**If ocDAI has not yet expired…**

1. Transfers`_amount` of ocDAI to `msg.sender`
2. Transfers `_amount` of cDAI to `msg.sender`
3. Burns `_amount` of `msg.sender`'s saveDAI tokens

### `withdrawForAsset`

`withdrawForAsset` __returns the full value of the user's saveDAI in terms of cDAI. To do so, it converts the ocDAI to cDAI.

```javascript
function withdrawForAsset(uint256 _amount) public
```

* **parameter**: `_amount` of saveDAI tokens to unbundle
* **emits**: `WithdrawForAsset`, an event reporting the `_amount` of saveDAI tokens unbundled and the saver that unbundled them
* **outcome**: the saveDAI tokens are burned and cDAI is transferred to `msg.sender`

#### How `withdrawForAsset` works

1. Requires that ocDAI has not yet expired
2. Swaps `_amount` of ocDAI for DAI on uniswap
3. Deposits that DAI into Compound, receiving more cDAI
4. Transfers the sum of the original amount of cDAI and the newly minted cDAI to `msg.sender`
5. Burns `_amount` of `msg.sender`'s saveDAI tokens

### `withdrawForUnderlyingAsset`

With `withdrawForUnderlyingAsset`, the user will receive back DAI.

```javascript
function withdrawForUnderlyingAsset(uint256 _amount) public
```

* **parameter**: `_amount` of saveDAI tokens to unbundle
* **emits**: `WithdrawForUnderlyingAsset`, an event reporting the `_amount` of saveDAI tokens unbundled and the saver that unbundled them
* **outcome**: the saveDAI tokens are burned and DAI is transferred to `msg.sender`

#### How `withdrawForUnderlyingAsset` works

1. Requires that ocDAI has not yet expired
2. Redeems`_amount` of DAI for cDAI on Compound
3. Swaps `_amount` of ocDAI for DAI on uniswap
4. Transfers the total sum of DAI to `msg.sender`
5. Burns `_amount` of `msg.sender`'s saveDAI tokens

