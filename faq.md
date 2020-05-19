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

## Using saveDAI

saveDAI is an insured savings account. You can do anything with saveDAI you can do with a normal savings account, and more:

- open an account / deposit funds (DAI)
- withdraw your funds
- make an insurance claim
- transfer your savings account (to another wallet you control, or to somebody else)
- sell your account

### How do I open a saveDAI account?

All you have to do to open a saveDAI account is make a deposit. That's it! No forms to fill out, no verification required.

### OK, so how do I make a deposit?

If you already have DAI, go to the [saveDAI app](https://app.savedai.xyz), Connect your wallet, enter how much DAI you want to deposit, Unlock DAI, and then click Deposit. In the Unlock step, you give approval for saveDAI to manage the DAI you deposit.

Once the deposit is complete, you'll receive saveDAI tokens in your wallet.

If don't yet have DAI, to use saveDAI today you'll need to get some. See the 'Step 1, get DAI' section from [this article](https://bankless.substack.com/p/how-to-get-a-dai-saving-account) for a couple good options. 

We're working on ways for you to deposit directly into saveDAI without needing to have DAI at all. Follow our [blog](https://blog.savedai.xyz) or on [twitter](https://twitter.com/save_dai to receive the latest updates.

### How does interest accrue?

TBD

### Why do I have so many saveDAI tokens in my wallet?

To minimize both security risks and transaction costs, saveDAI tokens are denominated in the same units as cDAI (tokens representing DAI lent and earning interest via Compound). Because the DAI in Compound is earning interest, cDAI tokens are worth an ever-increasing amount of DAI. Many Ethereum wallets today do the conversion to show you how much DAI your cDAI is worth, but those wallets may not yet do the same for saveDAI tokens. You will always be able to see how much DAI your saveDAI is worth in the [saveDAI app](https://app.savedai.xyz), which denominats saveDAI in terms of DAI.

### How do I withdraw my money from saveDAI?

Once you've deposited into saveDAI, you can withdraw at any time via the Manage section of the [saveDAI app](https://app.savedai.xyz). Click Withdraw, then simply enter the amount of saveDAI you want to withdraw (denominated in DAI) and click Withdraw again.

When you withdraw from saveDAI, you receive both component parts of saveDAI. You'll receive the interest-generating component in the form of cDAI tokens and the insurance component in the form of ocDAI tokens.

In future versions, you'll be able to choose the form of your withdrawal. For example, instead of receiving both cDAI and DAI, you'll be able to ask saveDAI to convert it all into cDAI or even DAI.

### What are insurance claims and why would I make one?

saveDAI's insurance protects your principal from many risks, including adverse financial revents and hacks on the DAI or Compound protocols. If such an adverse event were to cause the dollar-value of your savings, you could use your insurance to claim the original value of your principal (minus a deductible).

Insurance claims are processed automatically by the Opyn protocol. There are no humans involved to reject or delay your claim.

### How do I make an insurance claim?

You can make a claim any time after you deposit and before the insurance expires -- though it probably wouldn't make sense to do so unless an adverse event occured that impacted the dollar-value of your savings. To make a claim, head to the Manage section of the [saveDAI app](https://app.savedai.xyz), click Claim, enter the amount of saveDAI on which to make a claim (denominated in DAI), and then click Claim again.

Once your claim goes through -- which will take only as long as the Ethereum transaction -- you'll receive back ETH with a value equal to your deposit principal (minus a deductible)

### How is insurance coverage provided?

saveDAI sources its insurance from protective put options created and managed by the Opyn protocol. See [Opyn's FAQ](https://opyn.gitbook.io/opyn/faq#buying-insurance) for more information.

### When does the insurance expire?

The current version of insurance expires on February 10, 2021.

### Why is my Amount Insured lower than my deposit?

saveDAI's insurance includes a deductible. Your Amount Insured equals your Principal (the amount lent on Compound) minus the Deductible.

### Why is there a Deductible?

The insurance Deductible is set by the Opyn protocol. Under the hood, insurance from Opyn is a type of financial option called a "protective put", and the strike price for Opyn options is typically set slightly below the current value of the asset they protect (aka slightly "out of the money"). 

See [Opyn's FAQ](https://opyn.gitbook.io/opyn/faq#what-is-max-loss) and [whitepaper](http://convexity.opyn.co/) for more information.

## Can I build on top of saveDAI?

Yes, absolutely! See the rest of our documentation for how to get started.

## Security

### Is saveDAI safe? Has it been audited?

saveDAI is in the process of getting an audit.

### What if there is a bug in the saveDAI contract?

saveDAI is built to be secure. In fact, in an effort to minimize bug and attack surface area, the saveDAI contract does not introduce any net new functionality. Rather, it simply wraps existing functionality provided by existing protocols.

Still, we have taken steps to protect against bugs in the saveDAI contract with rigorous internal test, and we are in the process of getting an external audit.

### Does the saveDAI contract have an administrator?

Yes, saveDAI does have an administrator. The saveDAI adminstrator has limited privileges. It cannot freeze or transfer funds, or change any functional parameters of the contract. 

The owner of the saveDAI contract has the ability to pause deposits into saveDAI. If deposits are paused, no new funds can be added to the saveDAI contract and no new saveDAI tokens can be minted. However, all other saveDAI contract functions -- including withdrawals and insurance claims -- will still be available. 

The primary reason this ability exists is to protect users from unexpected risks. For example, if a vulnerability is discovered in the contract, the owner can prevent new funds from being deposited and placed at risk. Existing funds can be withdrawn by those who hold saveDAI tokens (likely those that originally deposited the funds), and then migrated to the new saveDAI contract once the vulnerability is fixed.

The deposit pause ability can also be used to enact a beta period for the contract where only a limited amount of value is deposited into the contract. Too much value added quickly can create risky conditions.

The contract owner also has the ability to change the name of the saveDAI token. The reason this ability exists is to add clarity and specificity to the name in the case that additional ocDAI option series are released with similar parameters to the current series used by saveDAI.

The current name of the saveDAI token is `saveDAI_20210210`. The date portion \(i.e., `20210210` \) represents the expiration date of the current insurance on your saveDAI tokens, which is the expiry date of the option represented by the ocDAI token.
