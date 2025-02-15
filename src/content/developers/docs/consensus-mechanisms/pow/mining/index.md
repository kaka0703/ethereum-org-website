---
title: Mining
description: An explanation of how mining works in Ethereum and how it helps keep Ethereum secure and decentralized.
lang: en
sidebar: true
preMergeBanner: true
---

<InfoBanner emoji=":wave:">
   Proof-of-stake will soon replace proof-of-work as Ethereum's consensus mechanism, meaning mining will be switched off. Instead, Ethereum will be secured by validators who stake ETH. You can start staking your ETH today. Read more on <a href="/upgrades/merge/">The Merge</a>, <a href="/developers/docs/consensus-mechanisms/pos/">proof-of-stake</a> and <a href="/staking/">staking</a>.    
</InfoBanner>

## Prerequisites {#prerequisites}

To better understand this page, we recommend you first read up on [transactions](/developers/docs/transactions/), [blocks](/developers/docs/blocks/) and [proof-of-work](/developers/docs/consensus-mechanisms/pow/).

## What is Ethereum mining? {#what-is-ethereum-mining}

Mining is the process of creating a block of transactions to be added to the Ethereum blockchain.

The word mining originates in the context of the gold analogy for crypto currencies. Gold or precious metals are scarce, so are digital tokens, and the only way to increase the total volume is through mining. This is appropriate to the extent that in Ethereum too, the only mode of issuance post launch is via mining. Unlike these examples however, mining is also the way to secure the network by creating, verifying, publishing and propagating blocks in the blockchain.

Mining ether = Securing the Network

Ethereum, like Bitcoin, currently uses a [proof-of-work (PoW)](/developers/docs/consensus-mechanisms/pow/) consensus mechanism. Mining is the lifeblood of proof-of-work. Ethereum miners - computers running software - using their time and computation power to process transactions and produce blocks.

## Why do miners exist? {#why-do-miners-exist}

In decentralized systems like Ethereum, we need to ensure that everyone agrees on the order of transactions. Miners help this happen by solving computationally difficult puzzles to produce blocks, securing the network from attacks.

[More on proof-of-work](/developers/docs/consensus-mechanisms/pow/)

## Who can become a miner on Ethereum? {#who-can-become-a-miner}

Technically, anyone can mine on the Ethereum network using their computer. However, not everyone can mine ether (ETH) profitably. In most cases, miners must purchase dedicated computer hardware to mine profitably. While it is true anyone can run the mining software on their computer, it is unlikely that the average computer would earn enough block rewards to cover the associated costs of mining.

### Cost of mining {#cost-of-mining}

- Potential costs of the hardware necessary to build and maintain a mining rig
- Electrical cost of powering the mining rig
- If you are mining in a pool, mining pools typically charge a flat % fee of each block generated by the pool
- Potential cost of equipment to support mining rig (ventilation, energy monitoring, electrical wiring, etc.)

To further explore mining profitability, use a mining calculator, such as the one [Etherscan](https://etherscan.io/ether-mining-calculator) provides.

## How Ethereum transactions are mined {#how-ethereum-transactions-are-mined}

1. A user writes and signs a [transaction](/developers/docs/transactions/) request with the private key of some [account](/developers/docs/accounts/).
2. The user broadcasts the transaction request to the entire Ethereum network from some [node](/developers/docs/nodes-and-clients/).
3. Upon hearing about the new transaction request, each node in the Ethereum network adds the request to their local mempool, a list of all transaction requests they’ve heard about that have not yet been committed to the blockchain in a block.
4. At some point, a mining node aggregates several dozen or hundred transaction requests into a potential [block](/developers/docs/blocks/), in a way that maximizes the [transaction fees](/developers/docs/gas/) they earn while still staying under the block gas limit. The mining node then:
   1. Verifies the validity of each transaction request (i.e. no one is trying to transfer ether out of an account they haven’t produced a signature for, the request is not malformed, etc.), and then executes the code of the request, altering the state of their local copy of the EVM. The miner awards the transaction fee for each such transaction request to their own account.
   2. Begins the process of producing the proof-of-work “certificate of legitimacy” for the potential block, once all transaction requests in the block have been verified and executed on the local EVM copy.
5. Eventually, a miner will finish producing a certificate for a block which includes our specific transaction request. The miner then broadcasts the completed block, which includes the certificate and a checksum of the claimed new EVM state.
6. Other nodes hear about the new block. They verify the certificate, execute all transactions on the block themselves (including the transaction originally broadcasted by our user), and verify that the checksum of their new EVM state after the execution of all transactions matches the checksum of the state claimed by the miner’s block. Only then do these nodes append this block to the tail of their blockchain, and accept the new EVM state as the canonical state.
7. Each node removes all transactions in the new block from their local mempool of unfulfilled transaction requests.
8. New nodes joining the network download all blocks in sequence, including the block containing our transaction of interest. They initialize a local EVM copy (which starts as a blank-state EVM), and then go through the process of executing every transaction in every block on top of their local EVM copy, verifying state checksums at each block along the way.

Every transaction is mined (included in a new block and propagated for the first time) once, but executed and verified by every participant in the process of advancing the canonical EVM state. This highlights one of the central mantras of blockchain: **Don’t trust, verify**.

## A visual demo {#a-visual-demo}

Watch Austin walk you through mining and the proof-of-work blockchain.

<YouTube id="zcX7OJ-L8XQ" />

## The mining algorithm {#mining-algorithm}

The Ethereum mining algorithm has undergone several upgrades since its inception. The original algorithm, "Dagger Hashimoto" was based around the provision of a large, transient, randomly generated dataset which forms a [Directed Acyclic Graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (the Dagger-part), with miners attempting to solve a particular constraint on it, partly determined through a block’s header-hash. This algorithm was novel because it had high memory-access bandwidth requirements but could be run using a modest processor, making it GPU-friendly but resistant to the type of ASIC-driven hardware arms race that could pose a centralization risk (more on [problems with ASICS](https://www.investopedia.com/investing/why-centralized-crypto-mining-growing-problem/)). After substantial upgrades to the algorithm, it was renamed to "Ethash". This renaming happened before mining began on Ethereum mainnet. Dagger-Hashimoto was a precursor, research algorithm that was not used on Ethereum mainnet.

More information on these mining algorithms is available at our [mining algorithms page](/developers/docs/consensus-mechanisms/pow/mining-algorithms/).

## Further reading {#further-reading}

- [What does it mean to mine Ethereum?](https://docs.ethhub.io/using-ethereum/mining/) _EthHub_

## Related tools {#related-tools}

- [Top Ethereum miners](https://etherscan.io/stat/miner?range=7&blocktype=blocks)
- [Etherscan mining calculator](https://etherscan.io/ether-mining-calculator)
- [Minerstat mining calculator](https://minerstat.com/coin/ETH)

## Related topics {#related-topics}

- [Gas](/developers/docs/gas/)
- [EVM](/developers/docs/evm/)
- [Proof-of-work](/developers/docs/consensus-mechanisms/pow/)
