# Smart Contracts 

Magic is an open-source and distributed project, built on top of smart contracts running on the popular [Ethereum](https://www.ethereum.org/) 
Virtual Machine (EMV).  Smart contracts provide a transparent "ledger" and accounting system, and more importantly gives 
the ability to define & distribute incentives for proper use of the network in a purely mathematical and distributed way.

Incentivized behaviors:
1. Quality Internet Service:  Providers should be providing consistent and fast service to those using their network.  
In order to keep this a distributed system, Magic defines a Proof of Availability (POA) concept which seeks to formally prove and define 
the availability and quality of a provider in which all parties of the system can agree upon.  More on this in 
the forthcoming whitepaper. Current implementation is speculative and subject to change as tokenomics are defined.

1. Use as a utility:  Magic coins are technically a "utility token" which should be used for buying & selling internet
connection by a consumer or any internet connected device.

The contracts that define the rules to this system are open-sourced.  The following contracts are defined:

[Magic Protocol on Github](https://github.com/magic-network/magic-protocol)

High-level contracts:
1. [MagicCoin](https://github.com/magic-network/magic-protocol/blob/master/contracts/token/MagicToken.sol): [View on Rinkeby](https://rinkeby.etherscan.io/token/0xc3cbfd0d0f583987ea43d92f7bc2624052ffd6f5)
1. Minter
1. Staker
1. Rounds
1. MagicCoin

In order to interface with these contracts on Ethereum's online IDE [Remix](https://remix.ethereum.org), you can import the 
remix formatted contracts [here](https://github.com/magic-network/magic-protocol/tree/master/remix).
