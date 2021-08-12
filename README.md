# ERC721 Contract Extensions
A set of composable extensions for the [OpenZeppelin](https://openzeppelin.com/) ERC721 base contracts.

## Available Extensions
### `WithSaleStart.sol`
An extension that enables the contract owner to set and update the date of a public sale.

This builds upon the `Ownable` extension, so only contract deployers can change the sale start via `setSaleStart(uint256 time)`.
Also, to stay true to the trustless spirit of NFTs, it is not possible to change the sale start after the initial sale started.

To use this in your project, call the `afterSaleStart` / `beforeSaleStart` modifiers.

```solidity
contract MyToken is ERC721, WithSaleStart {
  constructor()
    ERC721("MyToken", "MT")
    WithSaleStart(1735686000)
  {}

  function claim () external afterSaleStart returns (uint256) {
    // ...
  }
}
```

### `LimitedTokensPerWallet.sol`
Limits the amount of tokens an external wallet can hold.

### `OnePerWallet.sol`
A more extreme version of `LimitedTokensPerWallet`, which only allows holding one token in an external wallet address.

To use this in your project, call the `onePerWallet` modifier.

```solidity
contract OneForAllToken is ERC721, OnePerWallet {
  constructor()
    ERC721("OneForAllToken", "OFA")
  {}

  function mint () external onePerWallet returns (uint256) {
    // ...
  }

  // Transfer are taken care of by the library.
}
```

### `IncrementingTokenIDs.sol`
A simple token tracker that increments on each new mint.

### `RandomlyAssigned.sol`
(Semi-) Randomly assign token IDs from a fixed collection size on mint.

### `WithContractMetaData.sol`
Link to your collection meta data right from within your smart contract.

### `WithIPFSMetaData.sol`
Handles linking to metadata files hosted on IPFS.

### `WithFees.sol`
Abstracts out the complexity of current fee standards.

## Installation
1. In your project run `npm install @1001-digital/erc721-exensions`
2. Within your project, import the extensions you want to use like `import "@1001-digital/erc721-exensions/contracts/WithIPFSMetaData.sol";`

## Local Development
This project uses the [Hardhat](https://hardhat.org/) development environment. To set it up locally, clone this repository and run `npm install`.

Note: You can exchange `npm run` for `hh` if you have `hh` installed globally on your system.

- Run the test suite: `npm run test`
- Spin up a local development blockchain: `npm run node`
<!-- - Deploy contract with `npm run deploy:localhost` -->

## Thank You
If you have any **improvement suggestions**, **feedback** or **bug reports** please feel free add an issue, or reach out via Twitter [@jwahdatehagh](https://twitter.com/jwahdatehagh) or Email [jalil@1001.digital](jalil@1001.digital).
