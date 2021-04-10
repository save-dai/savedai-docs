# Dev Environment

## Web3 version + Solidity compiler version + Truffle  + Node

| Dependency | Version |
| :--- | :--- |
| Solidity | [0.7.6](https://docs.soliditylang.org/en/v0.7.6/) |
| Web3 | [1.2.9](https://web3js.readthedocs.io/en/v1.2.9/web3-eth.html) |
| Truffle | [5.2.4](https://www.trufflesuite.com/truffle) |
| Node | [13.7.0](https://nodejs.org/uk/blog/release/v13.7.0/) |

## Installation

1. Run `git clone` to clone this repo.
2. Run `cd savetoken`.
3. Run `npm install` to install all dependencies.

## Testing and Deployment

* To run a forked mainnet with Ganache, open a tab in your terminal and run:

`ganache-cli -e 1000 -f NODE_URL --unlock "0xc0a47dFe034B400B47bDaD5FecDa2621de6c4d95" --unlock "0x6B175474E89094C44Da98b954EedeAC495271d0F" --unlock "0x98CC3BD6Af1880fcfDa17ac477B2F612980e5e33"`

* In another tab, `cd` into the project and run:

`truffle test --network mainlocal`

