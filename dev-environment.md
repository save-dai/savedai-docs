# Dev Environment

## Web3 version + Solidity compiler version

| Dependency | Version |
| :--- | :--- |
| Solidity | [0.5.15](https://solidity.readthedocs.io/en/v0.5.15/) |
| Web3 | [1.2.2](https://web3js.readthedocs.io/en/v1.2.2/web3-eth.html) |

## Installation

1. Run `git clone` to clone this repo.
2. Run `cd savedai-contract-v1` .
3. Run `npm install` to install all dependencies.

## Testing and Deployment

* To run a forked mainnet with Ganache, open a tab in your terminal and run:

`ganache-cli -f https://mainnet.infura.io/v3/$INFURA_PROJECTID --unlock "0xc0a47dFe034B400B47bDaD5FecDa2621de6c4d95" --unlock "0x6B175474E89094C44Da98b954EedeAC495271d0F" --unlock "0x98CC3BD6Af1880fcfDa17ac477B2F612980e5e33" --unlock "0x5d3a536E4D6DbD6114cc1Ead35777bAB948E3643" --unlock "0x274d9e726844ab52e351e8f1272e7fc3f58b7e5f" --unlock "0x076c95c6cd2eb823acc6347fdf5b3dd9b83511e4" --unlock "0xcae687969d3a6c4649d114b1c768d5b1deae547b" --unlock "0xd89b6d5228672ec03ab5929d625e373b4f1f25f3"`

* In another tab, `cd` into the project and run:

`truffle test --network mainlocal`

