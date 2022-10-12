---
layout: post
title: Wallet Fingerprinting using nLocktime and nVersion
categories: [bitcoin, fingerprinting, privacy, wallet]
---

## Wallet Fingerprinting, nLocktime and nVersion

### What is nLocktime and nVersion?

**nLocktime**: The last four bytes of transaction data determine when a transaction may be mined. Locktime may be used to ensure that a transaction is locked until a certain block height or point in time. In order for the locktime to be effective, one of the sequence values must be set to anything less than the default maximum (0xffffffff), which is done automatically in most wallets.

![image](https://user-images.githubusercontent.com/94559964/194974178-a8eece0c-2057-4ef6-a4dc-3e64b7aa991a.png)

**nVersion**: First four bytes of transaction to identify data structure. Only two versions exist right now on mainnet that are considered standard: 1 and 2. Version 2 was introduced with [BIP68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki).

![image](https://user-images.githubusercontent.com/94559964/195232841-24964907-1821-4de6-8df2-fcea6018fcfe.png)

I examined nLocktime and nVersion for several open source bitcoin wallets and discovered that most wallet use nVersion 2. nLocktime for Bitcoin Core, Knots, Electrum, Sparrow and Specter is nearest block height. However, nLocktime for Bitcoin Core/Knots is zero if the transaction is created manually using RPC commands like `createpsbt` or `createrawtransaction`. Peter Todd had implemented nLocktime based on anti-fee sniping in [#2340](https://github.com/bitcoin/bitcoin/pull/2340) and [#24128](https://github.com/bitcoin/bitcoin/pull/24128) implements [BIP 326](https://github.com/bitcoin/bips/blob/master/bip-0326.mediawiki) sequence based anti-fee-snipe for taproot inputs.

[0xb10c](https://twitter.com/0xb10c) has written about wallet fingerprinting using fee rate: [https://b10c.me/observations/03-blockchaincom-recommendations/](https://b10c.me/observations/03-blockchaincom-recommendations/) however, nLocktime and nVersion are also crucial. There may be other factors that might help if a fingerprint matches more than one wallet. Andrew Chow has also created a tool to check if a transaction was created using Bitcoin Core or Electrum and explained in this video:

[![wallet-fingerprinting](https://i.imgur.com/dIwF5mv.png)](https://youtu.be/NAtDz2EE9ac)

It's an [open source tool](https://github.com/achow101/wallet-fingerprinting) written in rust.

### Why is wallet fingerprinting important?

Consider the following scenario: Alice is spying on Bob and Carol. She suspects one of them is participating in an activity based on a transaction, but she cannot confirm it. She recognizes that one of the wallets that claims to improve privacy was used for these transactions and examines the nVersion and nLocktime. This makes it simpler to identify Bob, who used Wasabi wallet for the transaction with version 1 and nLocktime 0.

### How to fix it?

If more wallets have the same nVersion and nLocktime, it will be difficult to identify the wallets used for a transaction. nLocktime could be any nearest block height however version needs to be 2 as most of the wallets use it and it is used for transactions that follow all consensus rules.

### Acknowledgements

- 0xb10c
- Andrew Chow
- Greg Walker
- nothingmuch
- RedGrittyBrick
