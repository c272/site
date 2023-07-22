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

A new API proposal being prototyped within Chromium, and the brainchild of a team comprised solely of Google engineers, has become a topic of heated conversation recently - Web Environment Integrity. This proposal has actually been public on GitHub from [as far back as late April](https://github.com/RupertBenWiser/Web-Environment-Integrity), however has gained the attention (and ire) of much of the larger developer community and users alike due to its highly polarising end goal and far-reaching implications if implemented across web services and devices.

What does Web Environment Integrity seek to achieve? I'll let Google's Ben Wiser ([@RupertBenWiser](https://github.com/RupertBenWiser)), one of the creators of the proposal, explain it for me.

> [WEI seeks to] allow web servers to evaluate the authenticity of the device and honest representation of the software stack and the traffic from the device.<br>
> -- [Ben Wiser, "WEI Explainer"](https://github.com/RupertBenWiser/Web-Environment-Integrity/blob/main/explainer.md)

Essentially, WEI is yet another [trusted computing](https://en.wikipedia.org/wiki/Trusted_Computing) technology. It aims to allow websites to verify the platform and environment of the browser using cryptographically signed "attestations", provided by a limited set of "attesters" which through some mechanism determine the level of trust for the user's platform. We've seen similar concepts to this introduced into many areas of software in recent years, the most notable of which that comes to mind being [Windows 11's hard requirement of a TPM](https://support.microsoft.com/en-us/windows/enable-tpm-2-0-on-your-pc-1fd5a332-360d-4f46-a1e7-ae6b0c90645c), and they are, across the board, incredibly controversial.

And for good reason. Trusted computing inherently seeks to secure the hardware not just **for** the user, but **against** the user. By enforcing the use of a limited, specified set of hardware and software in order to operate, these technologies can entirely remove the freedom of users to freely use their devices by forcing them into a 'Catch 22'; do you use your hardware or operating system of choice and lose access to a piece of potentially critical software, or bite the bullet and throw away your freedoms in order to avoid exclusion? 

This is the question that Google now seeks to extend to the web with WEI. 

## Have Your Cake and Encrypt it Too

Proponents of trusted computing will often argue for the range of security merits which the technology can provide. Secure I/O, integrity measurement and cryptographic services provided at the hardware level by devices such as a TPM (Trusted Platform Module) can be used to create a secure environment in which tampering is made incredibly difficult by sealing off software access to the guts of the security mechanisms and memory being used to facilitate applications on the device.

What these arguments frequently fail to consider, however, are the myriad of secondary effects that the use of such a cryptographic black box brings to the table, and what is (in my opinion) the fundamental misplacement of objectives in the name of providing further security.

Consider the following scenario: there is a well-established player in the music playback software market, developed by a large tech corporation. Let's call it 'Wotify', for this example. With trusted computing being commonplace, conglomerate music publishers such as SME and Warner have begun enforcing **remote attestation** in order to access their digital music library, attempting to prevent piracy and 'bad actors' utilising their works. This relies on the use of an 'attester' that offers integrity measurement, the ability to measure the security and integrity of a program and attest this to third parties (sounds familiar, doesn't it?).

By their very nature, 'attesters' are produced by a very limited group of large manufacturers. Allowing unvetted third parties to produce one would go against the fundamental concepts of trusted computing; they could simply produce a chip which acts in an unauthorised fashion and effectively disables any security guarantees that external third parties (which have no view or knowledge of the underlying hardware) could expect. For this reason, 'attesters' ship with an **endorsement key** or 'EK', which is uniquely generated at manufacture time and signed with keys from a trusted Certificate Authority (CA) much like an SSL certificate, designed to be resistant to hardware-level inspection.

So we've established that 'attesters' can only be created by a small group of manufacturers, but where does 'Wotify' come into this? Well, as the holder of a large market share in the music player space, they have the resources and contacts to have their attester-generated software signature added to the hard-coded allowlist of authenticated program signatures managed by the music publisher.

This read-only list of signatures allows the music publishers to verify that the software running on the user's device is indeed the official build of 'Wotify', and not some cracked version which is primed to record and steal the precious audio data of Warner Chappell, in turn giving the user app access to securely decrypt and use music data which they (in this scenario) provide. Of course, this signature list is strongly controlled by the publishers alone.

Now time for the entry of an up-and-coming competitor: 'Plotify'. Plotify has, for the sake of this example, an objectively far superior feature set to 'Wotify'; not only this, it also runs much faster on low-power devices and is generally more efficient. Among its devoted group of users the software it is incredibly popular, and they are seeking to expand their feature set in order to be able to play protected digital music files from SME and others.

In order to do this, they must now pass through the gatekeepers that are the music publishers and cabal of 'attester' manufacturers. I imagine their conversation would go something like this:

{{< chat-bubble avatar="img/profile/pfp_transparent.png" direction="left" name="Plotify Developers" >}}
Hello, please could we enter our program into your list of permitted client software?
{{< /chat-bubble >}}

{{< chat-bubble avatar="img/profile/pfp_disappointed.png" direction="right" name="SME-UMG-Warner Attested Digital Music" >}}
Why should we bother? We don't know if your software is secure, and you don't seem to have a very large user base, or a large security team. Come back when you're a billion dollar company.
{{< /chat-bubble >}}

{{< chat-bubble avatar="img/profile/pfp_sad.png" direction="left" name="Plotify Developers" >}}
...
{{< /chat-bubble >}}

Even if they somehow managed to convince the publishers to permit their application, all of their users must **also** be using hardware or software which supports one of the attesters supported by the end service to enable this functionality, otherwise an acceptable signature can't be generated in the first place.

At every stage in the pipeline there is a filter, an allowlist which binds the user to a set of choices decided entirely at the whim of the service provider, whomever that may be. We've taken what has traditionally been at the freedom of the user to decide -- their choice of operating system, hardware and software -- and wrestled it away in favour of giving the decision to the service providers.

The question here is fundamentally this:

**Whose responsibility is the security of the user's device? The user, or the service provider?**

In my mind, the answer is clear. Why on earth should a single service provider, such as a music publisher or a bank, decide my operating system, something that determines far more than just what music I listen to, or how I view my checking account? Protecting the user from themselves may be a good default, but it should not be the sole option.

Not only does the service provider lack the scope to be doing this, attestation only reinforces the worst practices that we've seen from modern tech companies in the last 20 years. As in the 'Plotify' example, only pre-existing large players are able to maintain a comprehensive feature set thanks to their influence over allowlists gatekeeping which programs are 'trusted' enough to have the privelege of accessing a certain functionality or service.

This in turn entrenches these existing applications within their markets, pushing out smaller competitors and leaving little to no room for innovation. Even if you've developed an innovative product, if it can't access half the functionality of your main competitor, nobody's going to use it. It also allows existing players to prevent the use of functionality that does not fit their business model or 'vision', as users will have no alternatives to turn to even if they desire the functionality they've been denied.

Of course Google and other behemoths promoting the use of technologies like this will insist that of course, they'll allow any software that meets their set of standards for security and other bells and whistles. However, how well has trusting large tech companies to [not](https://ec.europa.eu/commission/presscorner/detail/en/MEMO_17_1785) [breach](https://www.gov.uk/cma-cases/investigation-into-suspected-anti-competitive-conduct-by-google-in-ad-tech) [anti-competition](https://www.gov.uk/cma-cases/investigation-into-apple-appstore) laws gone over the past 20 years? Not only this, smaller users of these APIs will almost certainly not have the resources or engineer hours to give the time of day to smaller competitor products, and we already see this with OS support.

## A Two-Foot Garden Wall

One of the first major problems with Google's proposal we can see within the first few lines of their stated goals:

> <h3 style="color: var(--text-color-dark)">Goals</h3>
> - Allow web servers to evaluate the authenticity of the device and honest representation of the software stack and the traffic from the device.<br>
> - Offer an adversarially robust and long-term sustainable anti-abuse solution.<br>
> - Don't enable new cross-site user tracking capabilities through attestation.<br>
> - Continue to allow web browsers to browse the Web without attestation.

You may have noticed -- as did [many in the GitHub issues](https://github.com/RupertBenWiser/Web-Environment-Integrity/issues/108) for the project -- that the first two goals here, "Allow web servers to evaluate the authenticity of the device" and "Offer an adversarially robust and ... anti-abuse solution", conflict directly with the fourth: "Continue to allow web browsers to browse the Web without attestation." 

The immediate and most obvious use case for an attestation system like this is for the exclusion of unattested usage. After all, if you're allowing everyone to use your service anyway, what's the point of going through an attestation? All of the example use cases listed in the project explainer talk only about the "detection of" unwanted or illegitimate activity, but all must therefore imply the subsequent **prevention** of it. Nobody's building a burglar alarm just to see how many times their house is broken into.

As [@tbrandirali](https://github.com/tbrandirali) so neatly put it, "*this proposal is building a gate, and expecting it not to be used as a gate.*" Google seems to somewhat realise this issue themselves in their explainer, later on describing a possible mechanism for mitigating this use case, which they title "holdback":

> We are evaluating whether attestation signals must sometimes be held back for a meaningful number of requests over a significant amount of time (in other words, on a small percentage of (client, site) pairs, platforms would simulate clients that do not support this capability).
>
> Such a holdback would encourage web developers to use these signals for aggregate analysis and opportunistic reduction of friction, as opposed to a quasi-allowlist: A holdback would effectively prevent the attestation from being used for gating feature access in real time, because otherwise the website risks users in the holdback population being rejected.

The proposed solution is, quite hilariously, to simply make attestations probabilistic by sabotaging the functionality of the API itself. This destroys the point of the attestation on its own -- if the efficacy of this API is high, service operators will simply accept that they may deny service to a small subset of legitimate users, and take the [path of least resistance](https://en.wikipedia.org/wiki/Principle_of_least_effort) anyway, allowlisting attested clients only. If the efficacy of the API is low, service operators will simply opt not to use it, as it will not provide enough useful data even for "aggregate analytics" purposes, since you are essentially collecting fuzzed data.

There is no "Goldilocks zone" to hit here; the proposal at its core is fundamentally contradictory. The system is either useful and open to abuse by web services, or simply another useless addition to the pile of other user authentication methods. 

But hey, maybe you could skip past a Captcha or two?

## Entrenching the Chrome Throne
One paragraph after describing 'holdout', the proposers seem to completely disregard their prior objections to blocking based on attestation, inviting the possibility of blocking based solely on the browser.

> If the community thinks it's important for the attestation to include the platform identity of the application, and is more concerned about excluding certain browsers than excluding certain OS/attesters, we could standardize the set of signals that browsers will receive from attesters, and have one of those signals be whether the attester recommends the browser for sites to trust (based on a well-defined acceptance criteria).

If it wasn't already clear from my prior mention of anti-competitive practices, this would almost certainly be another step towards further entrenching Chrome's already stranglehold grip on the browser market share.

'Works best on Chrome' has been a concept Google has tried to push fervently for many years, particularly with first party sites like YouTube, which has notoriously had issues working on web engines other than Chromium. Johnathan Nightingale describes Google's seemingly innocent march towards "deprecating" other browsers during his time at Firefox in [this Twitter thread](https://twitter.com/johnath/status/1116871231792455686), which I highly recommend, but I'll place a small excerpt from it here:

> I think they were running out the clock. We lost users during every "oops". And we spent effort and frustration every clock tick on that instead of improving our product. We got outfoxed for a while and by the time we started calling it what it was, a lot of damage had been done.
>
> -- Johnathan Nightingale, Former VP @ Firefox

Google has a storied history of making seemingly innocent decisions in a step toward 'security' or 'performance' which inevitably end up, in some form or another, excluding competitors from the marketplace. The assurances given in this proposal are similarly weak, as they are forced to submit to the reality that attesters will inevitably developed by a small group of large companies.

In an attempt to give a semblance of reassurance to their point, they state that "established players" in the browser market (so, Chrome) would have to "only use attesters that respond quickly and fairly" to browsers requesting to be added to the club, however make no mention of who will be able to enforce this in practice. And of course they don't! Chrome is the sole upstream sitting at the top of the mountain here; they have no overlying authority which can compel them to follow through on their promises. And why should we trust them, given their history?

possible extra points:
  - you also have to convince *all websites* to use these attesters too, since it's up to them whether to trust one or not

## The Leaning Tower of Trust
- talk about anti-extension discussion and google's previous attempt to kill adblock/page modifying extensions with manifest v3
- talk about how useless their commitment to allowing extensions is, as it is again, contradictory to their goals.
  - can't have your cake and eat it
  - vertical trust stack is by definition weak if you literally deliberately open part of it

## Fingerprinting

## Conclusion

### The issues with/within the proposal
- some of their stated goals inherently conflict with eachother (namely first and last)
- almost all of the example use cases are for anti-bot use cases: this doesn't help at all against botnets?
  - "Detect compromised devices where user data would be at risk": If the platforms can do this already (and provide that info in attestation) they can tell the **user**
- this will be abused to hell and back for fingerprinting and blocking users based on platform/browser, and there's no good measure mentioned in the proposal to counter this
  - "holdback" is a hilariously stupid idea which defeats the entire point of the proposal while also keeping all of the negative elements
- the document says newcomers to the market will have to "prove themselves" to attesters, but who will they be?
  - the "keys to the kingdom" are entirely held by a tiny handful of "attesters" -- which will inevitably be controlled by the big players (MS, Apple, Google etc.). this will *easily* become anti-competition.
  - leaves no room for innovation/new entry. good for google, even further enshrines Chrome as the largest market share browser.
- ...
