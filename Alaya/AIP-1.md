---
AIP: 1
topic: AIP Purpose and Guidelines
status: Active
type: Meta
author: 
created: 2020/02/26
updated: 2020/02/26
---

## What is a AIP?

AIP stands for Alaya Improvement Proposal. An AIP is a design document providing information to the Alaya community, or describing a new feature for Alaya or its processes or environment. The AIP should provide a concise technical specification of the feature and a rationale for the feature. The AIP author is responsible for building consensus within the community and documenting dissenting opinions.

## AIP Rationale

We intend AIPs to be the primary mechanisms for proposing new features, for collecting community technical input on an issue, and for documenting the design decisions that have gone into Alaya. Because the AIPs are maintained as text files in a versioned repository, their revision history is the historical record of the feature proposal.

For Alaya implementers, AIPs are a convenient way to track the progress of their implementation. Ideally each implementation maintainer would list the AIPs that they have implemented. This will give end users a convenient way to know the current status of a given implementation or library.

## AIP Types

There are some types of AIP:

Need to vote on the chain：
- **Parameter**： Proposals for Parameter track must modify governable parameters on the chain. 
- **Upgrade**： Proposals for Upgrade track must initiate a voting upgrade on the chain, a complete installation package needs to be prepared before initiating the proposal.
- **Cancellation**：Proposals of Cancellation track are used to cancel the upgrading and parameter proposals in voting in the chain. We will only initiate this proposal in exceptional circumstances.

Text proposals include the following two types, and in general, no voting is required. Votes can be initiated through text proposals in important or divergent situations.

- **Meta** : Proposals made to the Meta track must affect changes to AIP-1. 
- **Requirement**:  Proposals made to the Meta track must be clear about new functions, optimization functions, etc.

## AIP Work Flow

### AIP Process 

Following is the process that a successful voting AIP will move along:
[ DRAFT ] -> [ FINAL ] -> [ ACCEPTED ] -> [  VOTE ] -> [ PASS ]

Following is the process that a successful non-voting AIP  will move along:
[ DRAFT ] -> [ FINAL ] -> [ ACCEPTED ] 

####  Draft
Once the champion has asked the Alaya community whether an idea has any chance of support, they will write a draft AIP as a [pull request].The title of the draft is: Draft: XXXX. Use a template from the Templates section to ensure you are including all the necessary information. 

:arrow_right: ​Final：At this stage you need to collect their feedback by sharing PR in the Alaya community, and their feedback will help you improve your draft. You can submit changes to the draft through multiple commit until you think the content is perfect, then you can modify the title of the proposal as "Final: XXXX"  and notify AIP Editor through comment.

A request for Final status will be denied if material changes are still expected to be made to the draft. We hope that AIPs only enter Final once, so as to avoid unnecessary noise on the RSS feed.

#### Final

AIP Editor will assign the AIP a number (generally the  PR number related to the AIP) and merge your pull request. The AIP Editor will not unreasonably deny a AIP.

If the AIP Editor deny a AIP., PR will be closed. Reasons for denying draft status include being too unfocused, too broad, duplication of effort, being technically unsound, not providing proper motivation or addressing backwards compatibility, or not in keeping with the Alaya philosophy.

The merged AIP will be reviewed by the Core Devs from a more professional and comprehensive perspective. The audit content includes the evaluation of the feasibility and integrity of the proposal.

- :arrow_right: Accepted: The review will last for two weeks. If the review is passed, AIP Editor will modify the proposal status to "Accepted".

- :arrow_right: Draft: The Core Devs can decide to move this AIP back to the Draft status at their discretion. E.g. a major, but correctable, flaw was found in the AIP.

- :arrow_right: Rejected: The Core Devs can decide to mark this AIP as Rejected at their discretion. E.g. a major, but uncorrectable, flaw was found in the AIP.

#### Accepted 

Any further changes are unlikely and AIP client developers should consider this AIP for inclusion. Once a AIP is accepted, a reference implementation needs to be created.

- :arrow_right: Vote​ ：Parameter proposal, upgrade proposal and cancellation proposal all need to vote on the chain.

#### Vote

Once the parameters, upgrade and cancellation proposals are accepted, voting can be initiated on the chain.

**Note**：Only alternative nodes can initiate on chain proposals. If the AIP author is not an alternative node, it can be initiated by any alternative node instead.

- :arrow_right: Pass: after voting on the chain, AIP editor needs to modify the proposal status to pass.
- :arrow_right: Fail: when the voting on the chain fails, AIP editor needs to modify the proposal status to fail.

Other exceptional statuses include:

- **Active** -- Some AIPs may also have a status of “Active” if they are never meant to be completed. E.g. AIP 1 (this AIP).

- **Abandoned** -- This AIP is no longer pursued by the original authors or it may not be a (technically) preferred option anymore.

    :arrow_right: ​Draft -- Authors or new champions wishing to pursue this AIP can ask for changing it to Draft status.

- **Rejected** -- A AIP that is fundamentally broken or a Core AIP that was rejected by the Core Devs and will not be implemented. A AIP cannot move on from this state.

