---
layout: post
title: Q&A with ZmnSCPxj
categories: [ZmnSCPxj, bitcoin, privacy]
---

[ZmnSCPxj](https://zmnscpxj.github.io/) is a randomly-generated Internet person who contributes to bitcoin and lightning. I interviewed them over emails and asked a few question about bitcoin, privacy etc.

![image](https://i.imgur.com/pniZLmv.png)


> What are the best practices for good opsec? Any suggestions for new developers interested to contribute to bitcoin?

You need to be ridiculously disciplined; I have not achieved this myself and a number of people already know a mapping of my parent-given name to my self-given name.
For the most part people are fairly respectful about this and will not generally leak this information further.

Try to change the way you write sentences and word things compared to your normal language-use patterns.

Use Tor at the minimum.
Use Tor Browser to access everything; many sites do not work well with Tor Browser but at least github works well.
You may get randomly blocked on github due to use of Tor exit points, but you should be able to request to get unblocked from a real human github auditor.
IRC clients can be configured to use Tor.

Do note that I am pseudonymous, and pseudonymity simply means that you have a different identity that is associated with your Bitcoin-dev-related activity.
One can argue that at this point, my pseudonym is less an anonymity-preserving name and more of a brand, similar to a recognizable corporate brand like "McDonald's" (do *you* know who the actual people are behind that corporate brand? in principle you can know this but most people do not bother; the brand is the identity they care about).

If you want to be truly anonymous, you need to use single-use identities, which are generally difficult to come by: you often need unique email addresses for each identity, email providers increasingly tie email addresses to information that can be tied to specific humans.
An example here is the "Tom Elvis Jedusor" identity that dropped `mimblewimble.txt`; it was only ever used that one time, and the file was hosted on a Tor onion server that has since been offline as well.
This is reasonably easy in IRC where you can take on any identity arbitrarily even over Tor, but would be difficult in other messaging systems.

Places that give Internet access for free are your friend.


> What are positives and negatives of being anon?

Personally I am not particular confident of my ability to actually contribute to the Bitcoin developer ecosystem.
The pseudonym is a way to protect myself, in case I ever screw up badly enough, I can always drop the pseudonym and move on to another one, and gives me enough self-confidence to actually begin contributing in the first place.

The main negative is having to be ridiculously disciplined.
No accidentally signing off with your parent-given name when you are in a context that you should be using your self-given name, and vice versa.
Etc.

Otherwise, in this space, anonymity is generally well-regarded, compared to other areas where an obvious pseudonym is immediately looked at with suspicion.


> How difficult is it for anons to contribute and get funding for their contributions?

In my experience, not difficult at all in the Bitcoin world.

You do have to get down and dirty with the actual code, and you do have to kinda be lucky with whatever project you start contributing.
You really want a project that (a) currently does not have enough contributors and (b) is poised in a space that will boom "soon".
For example, back just before Lightning became cool, you probably would have been very welcome if you started contributing to any of the main Lightning implementations (Core Lightning, LND, Eclair) and at the same time it would suddenly become very important for people who want to fund Bitcoin things to fund Lightning development, which would leave you in a good position where (a) existing contributors strongly welcome you for any help they can get and (b) any contributions you do make will catch the attention of people with the decision-making responsibility of figuring out who to fund.


> Tornado cash developer was arrested for working on a privacy focused project and kicked off GitHub. What should bitcoin developers working on privacy projects learn from this incident?

You need absolute discipline in not getting caught, and you should probably be aware of any particularly boneheaded local laws that might snag you.


> Any comments on Canadian truckers incident, tradeoffs of using privacy tools and relation between censorship & privacy?

None.


> Thoughts on the current state of privacy in bitcoin and lightning? Why is bitcoin used less on darknet markets right now compared to a few years back?

Privacy on Bitcoin is currently fairly bad, most people do not use things like JoinMarket or Wasabi often enough.
This is probably the reason why darknet markets are not using it as much anymore.
There is a strong undercurrent of "legitimacy" among large Bitcoin companies, and many such companies will coordinate to block obviously-dark UTXOs from being used with their products.

In practice, you do not get privacy on Lightning, as most people use unpublished ("private ha ha ha") channels, which leak that you are the ultimate source/destination of payments, and connect to large companies that are incentivized to gather the relevant information and resell it.
HTLCs can be used to track payments, due to consistent hash used, and even if we switch to PTLCs the timing, payment amount, and locktime can still be used to track payments.


> MEV is hot topic right now, do you think better privacy fixes it?

An issue to consider is that miners themselves may use privacy techniques to prevent from being detected as a participant in a contract that may have MEV issues.

We need to specifically design protocols to be resilient to MEV issues when a miner might be participating without knowledge of the other participants. It is probably best to design our contracts to consider that one or all but one participant is secretly a miner and may have the ability to affect the probability of one branch or another being confirmed.

Context: [https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2022-May/020502.html](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2022-May/020502.html)


> What are some of the most promising privacy-focused technologies or projects that you're currently excited about? Not necessarily bitcoin projects

The CoinSwap implementation of `belcher_`.


> Do you think it would be beneficial for Bitcoin implementations (core, knots, btcd, bcoin etc.) to have a dedicated maintainer for privacy-related changes to the P2P, mempool, or wallet level?

Yes.


> Taproot was expected to improve privacy by making nofn multisig look same as single sig in transactions. Its lacking the adoption apart from recent usage for inscriptions, any comments?

I think the big issue here is that there is little incentive to use the singlesig for Taproot.
Consider that for SegWit, it would be cheaper for a singlesig user to switch to SegWit from P2PKH, there is no similar discount for singlesig Taproot users.

On the other hand it does hide all n-of-n together, and more complex contracts (and inscriptions can be argued to be just such a contract) can also be hidden together in the same anonymity set.
Such complex uses are more likely to transition more and more into Taproot use, and novel complex uses will probably want to start out using Taproot as well, so the improved privacy will arrive in time.
Most singlesig users will continue to use SegWit, though, due to the lack of incentive to switch to Taproot.


> How do you think that Bitcoin will evolve over the next decade? Are there any particular areas of development that you think will be especially important?

I think that the base layer will be increasingly ossified, but novel ways to use the existing base layer will arise anyway.
Look at stuff that builds on top of Bitcoin, would be my bet.

### Acknowledgements

Alex Waltz, Max and nothingmuch helped in revieweing questions for the interview.