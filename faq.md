---
description: >-
    The driving force behind SaveToken is the belief that we can help more savers
    protect their savings by making deposit insurance dead simple.
---

# FAQ

## Overview

### What is SaveToken?

SaveTokens provide you with the flexibility to create your own insured, high-interest savings account that you control. There is no bank involved, and you can easily add to your savings, withdraw your savings, or move your savings between accounts \(i.e., Ethereum wallets\).

### How do SaveTokens work?

When you deposit into a SaveToken contract, the protocol does two things with your funds. First, it lends out most of your savings \(your principal\) to generate interest. This is similar to how a traditional savings account earns interest.

Alternatively, if you are using a SaveToken for a non-interest-bearing asset \(such as WETH or MKR\), the SaveToken contract will hold onto most of what you deposit.

Second, it uses a small amount of your savings to purchase insurance on your principal. Think of this as a form of deposit insurance, similar to FDIC insurance in the USA.

### How does saveDAI _really_ work?

The SaveToken protocol makes it easy to wrap any interest-bearing token with any corresponding insurance token. This enables savers to generate yield while at the same time protecting their underlying assets.

For instance, a user may wish to use [Aave's](https://aave.com/) lending and borrowing protocol to generate yield via aTokens while at the same time insuring those aTokens via a corresponding insurance protocol like [Cover](https://www.coverprotocol.com/).

To do this, the user would choose to mint SaveTokens with an ERC-20 stablecoin like DAI. The SaveToken protocol will then wrap the DAI with aDAI from Aave and CLAIM tokens from Cover, thus generating an insured, interest-bearing savings account.

### Why does the SaveToken protocol exist?

The Decentralized Finance \(DeFi\) space within the Ethereum ecosystem has produced a number of amazing financial building blocks or money legos, including lending and insurance protocols. Used together, those protocols can create an insured, high-interest savings account. But using them together involves a number of steps.

We built the SaveToken protocol to give users the autonomy to pair any interest-bearing token with any corresponding insurance token and to automate the process for them in order to...

1. Make it easier for the existing DeFi community -- users and developers alike -- to insure their interest-bearing savings
2. Enable a whole new set of people to open a protected savings account without a bank

## Using SaveTokens

Your SaveTokens are an insured savings account. You can do anything with your SaveTokens you can do with a normal savings account, and more:

-   open an account / deposit funds \(e.g., DAI, USDC, etc\)
-   withdraw your funds
-   make an insurance claim
-   transfer your savings account \(to another wallet you control, or to somebody else\)
-   sell your account

### How do I open a savings account with the SaveToken protocol?

All you have to do to open a savings account is make a deposit. That's it! No forms to fill out, no verification required.

### OK, so how do I make a deposit?

If you already have stablecoins like DAI or USDC, connect your wallet, enter how much you want to deposit, and choose the type of SaveToken you'd like to mint \(e.g., SaveToken that wraps aDAI with CLAIM tokens, SaveToken that wraps cUSDC with ocDAI tokens, etc\). Once the deposit is complete, you'll receive SaveTokens in your wallet.

### How do I withdraw my money from saveDAI?

Once you've deposited into the SaveToken protocol, you can withdraw at any time. Click Withdraw, then simply enter the amount of SaveTokens you want to withdraw and click Withdraw again.

When you withdraw from the SaveToken protocol, you receive both component parts of your SaveTokens. You'll receive the interest-generating tokens \(e.g., aDAI, cDAI, cUSDC, etc\) and the corresponding insurance \(e.g., COVER tokens\).

### What are insurance claims and why would I make one?

The SaveToken protocol's insurance protects your principal from many risks, including adverse financial events and security incidents. If such an adverse event were to cause the dollar-value of your savings, you could use your insurance to claim the original value of your principal \(minus a deductible\).

Insurance claims are processed automatically by the insurance token's protocol that is wrapped in your SaveTokens.

### How do I make an insurance claim?

You can make a claim any time after you deposit and before the insurance expires -- though it probably wouldn't make sense to do so unless an adverse event occurred that impacted the dollar-value of your savings. To make a claim, click Claim, enter the amount of SaveTokens on which to make a claim -- denominated in the underlying token deposited \(e.g., DAI\) -- then click Claim again.

### How is insurance coverage provided?

SaveTokens are insured by the corresponding insurance token that makes up a particular type of SaveToken. For instance, you could have SaveTokens that are wrapping aDAI and CLAIM tokens from the Cover protocol. In this case, the coverage is provided by the Cover protocol. However, another flavor of SaveToken could have a different insurance provider \(e.g., Opyn\).

### When does the insurance expire?

It depends on the underlying insurance protocol that is used for a given SaveToken. This information is provided via the SaveToken interface.

## Can I build on top of the SaveToken protocol?

Yes, absolutely! We encourage the community to build adapters for other interest-bearing and insurance token protocols. The SaveToken protocol currently has adapters in place that support the following protocols:

-   [Compound](https://compound.finance/) \(interest-bearing\)
-   [Aave v2](https://docs.aave.com/developers/) \(interest-bearing\)
-   [COVER](https://docs.coverprotocol.com/) \(insurance\)
-   [Opyn v1](https://opyn.gitbook.io/opynv1/) \(insurance\)

## Security

### Is the SaveToken protocol safe? Has it been audited?

_**UPDATE and link to audit report following Quantstamp audit**_

### What if there is a bug in the SaveToken protocol ?

The SaveToken protocol is built to be secure. In fact, in an effort to minimize bug and attack surface area, the SaveToken contract does not introduce any net new functionality. Rather, it simply wraps existing functionality provided by existing protocols.

Still, we have taken steps to protect against bugs in the SaveToken contracts with rigorous internal testing and an external security audit.

### Does the SaveToken protocol have an administrator?

Yes, the SaveToken protocol does have an administrator. The SaveToken admin has limited privileges. It cannot freeze or transfer funds, or change any functional parameters of the contract.

The owner of the SaveToken protocol has the ability to pause deposits. If deposits are paused, no new funds can be added to the SaveToken contract and no new SaveToken can be minted. However, all other SaveToken contract functions -- including withdrawals and insurance claims -- will still be available.

The primary reason this ability exists is to protect users from unexpected risks. For example, if a vulnerability is discovered in the SaveToken contract, the owner can prevent new funds from being deposited and placed at risk. Existing funds can be withdrawn by those who hold SaveTokens \(likely those that originally deposited the funds\), and then migrated to the new SaveToken contract once the vulnerability is fixed.

The deposit pause ability can also be used to enact a beta period for the contract where only a limited amount of value is deposited into the contract. Too much value added quickly can create risky conditions.

Over time, as the SaveToken contracts are battle-tested and the SaveToken developers and community grow ever more confident in their security, we hope to burn the administrator keys.