- **Superseded** -- A AIP which was previously Accpeted but is no longer considered state-of-the-art. Another AIP will be in Accpeted status and reference the Superseded AIP. An AIP cannot move on from this state.

- **Cancelled** --The AIP's status will change to "Cancelled" which means the AIP was cancelled by a passed Cancellation Proposal.

## What belongs in a successful AIP?

Each AIP should have the following parts:

- Preamble - RFC 822 style headers containing metadata about the AIP, including the AIP number, a short descriptive title (limited to a maximum of 44 characters), and the author details. See [below](#aip-header-preamble) for details.
- Abstract - A short (~200 word) description of the technical issue being addressed.
- Motivation (*optional) - The motivation is critical for AIPs that want to change the Alaya protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the AIP solves. AIP submissions without sufficient motivation may be rejected outright.
- Specification - The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Alaya platforms .
- Rationale - The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.
- Backwards Compatibility - All AIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The AIP must explain how the author proposes to deal with these incompatibilities. AIP submissions without a sufficient backwards compatibility treatise may be rejected outright.
- Test Cases - Test cases for an implementation are mandatory for AIPs that are affecting consensus changes. Other AIPs can choose to include links to test cases if applicable.
- Implementations - The implementations must be completed before any AIP is given status “Accepted”, but it need not be completed before the AIP is merged as draft. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of “rough consensus and running code” is still useful when it comes to resolving many discussions of API details.
- Copyright Waiver - All AIPs must be in the public domain. See the bottom of this AIP for an example copyright waiver.

## AIP Formats and Templates

AIPs should be written in [markdown] format.
Image files should be included in a subdirectory of the `assets` folder for that AIP as follows: `assets/aip-N` (where **N** is to be replaced with the AIP number). When linking to an image in the AIP, use relative links such as `../assets/aip-1/image.png`.

Below is a list of AIP templates for each type. Copy the template for the your AIP, fill it out, and submit the pull request with your AIP for review.  Note that all proposals must be licensed CC-0.

- [Cancellation](../templates/Cancellation-template.md)
- [Parameter](../templates/Parameter-template.md)
- [Upgrade](../templates/Upgrade-template.md)
- [Meta](../templates/Meta_template.md)
- [Requirement ](../templates/Requirement_template.md)

## AIP Header Preamble

Each AIP must begin with an [RFC 822](https://www.ietf.org/rfc/rfc822.txt) style header preamble, preceded and followed by three hyphens (`---`). This header is also termed ["front matter" by Jekyll](https://jekyllrb.com/docs/front-matter/). The headers must appear in the following order. Headers marked with "*" are optional and are described below. All other headers are required.

` aip:` *AIP number* (this is determined by the AIP Editor)

` topic:` *AIP topic*

` author:` *a list of the author's or authors' name(s) and/or username(s), or name(s) and email(s). Details are below.*

` * discussions-to:` *a url pointing to the official discussion thread*

` status:` *Draft | Final | Accepted | Vote| Pass | Fail | Active| Abandoned | Rejected | Superseded*

` type:` Parameter| Upgrade| Cancellation | Meta |Reqirement

description: brief summary

` created:` *date created on*

` * updated:` *comma separated list of dates*

` * requires:` *AIP number(s)*

` * replaces:` *AIP number(s)*

` * superseded-by:` *AIP number(s)*

` * Cancelled-by:` *AIP number(s)*

` * resolution:` *a url pointing to the resolution of this AIP*

Headers that permit lists must separate elements with commas.

Headers requiring dates will always do so in the format of ISO 8601 (yyyy-mm-dd).

## AIP Editor Responsibilities

For each new AIP that comes in, an Editor does the following:

- Read the AIP to check if it is ready: sound and complete. The ideas must make technical sense, even if they don't seem likely to get to final status.
- The title should accurately describe the content.
- Check the AIP for language (spelling, grammar, sentence structure, etc.), markup (Github flavored Markdown), code style

If the AIP isn't ready, the Editor will send it back to the author for revision, with specific instructions.

Once the AIP is ready for the repository, the AIP Editor will:

- Assign a AIP number (generally the PR number)
- Merge the corresponding pull request
- Send a message back to the AIP author with the next step.
- Change the AIP status from Final to Accepted, if the AIP is approved by the core developer.

Many AIPs are written and maintained by developers with write access to the Alaya codebase. The AIP editors monitor AIP changes, and correct any structure, grammar, spelling, or markup mistakes we see.

The editors don't pass judgment on AIPs. We merely do the administrative & editorial part.

## History

This document borrows from [Ethereum’s EIP-1](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1.md) written by Martin Becze and Hudson Jameson, which itself was derived from [Bitcoin's BIP-0001](https://github.com/bitcoin/bips/blob/master/bip-0001.mediawiki) written by Amir Taaki, which in turn was derived from [Python's PEP-0001](https://www.python.org/dev/peps/pep-0001/). In many places text was simply copied and modified.  Although the PEP-0001 text was written by Barry Warsaw, Jeremy Hylton, and David Goodger, they are not responsible for its use in the Alaya Improvement Process, and should not be bothered with technical questions specific to Alaya or the AIP. Please direct all comments to the AIP editors.

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
