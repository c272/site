---
layout: post
title: "Google's Proposal to Close the Gates of an Open Web - WEI"
date: 2023-07-20 10:40:00
tags:
  - Chromium
  - Open Computing
  - FOSS
description: >
  Google's new proposal for verification of 'secure web environments' comes with uncomfortable implications.
coverImage: /img/covers/google-wei.jpg
---

## Overview
A new API proposal being prototyped within Chromium, and the brainchild of a team comprised solely of Google engineers, has become a topic of heated conversation recently - Web Environment Integrity. This proposal has actually been public on GitHub from as far back as late April, however has gained the attention (and ire) of much of the larger developer community and users alike due to its highly polarising end goal and large, far-reaching implications if fully implemented across web-enabled devices.

What does Web Environment Integrity seek to achieve? I'll let Google's Ben Wiser ([@RupertBenWiser](https://github.com/RupertBenWiser)), one of the creators of the proposal, explain it for me.

> [WEI seeks to] allow web servers to evaluate the authenticity of the device and honest representation of the software stack and the traffic from the device.<br>
> -- [Ben Wiser, "WEI Explainer"](https://github.com/RupertBenWiser/Web-Environment-Integrity/blob/main/explainer.md)

Essentially, WEI is yet another [trusted computing](https://en.wikipedia.org/wiki/Trusted_Computing) technology. It aims to allow websites to verify the platform and environment of the browser using cryptographically signed "attestations", provided by a limited set of "attesters" which through some mechanism determine the level of trust for the user's platform. We've seen similar concepts to this introduced into many areas of software in recent years, the most notable of which that comes to mind being [Windows 11's hard requirement of a TPM](https://support.microsoft.com/en-us/windows/enable-tpm-2-0-on-your-pc-1fd5a332-360d-4f46-a1e7-ae6b0c90645c), and they are, across the board, incredibly controversial.

And for good reason. Trusted computing inherently seeks to secure the hardware not just **for** the user, but **against** the user. By enforcing the use of a limited, specified set of hardware and software in order to operate, these technologies can entirely remove the freedom of users to freely use their devices by forcing them into a 'Catch 22'; do you use your hardware or operating system of choice and lose access to a piece of potentially critical software, or bite the bullet and throw away your freedoms in order to avoid exclusion? 

This is the question that Google now seeks to extend to the web, with WEI. 

## Have Your Cake and Encrypt it Too

Proponents of trusted computing will often argue for the range of security merits which the technology can provide. Secure I/O, integrity measurement and cryptographic services provided at the hardware level by devices such as a TPM (Trusted Platform Module) can be used to create a secure environment in which tampering is made incredibly difficult by sealing off software access to the guts of the security mechanisms and memory being used to facilitate applications on the device.

What these arguments frequently fail to consider, however, are the myriad of secondary effects that the use of such a cryptographic black box brings to the table, and what is (in my opinion) the fundamental misplacement of objectives in the name of providing further security.

Consider the following scenario: there is a well-established player in the music playback software market, developed by a large tech corporation. Let's call it 'Wotify', for this example. With trusted computing being commonplace, conglomerate music publishers such as SME and Warner have begun enforcing **remote attestation** in order to access their digital music library, attempting to prevent piracy and 'bad actors' utilising their works. This relies on the use of an 'attester' that offers integrity measurement, the ability to measure the security and integrity of a program and attest this to third parties (sounds familiar, doesn't it?).

By their very nature, 'attesters' are produced by a very limited group of large manufacturers. Allowing unvetted third parties to produce one would go against the fundamental concepts of trusted computing; they could simply produce a chip which acts in an unauthorised fashion and effectively disables any security guarantees that external third parties (which have no view or knowledge of the underlying hardware) could expect. For this reason, 'attesters' ship with an **endorsement key** or 'EK', which is uniquely generated at manufacture time and signed with keys from a trusted Certificate Authority (CA) much like an SSL certificate, designed to be resistant to hardware-level inspection.

So we've established that 'attesters' can only be created by a small group of manufacturers, but where does 'Wotify' come into this? Well, as the holder of a large market share in the music player space, they have the resources and contacts to have their attester-generated software signature added to the hard-coded allowlist of authenticated program signatures managed by the music publisher.

This read-only list of signatures allows the music publishers to verify that the software running on the user's device is indeed the official build of 'Wotify', and not some cracked version which is primed to record and steal the precious audio data of Warner Chappell, in turn giving the user app access to securely decrypt and use music data which they (in this scenario) provide. Of course, this signature list is strongly controlled by the publishers alone.

Now time for the entry of a rag-and-tag competitor: 'Plotify'. Plotify has, for the sake of this example, an objectively far superior feature set to 'Wotify'; not only this, it also runs much faster on low-power devices and is generally more efficient. Within the devoted group of users of the software it is incredibly popular, and they are seeking to expand their feature set in order to be able to play protected digital music files from SME and others. In order to do this, they necessarily have to pass through the gatekeepers that are the music publishers and cabal of 'attester' manufacturers. I imagine their conversation would go something like this:

{{< chat-bubble avatar="img/profile/pfp_transparent.png" direction="left" name="Plotify Developers" >}}
Hello, please could we enter our program into your list of permitted client software?
{{< /chat-bubble >}}

{{< chat-bubble avatar="img/profile/pfp_disappointed.png" direction="right" name="SME-UMG-Warner Attested Digital Music" >}}
Why should we bother? We don't know if your software is secure, and you don't seem to have a very large user base, or a large security team. Come back when you're a billion dollar company.
{{< /chat-bubble >}}

Even if they somehow managed to convince the publishers to permit their application, all of their users will **also** necessarily have to be using hardware or software which supports one of the attesters supported by the end service, otherwise an acceptable signature can't be generated in the first place.

At every stage in the pipeline there is a filter, an allowlist which binds the user to a set of choices decided entirely at the whim of the service provider, whomever that may be. We've taken what has traditionally been at the freedom of the user to decide -- their choice of operating system, hardware and software -- and wrestled it away in favour of letting the service providers decide.

Not only does the service provider really have no scope to be doing this (why on earth should a music publisher decide my operating system, something that determines far more than just what music I listen to), attestation only reinforces the worst practices that we've seen out of modern tech companies in the last 20 years. As in the 'Plotify' example, only pre-existing large players are able to maintain a comprehensive feature set thanks to their influence over allowlists which gatekeep the programs that are 'trusted' enough to have the privelege of accessing a certain functionality or service.

This in turn entrenches these existing applications within their markets, pushing out smaller competitors and leaving little to no room for innovation. Even if you've developed an innovative product, if it can't access half the functionality of the competitor, nobody's going to use it. It also allows existing players to prevent the use of functionality that does not fit their business model or 'vision', as users have no alternatives to turn to even if they desire the functionality they've been denied.

Of course Google and other behemoths promoting the use of attestations like this will insist that of course, they'll allow any software that meets their set of standards for security and other bells and whistles. However, how well has trusting large tech companies to [not](https://ec.europa.eu/commission/presscorner/detail/en/MEMO_17_1785) [breach](https://www.gov.uk/cma-cases/investigation-into-suspected-anti-competitive-conduct-by-google-in-ad-tech) [anti-competition](https://www.gov.uk/cma-cases/investigation-into-apple-appstore) laws gone over the past 20 years? Not only this, smaller users of these APIs will almost certainly not have the resources or engineer hours to give the time of day to smaller competitor products, and we already see this with OS support.

The user can no longer judge a program simply on its merits alone; the service providers will make the decision for you, in advance.

## From Silicon to Browser

- mention google's previous attempt to kill adblock/page modifying extensions with manifest v3

## The issues with/within the proposal
- some of their stated goals inherently conflict with eachother (namely first and last)
- almost all of the example use cases are for anti-bot use cases: this doesn't help at all against botnets?
  - "Detect compromised devices where user data would be at risk": If the platforms can do this already (and provide that info in attestation) they can tell the **user**
- this will be abused to hell and back for fingerprinting and blocking users based on platform/browser, and there's no good measure mentioned in the proposal to counter this
  - "holdback" is a hilariously stupid idea which defeats the entire point of the proposal while also keeping all of the negative elements
- google literally openly mentions blocking based on browser in the document.
- the document says newcomers to the market will have to "prove themselves" to attesters, but who will they be?
  - the "keys to the kingdom" are entirely held by a tiny handful of "attesters" -- which will inevitably be controlled by the big players (MS, Apple, Google etc.). this will *easily* become anti-competition.
  - leaves no room for innovation/new entry. good for google, even further enshrines Chrome as the largest market share browser.
- ...
