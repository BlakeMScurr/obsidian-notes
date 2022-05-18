# 3rd School

## Lecture 1

#### IPs
Zero knowledge proofs from GMR
 	Prover knows something is true, then they interact until verifier is convinced that statement is true
GMR came up with the idea of zero knowledge here

#### Card example
How is zk even possible? Card example:
If I tell you some card from the deck is a black card. If I show you the black card I give more information. Instead I could show you all remaining 26 red cards, but not reveal which black card I have.

#### Internet voting
Groth got into ZK using internet voting. What's the point of ZKPs?
You encrypt a vote and send it to the authorities. Then they tally the votes without decrypting them using a multiparty computation.
However, we can encrypt -100 votes for Bob, how do we know a given vote is valid? ZKPs can solve this - voter sends the ciphertext and the zkp that the text is a valid vote.
ZKP.
ZKPs are common in cryptography protocols, we can use them to prove we're following the protocol correctly.

#### Round Complexity
NIZKs are where the prover only sends one message to the verifier, and the verifier sends nothing. That's what's interesting to Groth.
Generally, IZKs than NIZKs are more efficient for the prover, verifier and communication.
However, NIZKs are useful in many non interactive settings - consider an email, or posting something on social media, or sending some money etc. Many cryptographic tasks are non interactive - you make a signature or a ciphertext. Tasks where we want to prove to everyone in a canonical setting (blockchain) are implicitly non interactive, because we need to interact with a changing set of verifiers.

#### NIPs

We have a statement that $x \in L$.
Withness $w$ showing that $x \in L$, i.e., $(x, w) \in R_L$. We have a binary relation between witnesses and statements - some witnesses show that x is in L, those pairs of x and w are in the relation for that language.
Then we have $\pi$ that we send to the verifier to prove that $x \in L$.
If we didn't care about zk then the prover would just send the witness, and the verifier runs the NP relation and check that x in language. The challenge is to ensure that the prover doesn't reveal anything about the witness.

#### NIZKs
Properties: completeness, soundness, zk
Can prove a true statement
Cannot prove a false statement
Proof reveals nothing except truth of statement

#### ZK simulation
Fairly clear to show completeness and soundness, but how can we argue for zero knowledge?
The proof reveals nothing if it's possible for the verifier to simulate the proof instead of getting the proof from the prover.
I.e., if instead of getting a proof from the prover, they can just be like "oh I think the proof would be like this" then they have learned nothing more from the verifier.

#### NIZK proofs in the plain model only possible for trivial languages

But this doesn't work! I.e., we can't have the verifier able to generate the proofs totally by themselves. Shown by GO94. Why not?
Given PPP algos P, V, S (prover verifier and simulator) we can make a polynomial time decision algorithm for $x \in L$ or $x \notin L$. How does it work?
Run $S(x)  \rightarrow \pi$
Return $V(\pi)$
How do we know this works?
If $x \notin L$, soundess implies verifier algorithm rejects.
If $x \in L$ zero knowledge sholws simulation looks like real proof, and completeness means the verifier accepts.
??? why does this argument not apply for multi round interactive proofs?

#### NIZK by BFM
Blum, Feldman, and Micali get around this problem with a setup.
That extra bit of help is a common reference string.

#### CRS
Can be uniform or specific distribution. In BFM88 it's a uniform random string.
Key genreation algorithm K for generating CRS.
Let's just suppose (for now) that the CRS comes from a trusted party, a secure multi party computation, or with the multi string model per GO07 (where we only assume a majority of strings are valid (seems like sonic plonk etc have an n of 1 assumption))

#### Simulation trapdoor
How does the CRS help to allow non trivial proofs?
It helps in the simulation process.

## Lecture 2
### NIZK for Circuit SAT

Broadly, Jens Groth outlines a zero knowledge proof system for circuit satisfiability using pairings. 
	- He states the properties of the system
	- He introduces the subgroup decision assumption
	- He introduces BNG encryption
	- He introduces element commitment and its properties
	- He describes the structure of the circuit
	- He proves the soundness of the circuit
		- Proving that each value has a 0 or 1
		- Proving a NAND gate
	- He proves that the system has zero knowledge


Properties
	Perfect completeness, perfect soundness, computational zero knowledge
	Common reference string: O(1) group elements
	Proofs: O(|C|) group elements, where C is the size of the circuit
	
We use composite order groups
	n = pq for primes p and q (hence the name composite order), our groups G and G_t have order n
	Subgroup decision assumption - hard to tell if h (??? perhaps the group generated by h) has order n or q
	
BGN encryption
	Boneh-Goh-Nissim
	Public key (n, G, G_t, e, g, h), h has order q
	Secret key p, q, n= pq
	Encryption c = g^ah^r for r \rightarrow Z_n
	Decryption c^q = (g^ah^r)^q = g^{qa}h^{qr} = (g^q)^a, then we comput the discrete logarithm if a is small
	
Commitment
	Extension of the encryption scheme
	Same public key
	Commitment is the same as encryption
	a doesn't have to be a small number
	Commitment uniquely determines a mod p
	Commitment has addition and multiplication, multiplication goes to the target group
	??? what is the exact nature of the multipication? How do we know?
	
Structure of the circuits
	We want to prove that for a given circuit there is a value that can cause the output to be 1.
	Prover commits to the value of the input and intermediate wires, and a commitment the output 1 (which is trivial for the verifier to confirm).
	Prove that all the values are commitments to 0 and 1.
	Prove that all the commited values respect the NAND gates.
	
Proof for c containing 0 or 1
	We make a commiement with w
	We use the multiplication law to get an expression that is a commitment to 0 if w is 1 or 0
	We take the other part of the expression and  calculate it as a group element
	The verifier can check the proof using another element
	
Proof of NAND - soundness
	We can encode NAND as a linear equation b_0 + b_1 + 2b_2 - 2 \in {0,1} iff NAND(b_0, b_1) = b_2
	Any circuit can be encoded as NAND gates ,but any fan in 2 circuits have a similar table
	CRS is the BGN encryption key, so the size is 3 times the group element
	The proof size is (2|w| + |C|)k_G - a commitment for each wire (??? why 2 times the number of wires???), and one for each element of the circuit

ZK of the NAND proof
	We use the subgroup decision assumption
		Hard to distinguish whether h has order q or n
		The simulated crs h has order n, and we know \tau such that $h^{\tau} = g$
		\tau is the simulation trapdoor
		Commitments are nwo perfectly hiding trapdoor commitments - $g^1h^r = g^0h^{r + \tau}$
		Pretend that commitments are 0s or 1s, and the verifier doesn't know which
 		Simulator has a new crs, and just commit to 1s everywhere (simulator doesn't have witness), give proof that we contain zeroes or 1s (fine because they just contain 1s). Cheat the NAND gates, so we just pretend that some contain zeroes according to what the NAND needs.