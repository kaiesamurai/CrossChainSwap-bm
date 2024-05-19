# CrossChainSwap: Seamless Crypto Swapping Across Blockchains

## Introduction

CrossChainSwap provides the simplest way to swap cryptocurrencies across different blockchains. Users can effortlessly exchange **ERC-20 tokens** and **ETH** to **ONE (Harmony)** and vice versa.

To ensure fair exchanges, CrossChainSwap leverages **Chainlink Oracles** to retrieve accurate cryptocurrency values during swaps.

CrossChainSwap enables secure, trustless transactions between parties via smart contract escrows, guaranteeing either a successful exchange or a refund.

Future versions will support additional blockchains, including **Cosmos** and **Tomochain**.

## Architecture

The prototype includes safe ERC-20 token locking and unlocking functionality and transfers corresponding representative tokens on the Harmony chain.

### EthBridge Contract

Deployed on an Ethereum network, users can send ERC-20 tokens to this contract to lock them and trigger the transfer process. The EthBridge contract ensures secure implementation of token locking and event emission without risking user funds.

The token amount is converted to USD using Chainlink Oracle prices.

### Chainlink Oracle

Chainlink Oracle is utilized on both Ethereum and Harmony sides to determine the value of ERC-20 and ONE tokens during swaps, ensuring successful transactions.

### The Relayer

The Relayer service interfaces with both blockchains, allowing validators to attest to Ethereum blockchain events. The Relayer listens for **Locked** events from the EthBridge contract, validates them, and forwards transactions to the HmyBridge.

### HmyBridge Contract

The HmyBridge contract processes EthBridge claims and handles the results. Upon receiving and decoding transactions, it calculates the corresponding amount of ONE tokens using Chainlink Oracle data and transfers the ONE tokens to the user.



## Installation

### Testnet Version: Ropsten + Harmony Testnet

#### Deploy EthBridge Contract

Deploy on Ropsten testnet:

1. Configure `.env` with the following variables:

   ```env
   ETH_OPERATOR_ADDRESS=
   ETH_OPERATOR_PRIVATE_KEY=
   ETH_OPERATOR_MNEMONIC=
   INFURA_PROJECT_ID=
   ETH_GAS_LIMIT='6721975'
   ```

2. Deploy the contract:

   ```bash
   cd eth
   yarn migrate
   ```

#### Deploy HmyBridge Contract

Deploy on Harmony testnet:

1. Configure `.env`:

   ```env
   ETH_OPERATOR_ADDRESS='0x8f287eA4DAD62A3A626942d149509D6457c2516C'
   ETH_OPERATOR_PRIVATE_KEY='b03fd86516315e3f12874ddfd4f73a1cefd7fd8f608fec3eaba6f8fbdb2fa85d'
   ETH_OPERATOR_MNEMONIC="access ring phrase vapor smooth clever lens special gym lion junk brass"
   HMY_OPERATOR_ONE_ADDRESS='one12j4ycvnta3l68ep28lpe73n20wx470yfzq9uf3'
   HMY_OPERATOR_ADDRESS='0x54aa4C326BEc7Fa3e42A3Fc39F466A7B8D5f3C89'
   HMY_OPERATOR_PRIVATE_KEY='0x9af8bba5dd5fc34e523b9e6449e1488b8ac0697731afbd646e8b100a1226c9fd'
   HMY_OPERATOR_MNEMONIC='train jump giraffe parent awkward planet limit build pistol tag grunt farm tornado option fame pill kind flat jealous unfair story sausage curious bone'
   TESTNET_0_URL='https://api.s0.b.hmny.io'
   INFURA_PROJECT_ID='469a0721f318401584ab3639fb548d63'
   ETH_GAS_LIMIT='6721975'
   ETH_USER_ADDRESS='0x02610D24fd42f1237c584b6A699727aBAE7cC04e'
   ETH_USER_PRIVATE_KEY='4bbf6348fd657d6dbd5987251f2413d217f7c2601185a6343e87a7c22621d0fe'
   HMY_USER_ADDRESS='0xc162199cDaeAa5a82f00651dd4536F5d2d4277C5'
   ```

#### Run Frontend

