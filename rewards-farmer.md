# Rewards Farmer

## Overview

### What is Rewards Farmer?

Increasingly, DeFi protocols are incentivizing valuable in-protocol activities (e.g. providing liquidity) by distributing rewards tokens (also known as governance tokens) to users engaging in those activities. Receiving these tokens adds to the yield users receive from the protocol, which is great for the users. 

However, users accessing a rewards-giving protocol indirectly via a wrapper token contract &mdash; a contract that creates a token that wraps the underlying protocol's token &mdash; may not be able to access the rewards tokens they are owed. This is because the wrapper token contract is engaging in the rewardable activities on behalf of its users, and therefore the wrapper token contract is the recipient of the rewards tokens. Further, because the distribution rate of the rewards token can vary, it is difficult for the wrapper token contract to correctly allocate the rewards tokens it receives to its users.

Rewards Farmer resolves this issue.

### How does Rewards Farmer work?

Rewards Farmer creates a distinct instance &mdash; a proxy contract &mdash; of the rewards-receiving component of the wrapper tplem for each user. As each user's proxy contract receives that user's rewards directly, there is never any confusion about how much rewards are owed to each user.

When a user transfers some or all of their wrapper token balance to another address, a new proxy is created for the new address to hold the underyling protocol token and receive its associated rewards.

## Details and Implementation

### TBD
