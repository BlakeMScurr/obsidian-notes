      

**Root Oracles and High Trust Bridging**

  

Offchain applications, web interfaces, and bridges all rely on the state of the chain but can’t practically verify it for themselves. Instead of blindly trusting a third party, we can use a root oracle. A root oracle is third party who can be asked the current root of a chain, and loses large sums of money if they lie or make a mistake.

  

**Contract**

  

An oracle can deposit a bond.	

The oracle then attests to the hash of each block offchain by signing messages.

If the oracle ever attested to an incorrect hash, they are slashed, and the slasher recieves a modest reward.

The oracle’s bond vests periodically, so that the bond actually acts as an incentive.

  

**Trustworthiness**

  

Note that a user has to believe that the oracle has a proper bond. To be certain, the user would have to verify the blockchain themselves which almost defeats the purpose of the oracle. However, by verifying the chain to block B (where the oracle created their bond), the user has reasonable certainty that for block >B, any attestation by the oracle is valid. Moreover, it is much easier for the single idea that “oracle.eth has a $10m bond” to become a well known social fact than that “0x1234… is the root of block x” for every block.

  

**Cross Chain Oracles**

  

Suppose X runs an oracle on Ethereum. X cannot risk lying about the state of Ethereum *anywhere* for fear that the state comes back to the Ethereum oracle contract. Suppose X also had a positive incentive to publish Ethereum’s state root on some other chain, say, Gnosis. Now Gnosis contracts can rely on the Ethereum state root assuming X is compotent and follows their incentive. A reverse oracle can be made by the same principle.

  

Note, there may be some trickiness in coordinating blocktimes across chains. I.e., if Ethereum ends up producing blocks faster than expected, the obligation to provide the Ethereum state root on Gnosis at a given time may become impossible resulting in slashing. An alternative is to create a race to publish the state.

  

**Bridging**

  

Now many bridging options are available. For example, you could lock eth on Ethereum which can then be unlocked as weth on Gnosis with a zk proof that it was locked on Ethereum using Ethereum’s state root. It can be unlocked on Ethereum again with the same principle.

  

Secure bridging is a useful service, and the oracles should earn a fee.

  

**Note**

- We could use multiple oracles per bridge to increase certainty.

- Oracles get a cut of the bridge.

  

Also, in the race model, there is an incentive for X to lie. This applies if their collateral is less than the amount they could mint with a false block root. We could just limit the per block amount spent. Or we could have a chellenge period. Such that if another oracle gives a different root none of the minting is accepted. However, that only works if we know that everyone with a bond on the declaration chain also has a bond on the subject chain, or else we have a simple DOS attack. OK interesting, let’s say we have forced entry then!











# Further Idea

      

**A Nice Bridge**

  

**Oath (lower)**

  

All attestors have a locked bond.

The attestors is slashed if they *ever* lie about the block hash.

  

**Temple (lower)**

  

Become an initiate by joining a queue

You must have taken the Oath

You must have never joined before

Each priestess accepts you in turn

Atfer some time, you may join

Any preiestess who didn’t accept you is kicked out

Anyone who breaks their oath can be immediately kicked out

Anyone who votes to kick a true prisetess from the sanctum is kicked

  

**Sanctum (higher)**

  

Join the sanctum using the vote to join the priesthood

Be kicked from the sanctum with a 50% vote

  

**Oracle (higher)**

  

The first in the sanctum to give the oracle is rewarded.

Any contested oracle is considered invalid.

  

**Bridge**

  

Lock x eth with a hash h (e)

Mint x weth (g)

Use E->G oracle to get state root

Verify ZKP proving (x, h) in state, and you know h preimage

Check h not used yet

Set h to used

Mint weth

Burn x weth with a hash h (g)

Unlock x eth (e)

Use E->G oracle to get state root

Verify ZKP proving (x, h) in state, and you know h preimage

Check h not used yet

Set h to used