1. Navigate to the client directory and install dependencies:

   ```bash
   cd client
   yarn install
   ```

2. Start the frontend:

   ```bash
   yarn start
   ```

## Components

### EthBridge

Locks exchanged tokens and calculates their value using Chainlink Oracle, emitting a Lock token event for the Relayer.

### Relayer

Listens for EthBridge Lock events, validates, and forwards transactions to HmyBridge.

### HmyBridge

Processes Relayer events, calculates the corresponding amount of ONE using Chainlink Oracle, and transfers the ONE tokens.

## Challenges

Combining different blockchains presents operational difficulties, especially for token exchange use cases that require quick price updates. Chainlink Oracle integration on Harmony is straightforward, but incorporating additional blockchains, establishing relays, and liquidity pools remain challenges.

## Accomplishments

The team successfully built a functional demo within a short timeframe. Despite being a small use case in our broader project, the collaborative effort resulted in a complete demo.

## Learnings

The project improved our skills in smart contract development, Chainlink Oracle interaction, and frontend development.

## What's Next for CrossChainSwap

CrossChainSwap is a demo for our broader goal: cross-chain lending. Future versions will include additional blockchains such as Tomochain (native token Tomo) and Cosmos hub (native token Atom). We will also build an interface for liquidity providers to receive farming tokens.

## Built With

- Node.js
- React
- Solidity

## Try it out

Explore CrossChainSwap and experience seamless cross-chain crypto swapping.



## Inspiration

The rise of decentralized finance (DeFi) and the growing ecosystem of various blockchains inspired us to create CrossChainSwap. We wanted to simplify and secure the process of exchanging cryptocurrencies across different blockchains, leveraging the strengths of Chainlink Oracles for accurate price feeds and ensuring seamless transactions.

## What it does

CrossChainSwap allows users to swap cryptocurrencies across different blockchains effortlessly. It supports swapping **ERC-20 tokens** and **ETH** to **ONE (Harmony)** and vice versa. The platform uses smart contract escrows to guarantee secure, trustless exchanges, with the aid of Chainlink Oracles to ensure fair value determination during the swaps.

## How we built it

We built CrossChainSwap with several key components:

- **EthBridge Contract**: Deployed on the Ethereum network, it locks ERC-20 tokens and triggers the transfer process.
- **Chainlink Oracle**: Provides accurate cryptocurrency values on both Ethereum and Harmony blockchains.
- **Relayer**: Interfaces with both blockchains, validating and forwarding events from EthBridge to HmyBridge.
- **HmyBridge Contract**: Receives and processes events from the Relayer, calculating the corresponding amount of ONE tokens and transferring them to the user.

The frontend was built using React, while the smart contracts were developed using Solidity. We deployed the contracts on the Ropsten and Harmony testnets for testing.

## Challenges we ran into

Integrating different blockchains presented several challenges, especially operational complexities and ensuring timely price updates to avoid user losses. Chainlink Oracle integration was straightforward, but we faced difficulties in establishing secure and efficient communication between blockchains and maintaining synchronization.

## Accomplishments that we're proud of

We are proud of successfully building a working prototype of CrossChainSwap within a short timeframe. This project demonstrated our ability to integrate multiple technologies, including smart contracts, Chainlink Oracles, and cross-chain communication. The team's collaborative effort resulted in a functional demo that lays the foundation for future development.

## What we learned

Through this project, we enhanced our skills in:

- Writing and deploying smart contracts
- Integrating Chainlink Oracles
- Building secure and efficient cross-chain communication
- Developing user-friendly frontend interfaces

We also gained a deeper understanding of the complexities and potential of cross-chain DeFi solutions.

## What's next for CrossChainSwap

The prototype of CrossChainSwap is just the beginning. Next steps include:

- Launching on the Polygon mainnet
- Expanding support to additional blockchains such as Tomochain (with native token Tomo) and Cosmos hub (with native token Atom)
- Developing a user interface for liquidity providers to earn farming tokens
- Enhancing the security and efficiency of cross-chain transactions
- Establishing liquidity pools and consensus mechanisms between relayers

Our ultimate goal is to build a comprehensive cross-chain lending platform, providing seamless and secure DeFi services across multiple blockchain ecosystems.