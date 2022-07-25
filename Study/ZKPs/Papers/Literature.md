#flashcards/zkps/Literature

# Classial ZKPs

## GMR89

What is GMR89's title?
?
The Knowledge Complexity of Interactive Proof-Systems.
<!--SR:2022-10-22,128,250-->

Who are the authors of GMR89?
?
Shafi Goldwasser, Silvio Micali, and Charles Rackoff
<!--SR:2022-08-31,80,210-->

What does GMR89 contribute?
?
The notion of interactive proofs, communcation complexity, and that interactive proofs reduce communication complexity.
<!--SR:2022-08-13,76,210-->

## GMW91

What is GMW91's title?
?
Proofs that Yield Nothing but their Validity or All Languages in NP Have Zero-Knowledge Proof Systems
<!--SR:2022-08-13,38,130-->

Who are the authors of GMW91
?
Oded Goldreich, Silvio Micali, and Avi Widgerson
<!--SR:2022-09-15,80,190-->

What does GMW91 contribute?
?
If one way functions exist, then every NP language has a computationally zero-knowledge proof system.
<!--SR:2022-07-27,22,150-->

## BGKW88

What is BGKW88's title?
?
Multi-Prover Interactive Proofs: How to Remove Intractability Assumptions
<!--SR:2022-08-10,56,170-->

Who are the authors of BGKW88?
?
Michael Ben-Or, Shafi Goldwasser, Joe Killian, and Avi Widgerson
<!--SR:2022-09-03,60,170-->

What does BGKW88 contribute?
?
The notion of multi-prover interactive protocols, that all languages in NP have MIPs, and that 2 provers always suffice.
<!--SR:2022-08-23,34,130-->

What did BGKW88 see themselves as contributing?
?
An interactive proof system that doesn't rely on the one way function assumption, instead relying on physical separation.
<!--SR:2022-09-02,39,150-->

## FRS88

What is FRS88's title?
?
On the power of multi-prover interactive protocols
<!--SR:2022-08-21,78,210-->

Who are the authors of FRS88?
?
Lance Fortnow, John Rompel, and Michael Sipser.
<!--SR:2022-11-05,109,190-->

What does FRS88 contribute?
?
That interaction with two provers is equivalent to interaction with one prover plus oracle access to a proof string. $MIP[poly(n), poly(n)] \subseteq NEXP$.
<!--SR:2022-08-12,31,150-->

## BFL90

What is BFL90's title?
?
Non-deterministic exponential time has two prover interactive protocols.
<!--SR:2022-09-18,62,170-->

Who are the authors of BFL90?
?
Lázsló Babai, Lance Fortnow, and Carsten Lund
<!--SR:2022-09-11,76,190-->

What does BFL90 show?
?
NEXP has 1 round 2 prover interactive protocols. Thus $MIP[2, 1] = NEXP$
<!--SR:2022-10-09,80,170-->



# Early NIZKs

Who are the authors of GO94?
?
Oded Goldreich and Yair Oren
<!--SR:2022-08-28,34,190-->

What is the title of GO94?
?
Definitions and properties of zero-knowledge proof systems
<!--SR:2022-08-10,44,170-->

What does GO94 show, according to Groth's talk in the 3rd BIU winter school?
?
That NIZKs are only possible in the plain model for trivial languages, where $L \in BPP$
<!--SR:2022-09-23,88,250-->

What does GO94 show?
?
Classifies and defines two new definitions of zero knowledge: auxiliary input, and simultation, and shows that blackbox-simulation -> auxiliary -> GMR definition, and that composition of auxiliary gives auxiliary.
That 1 round NIZKs are only possible for trival (BPP) languages.
<!--SR:2022-09-22,62,190-->


# Pairing Based Snarks

Who are the authors of GOS12?
?
Jens Groth, Rafail Ostrovsky, and Amit Sahai
<!--SR:2022-11-06,117,250-->

What is the title of GOS12?
?
New techniques for noninteractive zero-knowledge
<!--SR:2022-08-01,17,150-->

What did GOS12 contribute?
?
- Introduced pairing based NIZKs. 
 - Reduced CRS size. 
 - First perfect NIZK for all NP. 
 - First universally composable NIZK argument for all NP in the presence of an adaptive adversary. 
 - First non-interactive zap for all NP based on a standard cryptographic security assumption.
<!--SR:2022-08-04,38,190-->

Who are the authors of GOS06?
?
Jens Groth, Rafail Ostrovsky, and Amit Sahai
<!--SR:2022-08-30,73,250-->

What is the title of GOS06?
?
Non-interactive zaps and new techniques for NIZK
<!--SR:2022-09-10,51,170-->

What did GOS06 contribute?
?
Gives non interactive Zaps for all NP (where they had only existed for some non trivial but not NP complete language before).
<!--SR:2022-07-31,19,130-->

Who are the authors of Gro06?
?
Jens Groth
<!--SR:2022-08-14,63,250-->

What is the title of Gro06?
?
Simulation-sound NIZK proofs for a practical language and constant size group signatures
<!--SR:2022-08-19,27,150-->

What did Gro06 contribute?
?
Applications of pairing NIZKs to particular problems (without expensive circuit reductions). First group signature scheme satisfying the strong security definition of Bellare, Shi, and Zhang, without random oracles, with constant group elements per signature.
<!--SR:2022-09-30,80,210-->

