---
layout: post
title: Nostr Privacy
categories: [nostr, privacy]
---

I have observed a few privacy issues with [nostr protocol](https://github.com/nostr-protocol/nostr) and apps related to privacy. This post is not an attempt to FUD although this could help in more users being aware of the problems and possible solutions.

## IP leak using profile image

It is possible for an attacker to save a malicious link as profile image and most of the nostr clients leak IP address for the users if they view the profile image in an event or elsewhere.

Steps to reproduce the issue:

1. Create a [canary](https://canarytokens.org/generate) token by selecting 'custom image bug'

   ![canary](https://i.ibb.co/BspfGDG/image.png)

2. Open [https://astral.ninja/](https://astral.ninja/) and save the URL you get from step 1 as profile image

3. Post something and wait for canary token email notifications.

4. You would see notifications like this:
   
   ![notification](https://i.ibb.co/y8Gq15y/image.png)

## Metadata leak in encrypted DM

Attackers can spy using public keys to see who is sending DMs to whom and the time. Although they wont know the content of messages.

Wiz had even [tweeted]((https://i.ibb.co/hfXDFZx/image.png)) about it and there are some NIPs, suggestions etc. to fix metadata leak for improving privacy in DMs.

NIP 21 (fiatjaf): [https://github.com/nostr-protocol/nips/pull/20](https://github.com/nostr-protocol/nips/pull/20)

NIP 24 (Jeff): [https://github.com/nostr-protocol/nips/pull/56](https://github.com/nostr-protocol/nips/pull/56)

Private DMs (phyro):  [https://gist.github.com/phyro/73a5db45dfaa29e96e5b4b0beb503957](https://gist.github.com/phyro/73a5db45dfaa29e96e5b4b0beb503957)

## Contact lists

Contact lists are defined in [NIP-02](https://github.com/Minds/nostr-nips/blob/master/02.md) and public information. There are no ways to create private contacts lists right now in the protocol however some workarounds like saving them as encrypted DM.

## Relays

Relays know a lot about clients so [joinstr](https://github.com/1440000bytes/joinstr) uses below things:

1. New keys for posting every event
2. Random subscription id for getting events
3. Websocket connection is closed after each task
4. A new tor circuit is created for each request

You could also run your own relay for some use cases although its always good to use multiple relays. Use clients that care about privacy and VPN/proxy. If you are running a relay, being anon could be helpful if government agencies have issues with some events being published in the future when nostr gets too big.

## Encrpted Channels

[NIP-28](https://github.com/nostr-protocol/nips/blob/master/28.md) defines public channels but there is no way to create encryped channels in the protocol right now. Vishal is working on a [NIP](https://github.com/nostr-protocol/nips/pull/59), implemented in [nostr-console](https://github.com/vishalxl/nostr_console) however it is still being reviewed and tested.

### Acknowledgements

- fiatjaf
- Jeff 
- phyro
- Vishal


