# CoreHAM: Hybrid AssetHub for the Masses for Usability-first Polkadot 2.0 Experimentation

| | |
| --------------- | -------------------------------------------------------------------------------------------------- |
| **Start Date**  | 1 January 2024  |
| **Description** | A design sketch for CoreHAM, a community-run parachain identical to AssetHub on Polkadot (or Kusama) but with<br/>(1) $HAM as the Native Token of CoreHAM, where HAM is distributed 1:1 to DOT Token Holders from genesis<br/>(2) NO existential deposit, to make CoreHAM maximally usable at the expense of storage bloat<br/> (3) A Hybrid 1.0/2.0 Smart Contract Design: Initially ink!+EVM smart contract support, but then extending to Polkadot 2.0 technologies: CorePlay, CoreJam, Sugondat Hyper-Data Availbility<br/> (4) Extrinsic/Transaction Fees paid in HAM and DOT (or KSM) <br/>A sync-first usability-first strategy is pursued, with a commitment to onboarding millions of users and thousands of developers in Polkadot 2.0 era, making CoreHAM ripe for Usability-first Polkadot 2.0 experimentation.  |
| **Authors**     | [Sourabh Niyogi](https://github.com/sourabhniyogi)  |

## Summary

We introduce CoreHAM, a community-developed hybrid parachain with a $HAM native token, 0 DOT existential deposit.  The genesis block issues HAM to all DOT Token holders, aiming for 1:1 DOT:HAM distribution as of some TBD era, considered maximally fair and ungamable.   CoreHAM will pursue a hybrid EVM+Coreplay smart contract design rather than 1.0 "App-chain" model.  HAM is utility coin owned by all DOT Token Holders.

## Motivation

*Polkadot is committed to a Minimal Relay Chain future, with scalability prioritized over usability*.  RFC #32 established Polkadot's dedication to async-first computing patterns. In this approach, the relay chain is specifically designated for the composability of async-sync using a "map-reduce" computing pattern, ensuring optimal scalability.  However, this architecture forces developers into complex async programming models (eg XCM) with users perceiving the result as being too complex.  This makes Polkadot difficult to onboard new developers who value usability over scalability.

*EVM Contracts are unlikely to thrive on AssetHub*.   Undeniably, the shadow of EVM sync looms large.  While top parachains Astar and Moonbeam adopted EVM, the culture of Polkadot finds the sync-first paradigm of EVM intrinsically suffocating to the fundamental necessity of using async compute patterns to scale.   The most popular application of Ethereum -- building your own cryptocurrency with ERC20s -- does not exist in any system chain, even though composability of ERC20s (including USDC, USDT) is done in EVMs second most popular application: Uniswap.   An AssetHub minters' expectation of being able to deploy familiar synchronous EVM contracts on AssetHub and trading (e.g. Uniswap V2, V3, Curve, etc.) will be immediately met with the requirement of managing asynchronous XCM transfers, keyless accounts that require significant developer + user education ... just to do what can be done on Ethereum with great ease already.  The resistance to having EVM Contracts in AssetHub is [palpable](https://forum.polkadot.network/t/permissioned-pallet-contracts-deployment-to-asset-hub-for-defi-primitives/3908/2), fundamentally because Polkadot 2.0 aims to solve async+sync composability and does not wish to compromise this in AssetHub.

*AssetHub (and other system chains) are not governed by OpenGov*.  While AssetHub user might hope that [RFC #45 - Lowering Deposit Requirements on Polkadot and Kusama Asset Hub](https://github.com/polkadot-fellows/RFCs/pull/45) and [RFC#62  - Lowering Existential Deposit on Asset Hub for Polkadot](https://github.com/polkadot-fellows/RFCs/blob/c76cfc459f5a5291fdb62bb727decd11feba7d95/text/0062-lowering-existential-deposit-on-assethub.md) to pass, Polkadot / Kusama system chains are fundamentally under control of the Polkadot Fellows.  RFCs have NO predictable timeline for being accepted or rejected, unlike OpenGov referendums, which take at most 28 days.   We conclude that AssetHub (and perhaps other system chains, dedicated to doing one thing well) are intended for _serious_ use cases only, and ignoring the need for every developers to support avoiding synchronous EVM contracts in the name of _asynchronous scalability_.   If Coreplay + CoreJam + Blobs system chains were to be developed (to be clear, this is unknown), then they too would be under the same centralized control of Polkadot Fellows.

**Hybrid Vision.**  We _severely_ love the uncompromising idealism of Polkadot Fellows, but believe there is a more pragmatic hybrid design that sacrifices some of this idealism in favor of pragmatism.  Similar to the way hybrid cars provide the world to fight climate change on the way to a fully electric future given a gas-powered past, we believe hybrid chains enable a path for the world to get to scalability given an EVM/sync-first past.  We believe that having a parachain with many of the beloved 1.0 functionality in Polkadot's top parachains (EVM) can coexist alongside soon to be loved 2.0 functionality being developed right now.  To the fullest extent that this 2.0 functionality is deployable in parachain, our hybrid vision drives us to deploy this in a new parachain fully supported by OpenGov and owned by DOT Token Holders.

We thus develop CoreHAM, initially for an asset-minting focussed community that prioritizes *usability*  over security and scalability of AssetHub, contrasted here:

| Parachain | CoreHAM - Hybrid 1.0+2.0 | AssetHub - No Smart Contracts |
|----|-----|----|
| Approach  | Sync-first, usability-first | Async-first, scalability-first |  
| Design Priorities  | Serious about scaling to 100K-1MM developers and 100MM+ users with 1.0 and 2.0 tech and state bloat | Serious about scaling uncompromising async+sync composability, without state bloat |  
| Hybrid?    | Yes - EVM + ink! + Coreplay + CoreJam + SugonDAT            | No / Unknown |
| Funded by   | Community / DOT Token holders via OpenGov | Polkadot Treasury |
| Controlled by  | DOT Token Holders | Polkadot Fellows |
| Existential Deposit | 0 DOT, 0 HAM | 0.1 DOT (or 0.004 DOT with RFC #62 or .01 DOT with Runtime) |
| Sufficient Assets | DOT + HAM   | DOT, USDC, USDT |
| Cost to mint $HAM | 0 | 12.5K DOT [$100K] (or 5K DOT [$40K] with RFC #62) |
| Cost to mint New Asset for all DOT Token Holders | < 3K DOT | < 3K DOT |
| Sync Trading methods | Asset Conversion Pallet, EVM Contracts, ink! Contracts, CorePlay contracts locally | Asset conversion Pallet only |
| Async Trading methods | Other DEXes | Other DEXes |
| Cost to run    | TBD via CoreTime              | 0 (Treasury Supported) |

We develop the CoreHAM Design in what follows.

## Stakeholders

- **DOT Token Holders**: Those who hold DOT on the Polkadot Relay Chain or any Polkadot system chain or parachain  
- **HAM Token Holders**: Those who hold HAM on CoreHAM

## CoreHAM Design

Note: These following are starting suggestions and are extremely likely to be revised by experienced parachain engineers.

### Native Token / Decimals

* HAM is the native token with 10 as decimals (same as DOT)

### Fees / Sufficient Assets

* DOT and HAM will be acceptable fees.

### Pallets

The pallets of CoreHAM are the same as AssetHub, including `assetconversion`, but also with the key pallets needed to support Smart Contracts:
1. `ethereum` and `evm`, similar to Astar + Moonbeam.
2. `contracts`, similar to Astar
3. `coreplay`, as soon as practical
4. `corejam`, if possible
5. `sugondat`, if possible

The combination of the above will  "fun" experimentation with Polkadot 2.0 technology in a *sync* environment.

### Existential Deposit

The Existential Deposit is 0 to support usability.  The implementation is trivial, changing [this](https://github.com/polkadot-fellows/runtimes/blob/30e0dbfdcb78722ed61325c0ebf1efdcdb6033ba/system-parachains/asset-hubs/asset-hub-polkadot/src/constants.rs#L21) to
```
pub const EXISTENTIAL_DEPOSIT: Balance = constants::currency::EXISTENTIAL_DEPOSIT / 10000000000;
```

### Genesis

The genesis block will issue HAM 1:1 to all DOT Token Holders at the conclusion of a specific era TBD on the Polkadot Relay Chain.   We are not aware of any technical reason why a genesis block could not have 1.25MM holders at this time, but this is subject to investigation and empirical testing.

This snapshot is expected to include:
* stakers on the Relay chain, _including in nomination pools_
* CEXes in aggregate (where each CEX must distribute to DOT holders as of a specific time)
* DOT holders in each parachain, if archive RPC nodes are available for each parachain
* DOT holders in aggregate, if archive RPC nodes are NOT available

Should archive nodes for some parachains be unavailable, a simple strategy may be to:
* send the parachain's unallocated amount to the Treasury
* at some later time, relay this unallocated amount to DOT holders in the parachain
This would have probably over 99.x% coverage then 100.0000% fair distribution.

Aside: edge cases may arise concerning DOT XCM Transfers in flight at the boundaries of an era between two chains.  The probability of this happening can be empirically determined with further

### Hybrid Substrate+EVM Chain Design

A precise technical specification to support both Substrate + EVM Addresses is highly desirable.  Fortunately, Moonbeam and Astar and many others have developed Substrate+EVM Chains with different SS58/ECDSA key schemes in the Polkadot ecosystem already over the last 2 years and new.   We believe a good design should have minimal education for existing Ethereum/EVM chain users as well as minimal education for existing Polkadot users, but the precise choice may require careful consideration of tradeoffs.

We believe a default choice is to use Astar's design choice, but more recent designs from HydraDX may be preferred after careful consideration.

### Trading

Being able to trade HAM and DOT on AssetHub and CoreHAM is a primary concern to prospective HAM holders and actual DOT Token holders (which, in a 1:1 Fair distribution, is _identical_).  As is common in the Polkadot ecosystem,  CoreHAM will open HRMP channels with other parachains, including AssetHub.  Dapp developers (eg a dedswap.xyz site) can develop XCM transfers functionality between CoreHAM and other chains, including the Polkadot Relay Chain.  Several paths are considered below.

#### Trading CoreHAM-Issued Assets on CoreHAM

End users can trade CoreHAM-issued assets using the `assetConversion` pallet except with the 0.3% fees lowered to 0.15% or 0.05% for the following pools:
* DOT/HAM -- available immediately
* DOT/USDC -- which will require an HRMP Channel with AssetHub
* DOT/USDT -- which will require an HRMP Channel with AssetHub

For EVM Smart Contracts, it is likely that community-provided Uniswap v2/v3 + Curve implementations will compete with the above, e.g. for USDC/USDT pairs, with different fee mechanics.  Stellaswap on Moonbeam, Arthswap on Astar are 2 familiar examples.  Following either Astar or Moonbeam's design, CoreHAM should have xcDOT, xcHAM system contracts to map into DOT and HAM to enable EVM Smart Contracts to thrive.  


#### Trading AssetHub-Issued+Foreign Assets  on CoreHAM

An HRMP Channel with AssetHub will be critical to support CoreHAM USDC + USDT, the top 2 stablecoins.    These should have xcUSDC, xcUSDT system contracts to map into USDC and USDT to enable EVM Smart Contracts to reference these assets as ERC20 assets.  

## Implementation

Given CoreHAM's hybrid chain design, 0 ED, we believe Tanssi can be an excellent infrastructure operator, who makes it easy to deploy a testnet version of CoreHAM.

(courtesy of Cedric of Ajuna)

1. Get Tokens, for https://apps.tanssi.network/  to support long-lasting chains (> 48h)

2. Fork this
 https://github.com/moondance-labs/tanssi/commit/47c8e8adef67be7936f3e23211489bac6ef5d15a
and copy-paste Assethub's spec, build a runtime upgrade

3. Add in the needed FRAME pallets to this [container-chains/templates/simple/runtime/src/lib.rs](https://github.com/paritytech/polkadot-sdk/blob/4f832ea865e48625c8035ec08b8fb98e9f0e5519/cumulus/parachains/runtimes/assets/asset-hub-rococo/src/lib.rs)

4. Whenever and wherever possible, add in new functionality from Polkadot 2.0.

However, there are many design considerations in having a Hybrid chains, extending to Polkadot 2.0.

Natural candidates for CoreHAM engineering execution would be those who have deployed Hybrid chains and are intimately familiar with the new Coreplay+CoreJam+Sugondat technology stack.

## Testing, Security, and Privacy

As is common in Polkadot parachain development, it will be natural to use Rococo + Kusama Relay Chains as test network and a canary network to deploy the following 3 parachains:
* CoreHAM for Rococo: (where ROC and RAM substitute for DOT and HAM)
	* Obtain maximally fair DOT distribution genesis configurations, measured in terms of total issuance being fully modeled across the entire Polkadot ecosystem
	* Successful demonstration of Substrate Addresses paying extrinsic fees with ROC  or RAM to transfer amounts below AssetHub ED
	* Successful demonstration of EVM Addresses paying transaction fees with xcROC or xcRAM  
	* Successful demonstration of Substrate Address adding/removing liquidity using assetconversion pallet and trading  ROC/RAM pair
	* Successful demonstration of EVM Addresses a v2 xcROC/xcRED   
  * demonstration of ink! Uniswap v2 Contracts
* CoreHAM for Kusama (where KSM and KAM substitute for DOT and HAM)
	* same as above, but with _purchased_ CoreTime
* CoreHAM for Polkadot
    * same as above, but with _purchased_ CoreTime

At of the end of 2023, CoreTime just been launched on Rococo and we believe CoreTime will be able to follow on Kusama by the end of Q1.  Thus we believe CoreHAM for Rococo can be deployed at the end of Q1 and CoreHAM for Kusama can be deployed in Q2 (using CoreTime on Kusama) and CoreHAM for Polkadot can be launched in Q3, following CoreTime launch on Polkadot.

## Performance, Ergonomics, and Compatibility

### Performance

The reduction of ED to 0 is extremely likely to require one of the [Possible Solutions for Unsustainable Storage Growth](https://forum.moonbeam.network/t/possible-solutions-for-unsustainable-storage-growth/845) used by Moonbeam, which also has an ED of 0.  If the chosen solution [MBIP-4: Storage Base Fee](https://forum.moonbeam.network/t/possible-solutions-for-unsustainable-storage-growth/845#mbip-4-storage-base-fee-14) is reasonable, it may be highly valuable to establish this at genesis.

### Ergonomics

CoreHAM aims to address ergonomics for two groups:
1. _Developers_ can build on the old paradigm EVM Contract and new 2.0 Polkadot paradigm with sync patterns on a single CoreHAM chain.

2. _Users_ can use everyday applications with a non-zero ED on a CoreHAM chain.

CoreHAM does what Polkadot Fellows cannot:  offer developers+users something that  _cannot_ scale but is _usable_

Then, when there actually is a _need_ to scale, CoreHAM developers can move their application _within Polkadot_ to a place where they can.  


### Compatibility

CoreHAM aims to be as compatible with EVM as Moonbeam+Astar and other Hybrid Chains, but also future proof in being able to handle Polkadot CorePlay and if possible, Sugondat and


## Costs / Benefits

*Costs to DOT Tokenholders*.   We believe at most 100K DOT in OpenGov support per year would required to build and maintain the CoreHAM chain
* a small team (3-4) of Substrate engineers maintaining CoreHAM
* securing CoreTime within Kusama and then Polkadot for CoreHAM

*Benefits to DOT Tokenholders*.  We believe CoreHAM can be a strong candidate for being a top 3 chain parachain in 2024-2025 with its Hybrid 1.0/2.0 chain design.  It is competitively differentiated from AssetHub, and can be supported by an OpenGov community that recognizes that a successfully marketed and growing CoreHAM chain (in bringing new users, new DOT revenue, new CoreTime) is highly valuable to the Polkadot ecosystem.

## Future Directions for CoreHAM

While CoreHAM can be seen as a less serious relative of AssetHub, CoreHAM is  serious about Polkadot 2.0 _experimentation_  and committed to bringing millions of users to Polkadot and thousands of builders to Polkadot 2.0 technology:  

* [CorePlay](https://github.com/polkadot-fellows/RFCs/tree/gav-coreplay)
* [CoreJam](https://github.com/polkadot-fellows/RFCs/tree/gav-corejam)
* [Sugondat/Blobs](https://github.com/thrumdev/blobs/tree/main/sugondat-chain)

We believe CoreHAM can become a hotbed for experimentation, not just for asset minting and trading but many of Polkadot 2.0 innovations that are _also_ highly experimental in nature.  The narrative is clear:

**COREHAM ENABLES POLKADOT 2.0 EXPERIMENTATION**

While it is critical for Polkadot to be _serious_ in its pursuit of the ubiquitous scalable map-reduce computer, we believe CoreHAM can rapidly evolve to be a place for people to experiment with both old ideas from Ethereum and these breakthrough new ideas from Polkadot 2.0 in a single hybrid chain: **CoreHAM**.    

This can be done without excess conservativeness (e.g. premature fear of state bloat, forcing async patterns unnecessarily) and having a sense of urgency.  This can be supported by OpenGov-based marketing supporting a grassroots community effort fully aligned with the DOT Tokenholders.

## Competition

CoreHAM can be seen as Moonbeam+Astar rebooted in a 2.0 era, fully owned by DOT Token holders.

**1.0 Competition.**  CoreHAM must compete with AssetHub as well all other 1.0-centric "appchains" (Astar, Moonbeam, hydradx, polkadex, etc. see [Defillama]( https://defillama.com/chains/Polkadot))  but more honestly, with a much larger of Ethereum/EVM chains which dwarf the entire Polkadot ecosystem.   It is possible that USDT  and USDC, issued on AssetHub, would be quite attractive for sync trading within AssetHub.  However, AssetHub on Polkadot is virtually unused, it is believed, due to lack of marketing, and a strong commitment to async composability and security-first considerations.  By comparison, Astar and Moonbeam engage in consistent marketing and lead Polkadot defi activity, probably in no small part due to their being Hybrid chains.  However, they are not _community-owned_ parachains supportable by the DOT Token holder via OpenGov.  At present, OpenGov-funded marketing is a minority viewpoint, but we believe this viewpoint can change with DOT Token holders being direct owners in CoreHAM's success.  

**2.0 Competition.**. We are not aware of any chain incorporating DOT 2.0 technology of  Coreplay, CoreJam, Sugondat/DA while making asset minting/trading easy in a single chain, and certainly not with the DOT Token holder's interest aligned as perfectly as developed in CoreHAM.  

## Unresolved Questions

1. What is the best way circa 2024 to implement a Hybrid Chain to maximize usability?  Specifically with Tanssi?  Is there a better way to do it?
2. Can OpenGov actually overcome its anti-marketing bias and grow Polkadot with new Polkadot 2.0 technology?   Is CoreHAM's "single chain" design a good way to do it?
3. Are there any technical reasons why we cannot have 1.25MM entries in the genesis block of CoreHAM?