Who are the authors of GS12?
?
Jens Groth, Amit Sahai
<!--SR:2022-09-14,84,250-->

What is the title of GS12?
?
Efficient noninteractive proof systems for bilinear groups
<!--SR:2022-07-29,17,130-->

What did GS12 contribute?
?
Practical efficient NIZK and NI witness indistinguishable proofs by satisfying equations over bilinear groups rather than reducing to circuit satisfiability.
<!--SR:2022-08-07,33,150-->

??? why do we use reductions to circuits today, i.e., circom? Especially since it uses groth16!

Who are the authors of Gro10?
?
Jens Groth
<!--SR:2022-11-24,133,250-->

What is the title of Gro10?
?
Short pairing-based non-interactive zero-knowledge arguments
<!--SR:2022-07-31,17,190-->

What did Gro10 contribute?
?
Constant sized proofs without Fiat-Shamir heuristic or random oracles. Introduces the q-computational power Diffie-Hellman and q-power knowledge of exponent assumptions.
<!--SR:2022-10-06,80,250-->

Who are the authors of Gro09?
?
Jens Groth
<!--SR:2022-09-03,75,250-->

What is the title of Gro09?
?
Linear algebra with sub-linear zero-knowledge arguments
<!--SR:2022-07-30,17,130-->

What did Gro09 contribute?
?
Given commitments to matrices, gives a sublinear proof showing their product. Arithmetic circuits can be formed using these matrices, giving a more efficient reduction than earlier proof systems for circuit satisfiability
<!--SR:2022-08-11,42,170-->

Who are the authors of Groth16?
?
Jens Groth
<!--SR:2022-08-22,68,250-->

What is the title of Groth16?
?
On the Size of Pairing-Based Non-interactive Arguments
<!--SR:2022-09-28,69,190-->

What did Groth16 contribute?
?
Construction of a 3 element pairing based SNARK, and proof of a lower bound of 2 group elements in the symmetric group setting
<!--SR:2022-08-23,57,210-->

## Universal Updatable Snarks

### GKMMM18

Who are the authors of GKMMM18?
?
Jens Groth, Markulf Kohlweiss, Mary Maller, Sarah Meiklejohn, Ian Miers.
<!--SR:2022-08-23,39,230-->

What is the title of GKMMM18?
?
Updatable and Universal Common Reference Strings with Applications to zk-SNARKs
<!--SR:2022-08-16,35,250-->

What did GKMMM18 contribute?
?
A zk-SNARK with an updatable and universal CRS.
Updatability guarantees the security of the CRS as long as one party is honest.
Universality means the CRS applies to any relation.
Neither property had existed before.
<!--SR:2022-07-26,27,250-->

### MBKM19

Who are the authors of MBKM19?
?
Mary Maller, Sean Bowe, Markulf Kohlweiss, Sarah Meiklejohn
<!--SR:2022-09-26,70,270-->

What is the title of MBKM19?
?
Sonic: Zero-Knowledge SNARKs from Linear-Size Universal and Updatable Structured Reference Strings
<!--SR:2022-07-27,10,190-->

What did MBKM19 contribute?
?
A zk_SNARK with a universal updatable CRS that scales linearly with respect to the supported circuits. GKMMM18's CRS, the previous state of the art, scaled quadratically.
<!--SR:2022-08-21,38,230-->

What is MBKM19 otherwise known as?
?
Sonic
<!--SR:2022-09-08,53,250-->

### GWC21

Who are the authors of GWC21?
?
Ariel Gabizon, Zachary J. Williamson, Oana Ciobotaru
<!--SR:2022-08-27,41,210-->

What is the title of GWC21?
?
Plonk: Permutations over Lagrange-bases for Oecumenical Noninteractive arguments of Knowledge
<!--SR:2022-08-02,20,230-->

What did GWC21 contribute?
?
A zk-SNARK with an linear sized updatable universal structured reference string with practical prover time. Where the prover requires about 7.5-20 times fewer group exponentiations than Sonic/MBKM19, the previous state of the art.
<!--SR:2022-09-04,46,250-->

What is GWC21 otherwise known as?
?
Plonk
<!--SR:2022-07-31,30,250-->

# CRS MPC Protocols

## BGM19

Who are the authors of BGM19?
?
Sean Bowe, Ariel Gabizon, Ian Miers
<!--SR:2022-08-21,39,230-->

What is the title of BGM19?
?
Scalable Multi-party Computation for zk-SNARK Parameters in the Random Beacon Model
<!--SR:2022-09-17,67,270-->

What did BGM19 contribute?
?
A scalabe multi-party computation secure in the random beacon model which omits the precommitment phase, which holds even if an adversary has limited influence on the beacon.
<!--SR:2022-08-08,34,250-->

# To investigate 
Algebraic methods for interactive proof systems, Lund, Fortnow, Karloff, Nisan.
This seems to show that MIP = NEXP, and seems to have the same result as BFL. It also has to do with PSPACE. This was mentioned in Shafi Goldwasser's Turing award speech.


Groth +parents
R1CS origin
AIR origin
STARK +parents
Sonic +parents
Marlin +parents
NIZK hidden bits model
Trapdoor permutation
NIZK micali