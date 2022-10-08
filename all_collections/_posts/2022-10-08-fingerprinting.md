---
layout: post
title: Wallet Fingerprinting using locktime and version number
date: 2022-10-08 10:30:00
categories: [bitcoin, fingerprinting,privacy,wallet]
---

## Wallet Fingerprinting, Locktime and Version

![image](https://user-images.githubusercontent.com/94559964/194702372-ea77cc5d-8acb-4a89-a3cd-985f5c259112.png)

I checked loctime and version for some open source bitcoin wallets and found that it would be better if all the wallets used version 2 and loctime 0. Below are the wallets that use version 2 and locktime 0 as default values for transactions:

- Bitcoin Core
- Bitcoin Knots
- Blockstream Green
- Bluewallet
- Hexawallet
- FullyNoded
- Nunchuk
- Samourai

[0xb10c](https://twitter.com/0xb10c) has written about wallet fingerprinting using fee rate: https://b10c.me/observations/03-blockchaincom-recommendations/ however locktime and version play an important role as well. There can be various other things which can help to further narrow down in case fingerprint matches multiple wallets.

### Why is wallet fingerprinting important?

Consider an example in which Alice is spying on Bob and Carol. She thinks one of them is involved in an activity based on some transaction but unable to confirm it. She Knows one of the privacy wallet was used for these transactions so looks at the version and locktime. This makes it easier to track Bob who used Wasabi wallet with version 1 and locktime 0.

### How to fix it?

These are not the only wallets used by bitcoin users but I wanted to focus on open source wallets and feel free to add more in this list or correct any information. The goal of this post is to request wallet developers to agree on same default valuesas it would improve privacy.
