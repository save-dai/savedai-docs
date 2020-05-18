---
description: >-
  The driving force behind saveDAI is the belief that we can help more savers
  protect their savings by making deposit insurance dead simple.
---

# FAQ

## Overview

### What is saveDAI?

saveDAI is an insured, high-interest savings account that you control. There is no bank involved, and you can easily add to your savings, withdraw your savings, or move your savings between accounts (i.e., Ethereum wallets).

### How does saveDAI work?

When you deposit into saveDAI, saveDAI does two things with your funds. First, it lends out most of your savings (your principal) to generate interest. This is similar to how a traditional savings account earns interest. 

Second, it uses a small amount of your savings to purchase insurance on your principal. Think of this as a form of deposit insurance, similar to FDIC insurance in the USA.

### How does saveDAI _really_ work?

saveDAI is an ERC20 token on the Ethereum blockchain. It's effectively a wrapper around functionality from several existing smart contract protocols. saveDAI's interest-generating component is cDAI, which it receives after lending most of the original DAI on Compound. The insurance component is ocDAI, which is a protective put option on the Opyn protocol that saveDAI purchases via Uniswap.

### Why does saveDAI exist?

The Decentralized Finance (DeFi) space within the Ethereum ecosystem has produced a number of amazing financial building blocks (some might call them legos), including lending and insurance protocols. Used together, those protocols can create an insured, high-interest savings account. But using them together involves a number of steps. 

We built saveDAI to automate most of those steps in order to...

1. Make it easier for the existing DeFi community -- users and developers alike -- to insure their interest-bearing savings
2. Enable a wholy new set of people to open a protected savings account without a bank

## How can I use saveDAI?

TBD

## Buying saveDAI

### How is saveDAI priced?

TBD

### How do claims work?

TBD

### How is insurance coverage provided?

TBD

### How does interest accrue?

TBD

## Withdrawing saveDAI

### How can I withdraw for the asset and oTokens \(i.e., cDAI and ocDAI\)?

TBD

### How can I withdraw just the asset \(i.e., cDAI\)?

TBD

### How can I withdraw for the underlying asset \(i.e., DAI\)?

TBD

## Exercising Insurance

### Why should I exercise insurance?

TBD

### How can I exercise insurance?

TBD

## Can I build on top of saveDAI?

TBD

## Security

### Is saveDAI safe? Has it been audited?

\[update after audit and include link to audit report\]

### What if there is a bug in the saveDAI contract?

We recognize that this is a risk, and we have taken precautions to protect against this risk with rigorous internal testing and an external audit \[include link to audit report\]. 

Even with this risk, you can still gain significant safety from the oTokens that are used to insure your saveDAI. From [Opyn's documentation](https://opyn.gitbook.io/opyn/faq#what-if-there-is-a-bug-in-opyns-smart-contracts), "\[w\]ith Opyn insurance, you can only lose your Compound deposits in the case that both Opyn and Compound are compromised at the same time. For example, if the probability that Opyn is compromised is 1% and the probability that Compound is compromised is 1%, then with Opyn insurance, your risk of losing your funds drops to 0.01%."

### Does the saveDAI contract have an administrator?

Yes, saveDAI has an extremely small administrative footprint. The owner of the saveDAI contract has the ability to change the name of the saveDAI token. The current name of the saveDAI token is `saveDAI_20210210` . The date portion \(i.e., `20210210` \) represents the expiration date of the current insurance on your saveDAI tokens. In other words, it represents Opyn's current oToken "expiry date".

