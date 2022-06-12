#flashcards/zkps/GMR89

# The Knowledge Complexity of Interactive Proof-Systems
## Introduction
### Interactive Proof Systems
* IPs are a new method of communicating a proof
	* IPs are interactive
		* A verifier asks a series of questions of a prover
	* IPs are probabilistic
		* The verifier can be convinced of a false n-bit statement with $1/2^n$ probability
		* The verifier can be convinced of a true n-bit statement with $1-1/2^n$ probability.

What are interactive proof systems?
?
Interactive proof systems are a method of communicating a proof, they are interactive and probabilistic.
<!--SR:2022-06-29,43,190-->

What does the "interactive" in interactive proof systems mean?
?
That a verifier asks a series of questions of a prover.
<!--SR:2022-06-17,50,250-->

In what sense are interactive proofs probabilistic?
?
The verifier can be convinced of a false n-bit statement with $1/2^n$ probability.
The verifier can be convinced of a true n-bit statement with $1-1/2^n$ probability.
<!--SR:2022-06-18,30,210-->

### Knowledge Complexity
* We can investigate the knowledge (as opposed to time) complexity of a proof
	* Proofs generally convey more than just their result
		* Hamiltonian proofs give a path, not just true/false
			* A path is not just trivial information, it's real knowledge that is hard to compute
	* We can measure the knowledge conveyed by a proof
	* We can classify languages according to knowledge complexity

What is knowledge complexity?
?
A measure of the additional knowledge conveyed by a proof.
<!--SR:2022-06-30,52,230-->

What extra information does a standard NP proof of a Hamiltonian path convey?
?
The exact path itself, as opposed to just the 1 bit statement of its existence.
<!--SR:2022-06-14,44,250-->

What is knowledge as opposed to information, roughly?
?
Knowledge is information that is difficult to acquire.
<!--SR:2022-09-17,103,250-->

How can we study knowledge complexity per se, rather than instances of proof systems?
?
By classifying languages according to their knowledge complexity.
<!--SR:2022-09-02,90,230-->
 

### Interaction reduces knowledge
* Interaction may decrease knowledge complexity
	* For quadratic residuosity, interaction appears to remove the need to send m's factorisation
		* There is an interactive proof for quadratic residuosity that gives no extra knowledge
		* All efficient algorithms for quadratic residuosity require m's factorisation
		* ??? does efficient mean polynomial, i.e, in P?
		* All known NP algorithms of quadratic residuosity exhibit m's factorisation to the verifier
		* ??? is it true that "exhibit" means send from the "prover" to the "verifier" (given the 2 party understanding of NP)

How do interactive proofs relate to knowledge complexity?
?
Interaction may reduce knowledge complexity.
<!--SR:2022-09-08,94,230-->

How does adding interaction reduce the knowledge complexity of deciding quadratic residuosity?
?
It removes the need to give `m`'s factorisation, and allows a zero knowledge proof.
<!--SR:2022-10-06,116,250-->

What is true of all known NP algorithms of quadratic residuosity?
?
They exhibit `m`'s factorisation to the verifier.
<!--SR:2022-09-26,108,250-->

## Interactive Proof Systems

### NP
* NP is a formalisation of theorem proving
	* Proofs in NP are easy to verify - which loosely defines NP
	* NP is a formalisation
		* NP's parts are a prover, verifier, output tape, and input tape
		* The prover is an exponential turing machine
		* The verifier is a polynomal turing machine
		* If $x \in L$ the verifier halts and accepts

What intuitive notion is NP a formalisation for?
?
Theorem proving.
<!--SR:2022-09-19,102,250-->

What's the key property of proofs in NP?
?
That proofs are easy to verify, i.e., they can be verified in polynomial time.
<!--SR:2022-09-16,103,250-->

What "physical" parts does NP consist of?
?
A prover, verifier, input tape, and communication tape.
<!--SR:2022-09-11,91,230-->

What are NP's prover and verifier?
?
The prover is an exponential time turing machine.
The verifier is a polynomial time turing machine.
<!--SR:2022-07-21,60,230-->


### Proof Systems in General

* Theorem proving has 3 intuitive properties
	* It must be possible to prove a true theorem
	* It must be impossible to prove a false theorem
	* It must be easier to verify a proof than construct it originally
		* An inefficiently verifiable proof is uncommunicable computation and doesn't capture our intuitive notions

What are the 3 defining features of theorem proving for GMR?
?
It must be possible to prove a true theorem.
It must be impossible to prove a false theorem.
It must be easier to verify a proof than construct it originally.
<!--SR:2022-09-17,97,230-->

What, intuitively, is the difference between a proof and a computation, for GMR?
?
A proof has a is easier to verify than compute, whereas a computation must be entirely rerun to be verified.
<!--SR:2022-09-29,108,250-->

### Moving from NP to IPs

* "Proof", like "computation",  is an intuitive notion with various formalisations
	* "Computation" has the meaningfully different formalisations of, for example, deterministic Turing machines, and probabilistic Turing machines.
	* "Proof" has the formalisations of NP and now IP
	* If NP is "book proofs", IP is "classroom proofs"

What two foundational ideas are actually intuitive notions with various formalisations, for GMR?
?
Proof and computation.
<!--SR:2022-08-30,91,250-->

What are GMR's examples of formalisations for "computation?"
?
Deterministic Turing machines, and probabilistic Turing machines.
<!--SR:2022-09-28,113,270-->

What are GMR's examples of formalisations for "proof?"
?
NP and IP.
<!--SR:2022-09-07,97,250-->

What are GMR's analogies for NP and IP?
?
NP is "book proofs", IP is "classroom proofs."
<!--SR:2022-07-03,55,250-->

### IPs Informally

* IPs are "class room proofs"
	* In classrooms students can raise questions at crucial points
	* A book must, in a sense, answer possible all questions in advance
	* ??? Is "questions" really the right way to frame this? The actual protocol seems to have more to do with challenges.
	* A classroom lesson is a teacher and student in conversation about an proposition.

How might a class be more useful than a textbook?
?
In classrooms, students can raise questions at crucial points.
A book must, in a sense answer all possible questions in advance.
<!--SR:2022-09-03,87,230-->

What are the components of a classroom lesson (in the context of IPs at a high level)?
?
A classroom lesson has a *teacher* and *student* in *conversation* about a *proposition*.
<!--SR:2022-08-28,81,230-->

### Interactive Turing Machine

* An ITM models a person who listens, thinks, daydreams creatively, and speaks about an proposition
	* An ITM contains an a listening tape, a work tape, a random tape, a speaking tape, and an input tape.
		* The listening tape is read only
		* The work type is read-write
		* The random tape represents creative daydreaming
			* The random tape provides unmodelability - the uniqueness of a human mind captured by "creative daydreaming"
			* The random tape is read left to right
			* A "coin flip" means reading a random bit from the tape
			* ??? Is "creative daydreaming" really the best analogy here? Do we use daydreaming to generate challenges for others? Am I trying to capture human/ITM irreducilility?
	* The speaking tape is write only, write once, unskippable
	* The input tape represents the proposition

What does ITM stand for?
?
An Interactive Turing Machine.
<!--SR:2022-08-23,85,250-->

What does an ITM model?
?
A person who *listens*, *thinks*, *daydreams creatively*, and *speaks* about a *proposition*.
<!--SR:2022-09-13,101,250-->

What are the components of an ITM?
?
Turing machine
Listening tape
Work tape
Random tape
Speaking tape
Input tape
<!--SR:2022-07-31,67,230-->

How is an ITM's listening tape implemented?
?
It is read only.
<!--SR:2022-06-16,45,250-->

How is an ITM's work tape implemented?
?
It is a full read-write tape.
<!--SR:2022-07-06,58,250-->

What does an ITM's random tape achieve?
?
It means an ITM can't simply be modelled in an interaction with a more powerful adversary.
<!--SR:2022-06-15,45,250-->

What does an ITM's random tape represent?
?
The irreducibility/unmodelability of the human mind, we can think of this as our capacity for creative daydreaming.
<!--SR:2022-09-06,96,250-->

How is an ITM's random tape implemented?
?
It is readonly from left to right.
<!--SR:2022-06-22,48,250-->

How can we think of a read from an ITM's random tape?
?
It's a coin flip.
<!--SR:2022-06-26,52,250-->

How is an ITM's speaking tape implemented?
?
As a write only tape, where each cell can only be written once, and each cell must be written in in order to proceed to the next.
<!--SR:2022-08-11,76,250-->

What does an ITM's input tape represent?
?
The proposition being thought about.
<!--SR:2022-09-01,92,250-->

### Interactive Pair

* An pair of interactive Turing machines represents two people having a polite conversation on a proposition
	* Concretely, an interactive pair (A, B) is:
		* 2 ITMs A and B
		* Where each listens to the others' speaking tape
		* and A and B take turns being active
		* and A or B can halt the pair
	* An interactive pair defines a probability space of conversations the two people might have on a proposition
		*  a<sub>i</sub> is A's i<sup>th</sup> message, which is the entire string written during A's turn. Likewise for B.
		* The text of a computation of (A, B) on input x is { b<sub>1</sub>, a<sub>1</sub>, ..., b<sub>n</sub>, a<sub>n</sub>}. Note, a<sub>n</sub> is empty if B halts
		* The text of all possible computations of (A, B) on x is called (A, B)[x]
		* ??? What exactly is the "natural" way to take a probability space over? Are the outcomes all the possible strings in the conversation? Are the random strings uniformly distributed, i.e., is a coin flip 50%? If a probability space is $(\Omega, \mathcal{F}, P)$, is $\mathcal{F}$ just the set of accepting and not accepting? Is $P$ just the probability of that? 
		* (A, B)[x] is taken over the coin tosses of both machines

What does a pair of interactive Turing machines represent?
?
The possible polite conversations that two (particular) people might have on a proposition.
<!--SR:2022-07-08,42,210-->

How do we define an interactive pair (A, B)?
?
2 ITMs A and B.
Where each listen's to the others' speaking tape.
They take turns being active.
Either can halt the pair.
<!--SR:2022-07-14,55,230-->

What is output of an interactive pair?
?
Let $a_i$ be A's $i^{th}$ message, which is the entire string written during A's turn, likewise for $b_i$. The output is $\{b_1, a_1, ..., b_n, a_n\}$, where $a_n$ is empty if B halts.
<!--SR:2022-08-14,79,250-->

What is (A, B)[x] for an interactive pair?
?
The text of all possible computations of (A, B) on input x, taken over the distribution of the coin tosses of both machines.
<!--SR:2022-07-02,20,150-->

### Interactive Proof System Definition

* An interactive proof system is like a classroom lesson
	* On an idea
	* In a topic
	* As a conversation
	* Where true ideas can be proven
	* And false ideas cannot

* IPs are formalised where:
	* The topic is a language $\mathcal{L} \subseteq \{0, 1\}^*$
	* The idea is $x \in \mathcal{L}$
	* The conversation is the interactive pair (A, B)
	* True ideas being provable is formalised as
		* For all $x \in \mathcal{L}$, the probability that B halts and accepts $\geq 1 - 1/2^k$ for all k and sufficiently large n
		* ??? How can we encode provability precisely and concisely? Perhaps $\forall x \in L, P(a_i = \epsilon \land B_{accepts}) over B  \geq 1 - 1/n^k\;\;\;\;\forall k,\;\forall n \gt m | m \in \mathbb{N}$? In particular, what does "over b's coin flips mean in detail?", and what do "for all k" and "sufficiently large n" mean?
	* False ideas being unprovable is formalised as
		* For all $x \notin \mathcal{L}$, the probability that B halts and accepts $\leq 1/2^k$ for all k and sufficiently large n
		* ??? Why exponential? Is it different to simply approaching 1 or 0? Is it to denote that the efficiency of communication must be high?
	* Note, probabilities are taken over B (the verifier's) random coin tosses

* Note: B doesn't need a specific A, since an IP's properties apply across all possible A' provers.
* Note: IPs don't require proofs of non-membership for $x \notin \mathcal{L}$, just like NP (think co-NP, i.e., graph non-isomorphism or non-hamiltonian)

What is an interactive proof system analogous to?
?
A lesson in a classroom.
<!--SR:2022-09-02,93,250-->

What are the properties of a classroom lesson (in the context of an interactive proof system)?
?
The lesson is *on an idea*, which is *in a topic*, held as a *conversation*, where *true ideas can be proven*, and *false ideas cannot be proven*.
<!--SR:2022-07-07,50,210-->

What are the "objects" (in an OOP sense) in an interactive proof system?
?
A language $\mathcal{L} \subseteq \{0,1\}^*$, an input $x \in \mathcal{L}$, and an interactive pair $(A,B)$
<!--SR:2022-06-29,25,190-->

How is the general topic of an interactive proof system formalised?
?
As a language $\mathcal{L} \subseteq \{0,1\}^*$
<!--SR:2022-09-11,99,250-->

How is the "idea" in an interactive proof system formalised?
?
As the input $x \in \mathcal{L}$
<!--SR:2022-07-03,46,210-->

How is the notion that true ideas can be proven in an interactive proof system formalised?
?
$\forall x \in \mathcal{L}$, the probability that B halts and accepts $\geq 1 - 1/n^k$ for all $k$ and sufficiently large $n$ (taken over B's coin flips)
<!--SR:2022-06-17,18,130-->

How is the notion that false ideas cannot be proven in an interactive proof system formalised?
?
$\forall x \notin \mathcal{L}$ given as input to $(A', B)$ the probability B accepts $\leq 1/n^k$ for all $k$ and sufficiently large $n$ (taken over B's coin flips)
<!--SR:2022-06-27,17,130-->

Does a verifier in an interactive proof system require a specific prover? Why/why not?
?
No, because the properties (true statements are provable, and false ones aren't) hold independently of the prover by definition.
<!--SR:2022-07-13,53,210-->

What proofs can be constructed in an interactive proof system for $x \not in \mathcal{L}$?
$
None are guaranteed to be able to be constructed. Interactive proof systems don't concern proofs of non-membership, just like NP (think of proving a non-hamiltonian as intuitively not in NP).

### Quadratic Residuosity Interactive Proof

#### QNR

 * The quadratic non-residue language contains non-"squares" mod some large number.
	 * $Z^*_m$ denotes integers between 1 and m relatively prime to m.
	 * $a \in \mathbb{Z^*_m}$ is quadratic residue mod m if $a = x^2\ mod\ m$ for some $x \in \mathbb{Z^*_m}$
	 * $a \in \mathbb{Z^*_m}$ is quadratic non residue mod m if $a \neq x^2\ mod\ m$ for any $x \in \mathbb{Z^*_m}$
	 * $QNR =\mathcal{L} = \{m,x | x \in Z^*_m is\ quadratic\ non\ residue\}$
 * $QNR \in NP$
	 * Factorising m allows us to use an efficient algorithm reminiscent of euclid's algorithm that involves the basic consequences of the quadratic reciprocity formula.

What is QNR, loosely?
?
The quadratic non residue language. The language of non-"squares" mod some large number.
<!--SR:2022-08-18,82,250-->

What is $\mathbb{Z^*_m}$?
?
The integers between 1 and m relatively prime to m.
<!--SR:2022-08-27,89,250-->

$a \in \mathbb{Z}^*_m$ is a quadratic residue if . . . ?
?
$a = x^2\ mod\ m$ for some $x \in \mathbb{Z}^*_m$
<!--SR:2022-06-22,48,250-->

$a \in \mathbb{Z}^*_m$ is a quadratic non-residue if . . . ?
?
$a \neq x^2\ mod\ m$ for all $x \in \mathbb{Z}^*_m$
<!--SR:2022-09-24,103,250-->

Is $QNR \in NP$? How do we know?
?
Yes. If the prover factorizes m, the verifier can decide quadratic residuosity in polynomial time using a method like euclid's algorithm that uses quadratic reciprocity.
<!--SR:2022-06-27,52,250-->

#### QNR IP

##### Protocol

* QNR has a simple Interactive Proof System
	* ??? Why are we making a protocol for QNR rather than QR? Is it because we can easily for known quadratic residues, but we can't form quadratic non-residues, so we can't easily construct a mix of a known nature?
	* B (the verifier) chooses $n = |m|$ random members of $\mathbb{Z}^*_m$, $\{r_1, r_2,..., r_n\}$
		* ??? Can we choose a random element of $\mathbb{Z}^*_m$ efficiently by choosing a random number less than m and checking its relative primality with euclid's algorithm (or similar)?
		* ??? How much is $|m|$? Is it $log_2 m$? It could also be $m$, depending on whether we interpret bars as absolute value or string length.
	* B flips n coins and forms $\{t_1, t_2, ..., t_n\}$
		* If tails, B forms $t_i = xr_i^2\ mod \ n$
		* If heads, B forms $t_i = r_i^2\ mod\ n$
	* B sends $\{t_1, t_2, ..., t_n\}$ to A
	* A tells B their coin flips

What does B do in the basic QNR IP?
?
Choose random numbers.
Form squares (i.e., non residues).
Mix/multiply some with input x.
Sends the mix to A.
<!--SR:2022-06-21,39,230-->

How does B mix random numbers with x in the basic QNR IP?
?
B flips n coins and forms $\{t_1, t_2, ..., t_n\}$
If tails, B forms $t_i = xr_i^2\ mod \ n$
If heads, B forms $t_i = r_i^2\ mod\ n$
<!--SR:2022-08-12,77,250-->

What does A do in the basic QNR IP?
?
Calculates B's coin flips by deciding quadratic residues, and sending those flips back to B.
<!--SR:2022-08-21,84,250-->

##### Properties

* The above forms an interactive proof system
	* If $x \in QNR$, then $xr_i^2 \in QNR$ and $r_i^2 \notin QNR$, so the prover can perfectly pick the coin toss.
		* Note that convincing B with a probability of $1$ is better than a $1 - 2^n$ probability (the first requirement of an interactive proof system).
	* If $x \notin QNR$ then $r_i^2$ and $r_i^2x^2$ are random quadratic residues which A can't distinguish.
	* A has a 1/2 chance of guessing each toss.
	* A has a $1 - 1/2^n$ chance of convincing B of a false statement (the second reuirement of an interactive proof system).
		* Note that this probability is only given by chosing $n = |m|$ and by chosing a higher or lower n we get a different probability.
* This system is not zero knowledge.
	* B can form $\{t_1, ... t_n\}$ such that they learn additional information from the answers. By setting t to some random element of $\mathbb{Z}$ gives the quadratic residuosity of t (if A acts according to the protocol).

How do we know that we can prove $x \in \mathcal{L}$ with sufficient probability in the basic QNR IP?
?
$x \in QNR \implies xr^2 \in QNR \land r^2 \notin QNR$ so the prover can perfectly pick the coin toss.
<!--SR:2022-08-25,87,250-->

How do we know that we can't falsely prove $x \in \mathcal{L}$ (i.e., where $x \notin \mathcal{L}$) with non-negligible probability for the basic QNR IP?
?
$x \notin QNR \implies xr^2 \notin QNR \land r^2 \notin QNR$ making either case a random quadratic residue.
So the verifier has a $1/2$ chance of picking any given toss, and a $1/2^n$ chance of getting all n tosses.
<!--SR:2022-08-15,80,250-->

How many coin flips does the verifier do in the basic QNR IP?
?
$n = |x|$, i.e., the length of x.
<!--SR:2022-08-13,78,250-->

How is the basic QNR IP not zero knowledge?
?
By acting maliciously and sending a random element with unknown residuosity, B learns its residuosity.
<!--SR:2022-09-08,97,250-->

### The Class IP

* IP, Interactive Polynomial-time, is the class of languages possessing an interactive proof system.
* $IP_T(n)$ is the class of languages where the prover runs in $T(n)$ time
* IP[f(n)] is the class of languages where the system halts withing f(n) turns where n is the length of the input string.

What is IP?
?
The class of languages possessing an interactive proof system.
<!--SR:2022-08-19,83,250-->

What is $IP_{T(n)}$?
?
The class of languages with an interactive proof system where the prover runs in $T(n)$ time.
<!--SR:2022-08-07,73,250-->

What is $IP[f(n)]$?
?
The class of languages with an interactive proof system that halts within $f(n)$ turns.
<!--SR:2022-06-24,17,230-->

### Arthur Merlin Games
* "Arthur-Merlin" by Babai games are a predecessor of IPs by GMR
	* Merlin is the prover and Arthur is the verifier
	* AM games differ from IPs in that the prover sees all coin tosses
	* AM games don't require arbitrary interaction - it's sufficient for Arthur to talk and Merlin to respond.

Who invented Arthur-Merlin games?
?
László Babai.
<!--SR:2022-08-09,75,250-->

Which came first, Arthur-Merlin games, or Interactive Proof Systems?
?
Arthur-Merlin games.
<!--SR:2022-09-21,108,270-->

How do the features of Arthur-Merlin games compare to interactive Proof Systems?
?
Merlin is similar to the prover, and Arthur the verifier.
They differ in that in an Arthur-Merlin game, the prover sees all coin tosses, and they don't require arbitrary interaction (it's sufficient for Arthur to talk and Merlin to respond).
<!--SR:2022-07-17,56,230-->

### Interactive Hierarchy

* $L \in AM \implies L \in NP$ for a random oracle
* $AM \subseteq IP$, in fact $AM \subseteq IP[1]$
* Probably $AM \subset IP$ according to GMR
* Probably $IP[k] \subset IP[k+1]$ according to GMR

How do classes AM and NP compare?
?
$L \in AM \implies L \in NP$ for a random oracle
<!--SR:2022-07-19,37,190-->

How do classes AM and IP compare?
?
$AM \subseteq IP$, in fact $AM \subseteq IP[1]$, probably $AM \subset IP$ according to GMR.
<!--SR:2022-06-29,29,230-->

What is the interactive hierarchy, for GMR?
?
The hypothesis that strictly $IP[k] \subset IP[k+1]$
<!--SR:2022-08-05,71,250-->



## Knowledge
### Philosophy of Knowledge
#### Notions of Knowledge

#### MCF

* Consider communication as a tool for transfering knowledge
* The MCF (Model Centric Framework) is a previous formalisation for knowledge and communication
	* MCF captures people's inherently limited knowledge about the physical world, but doesn't capture the difficulty in thinking things through
	* MCF assumes infinite computing power by all
	* MCF assumes input can be hidden to different participants
	* MCF pertains to getting knowledge about the physical world in the form of experiment and empirical evidence.

What is communication for, according to GMR?
?
Transferring knowledge.
<!--SR:2022-06-19,48,250-->

What is MCF?
?
The Model Centric Framework is a formalisation for knowledge and communication.
<!--SR:2022-09-10,92,230-->

What worldview does MCF capture?
?
The scientific/empricial worldview that it's hard to learn facts about reality, and that we communicate testimony about those facts.
<!--SR:2022-07-01,28,190-->

What are MCF's assumptions?
?
Infinite computing power by all. The various inputs discussed can be hidden to different participants.
<!--SR:2022-08-28,89,250-->

#### GMR vs MCF

* GMR differ from the MCF
	* GMR hold that computation is limited and we study available objects
		* This is logical in an adversarial/cryptographic context, as there can be no proofs about the non-availability of inputs, but we can reasonably assume computational limitations.
	* GMR studies what a polynomially bounded participant can learn from communication
	* GMR studies the quantity of knowledge required to prove a theorem
	* ??? are the "lessons from communcation" and "knowledge to prove a theorem" ultimately the same in GMR? I.e., that if the knowledge required to prove a theorem is 0, then the amount learned by the communication of that theorem is also 0?
	* GMR's notion of knowledge doesn't just apply abstractly to discourse, but is useful in cryptography

How do GMR differ from the MCF philosophically?
?
GMR hold that our computation is limited, and that we communicate about available public inputs.
<!--SR:2022-08-10,76,250-->

What does GMR's philosophy of knowledge apply to, in addition to epistemology?
?
Cryptography.
<!--SR:2022-09-10,99,250-->

What does GMR study with respect to knowledge?
?
What a polynomially bounded participant can learn from communication.
The quantity of knowledge required to prove a theorem.
<!--SR:2022-06-19,33,210-->

### Distinguishing
#### Ensembles

* An I-c-ensemble represents a probabilistic computation (with polynomially bounded output) on a language
	* An ensemble is used as an abstraction that lets us compare and distinguish different types of computations
		* $I$ is the strings of a language
		* $x$ is the input of the computation
		* $\Pi_x$ is the distribution of outputs on $x$
		* $c$ is greater than or equal to the highest power of the polynomial restricting the output size, so that all possible ouputs are represented in the ensemble
	* An ensemble is formalised as a probability distribution
		* Let $I$ be an infinite set of strings
		* Let $c$ be a positive constant 
		* $\forall x \in I$ where $|x| = n$ let $\Pi_x$ be a probability distribution over $n^c$ bit strings
		* We say $\Pi = \{\Pi_x | x \in I\}$ is an I-c-ensemble.

What does an I-c-ensemble represent?
?
The possible outputs (with polynomially bounded length) of a probabilistic computation over the strings in some language.
<!--SR:2022-06-26,16,130-->

What is an I-c-ensemble used for?
?
As an abstraction that allows us to compare and distinguish different types of computations.
<!--SR:2022-08-02,63,210-->

What is an I-c-ensemble's $I$ through a computational lens?
?
The language accepted by the probabilistic computation.
<!--SR:2022-07-03,21,190-->

What is an I-c-ensemble's $x$ through a computational lens?
?
The input of a computation.
<!--SR:2022-09-06,95,250-->

What is an I-c-ensemble's $\Pi_x$ through a computational lens?
?
The distribution of outputs on $x$
<!--SR:2022-09-14,101,250-->

What is an I-c-ensemble's $c$ through a computational lens?
?
The highest power (probably +1) in the polynomial restricting the output size, so that all possible outputs are represented in the ensemble.
<!--SR:2022-08-22,81,230-->

How do we define an I-c-ensembles's $I$?
?
An infinite set of strings.
<!--SR:2022-07-04,56,250-->

How do we define an I-c-ensembles's $c$?
?
Some natural number.
<!--SR:2022-08-29,90,250-->

How do we define an I-c-ensembles's $\Pi_x$?
?
$\forall x \in I$ where $|x| = n$ let $\Pi_x$ be a probability distribution over $n^c$ bit strings
<!--SR:2022-07-29,66,230-->

How do we define an I-c-ensemble $\Pi$?
?
We say $\Pi = \{\Pi_x | x \in I\}$ is an I-c-ensemble.
<!--SR:2022-09-15,102,250-->


#### Distinguishers

* A distinguisher represents a computationally bounded adversary trying distinguish encrypted data from truly random data
	* For an interactive proof, we use it to represent the verifier attempting to learn whatever extra knowledge it can from the prover's messages
	* A distinguisher is a probabilstic polynomial time algorithm D that takes a string $s$ and oupts a bit.
	* Distinguishers distinguish between two ensembles
		* Let $\Pi_1 = \{\Pi_{1,x} |\ x\ in\ I\}$ and $\Pi_2 = \{\Pi_{1,x} |\ x\ in\ I\}$ be I-c-ensembles
		* Let $p^D_{x, 1}$ denote the probability that D outputs 1 on the input a $|x|^c$ bit long string chosen with $\Pi_{1,x}$
		* Let $p^D_{x, 2}$ denote the probability that D outputs 1 on the input a $|x|^c$ bit long string chosen with $\Pi_{2,x}$

What does a distinguisher represent in general?
?
A computationally bounded adversary trying to distinguish between distributions, such as encrypted data from truly random data, or the output of an interactive proof system from an imitator.
<!--SR:2022-06-25,33,210-->

What does the distinguisher represent in an Interactive Proof?
?
An verifier trying to tell its own studies apart from notes taken in class.
<!--SR:2022-07-11,53,230-->

What is the definition of a distinguisher?
?
A probabilistic polynomial time algorithm $D$ that takes a string $s$ and outputs a bit.
<!--SR:2022-09-12,100,250-->

What, formally, does a distinguisher distinguish between?
?
Two I-c-ensembles $\Pi_1 = \{\Pi_{1,x} |\ x\ in\ I\}$ and $\Pi_2 = \{\Pi_{2,x} |\ x\ in\ I\}$
<!--SR:2022-06-18,17,150-->

What does $p^D_{x, 1}$ denote?
?
The probability that D outputs 1 on the input a $|x|^c$ bit long string chosen with $\Pi_{1,x}$
<!--SR:2022-09-09,98,250-->

What does $p^D_{x, 2}$ denote?
?
The probability that D outputs 1 on the input a $|x|^c$ bit long string chosen with $\Pi_{2,x}$
<!--SR:2022-07-18,58,230-->

#### At Most Distinguishable

* Two ensembles are "at most p-distinguishable" if they can only be told apart with a p(n) probability
	* Let $p:N \to [0,1]$
	* We say ensembles $\Pi_1, \Pi_2$ are "at most p-distinguishable" if, for all distinguishers D, $|p^d_{x,1} - p^d_{x,2}| < p(|x|) + 1/|x|^k$ for all k and sufficiently long x.
		* ??? why are we requiring the probability difference to grow faster than any polynomial? Is it because that captures the intuitive notion of distinguishability? Or is it because there exists some reduction, where a polynomial machine could take any polynomial distinguishability and reduce it (to linear or a lower degree polynomial etc)?

When (at a high level) are two ensembles "at most p-distinguishable?"
?
If they can be told apart with at most p(n) probability
<!--SR:2022-07-10,51,230-->

Ensembles $\Pi_1, \Pi_2$ are "at most p-distinguishable" if . . .?
?
for all distinguishers $D$, $|p^d_{x,1} - p^d_{x,2}| < p(|x|) + 1/|x|^k$ for all k and sufficiently long x.
Where $p:N \to [0,1]$
<!--SR:2022-06-15,22,190-->


#### 0-Distinguishability

* 0-distinguishability is an important case of p-distinguishability for cryptography
	* We call 0-distinguishable ensembles indistinguishable
	* Indistinguishable ensembles are "equal" with respect to any polynomial time computation.
	* Indistinguishability was discussed before GMR for probabilistic encryption and pseudo random number generation.

* zkQNR is 0-distinguishable but moreso
	* The probabilities for all $|x|^c$ bit string are equal, except a set of strings whose total probability doesn't exceed $1/2^{d|x|}$ for some d between 0 and 1.
	* This extra indistinguishability is not necessary for the theory of zero knowledge

* distinguishers are fed a single $|x|^c$-bit string at a time
	* 0-dist ensembles remain 0-dist even if we feed m strings at a time, provided $m < poly(|x|)$
	* p-dist ensembles may become radically more distinguishable if fed multiple strings
		* This relates to the security of encryption key reuse
			* ??? Should we think of $\Pi_1$ as true random, and $\Pi_2$ as the text encrypted with k? Then $x_1$, $x_2$ messages may make it easier to tell the ciphertext from random, thus partially decrypting it.

What are 0-distinguishable otherwise described as?
?
Indistinguishable.
<!--SR:2022-09-05,95,250-->

What does it mean for two ensembles to be indistinguishable?
?
That they are "equal" with respect to any polynomial time computation. At least, their difference vanishes superpolynomially.
<!--SR:2022-06-18,13,130-->

What was distinguishability used for before GMR?
?
Probabilistic encryption and pseudo random number generation.
<!--SR:2022-06-24,37,230-->

In what sense is zkQNR indistinguishable?
?
Strictly more than traditional indistinguishability: for all $|x|^c$ bit string are equal, except a set of strings whose total probability doesn't exceed $1/2^{d|x|}$ for some d between 0 and 1.
<!--SR:2022-07-02,41,230-->

??? how does this further notion of indistinguishability map onto my understanding of the proof for the zero knowledge of the protocol?

Which notion of indistinguishability presented in GMR is necessary for zero knowledge?
?
"at-most-0-distinguishable", as opposed to "largely equal distributions aside from a vanishing sum" which zkQNR additionally fulfills.
<!--SR:2022-07-24,61,230-->

How much data is each distinguisher fed at a time?
?
A single $|x|^c$-bit string
<!--SR:2022-06-21,29,210-->

What happens to 0-distinguishable ensembles if they're fed $m > 1$ strings?
?
They remain 0-distinguishable, provided $m < poly(|x|)$.
<!--SR:2022-06-16,13,130-->

What happens to p-distinguishable ensembles if they're fed $m > 1$ strings?
?
They may become significantly more distinguishable.
<!--SR:2022-08-24,86,250-->

Why does feeding $m > 1$ strings to a distinguisher matter for encryption schemes?
?
It can be equivalent to sending multiple messages encrypted by the same key, which may significantly reduce the distinguishability of the ensembles and security of the encryption.
<!--SR:2022-08-16,80,250-->
### Knowledge Communication
#### Knowledge Communication Definition
* Communications that convey knowledge are those that output an infeasible computation
	* Transmitting random bits does not convey knowledge because we can generate them ourselves.
		* ??? this is somewhat non-obvious to me, is this intuition part of the reason we define I-c-ensembles, and indeed Interactive proof systems as probabilstic computations? Perhaps if our distinguishers were deterministic machines we could not feasibly generate randomness, and random information (and stuff mixed with it) would become knowledge.
	* Transmitting the result of a polynomial computation does not convey knowledge because we can compute it ourselves.
	* Knowledge communication can be expressed in bits

Informally, which communications convey knowledge?
?
Those that transmit the output of an unfeasible computation, a computation that we cannot perform ourselves.
<!--SR:2022-06-25,37,230-->

How much knowledge do random bits convey and why?
?
None because we could generate them ourselves trivially.
<!--SR:2022-08-26,88,250-->

How much knowledge do the results of a polynomial computation convey and why?
?
None because we could compute it ourselves easily.
<!--SR:2022-09-04,94,250-->

What is the unit for knowledge communcation?
?
Bits.
<!--SR:2022-06-18,53,270-->

#### Machine Ensembles
* Probabilistic (polynomial output) turing machines generate ensembles
	* $M[x]$ is the possible outputs of M on $x in I$
	* $M[.] = {M[x] | x \in I}$
* $(A, B)[.]$ is the ensemble associated with the ITM pair $(A, B)$.

How do we define the the possible outputs of a probabilistic turing machine?
?
The I-c-ensemble $M[.] = \{M[x] | x \in I\}$ where $M[x]$ is the possible outputs of M on x.
<!--SR:2022-06-25,32,190-->

How do we characterise and denote the possible outputs of an ITM pair?
?
As an I-c-ensemble $(A,B)[.]$
<!--SR:2022-06-19,19,230-->

#### Communication
* We can think of communication measurement as a student scrutinising a lesson for hidden knowledge
	* He imitates the lesson as best he can
	* He distinguishes the lesson from his imitation as best he can
	* The degree to which he can distinguish is the degree to which the lesson conveyed real esoteric knowledge
	* ??? How does the $1-1/2^n$ in the definition of communiction give bits of knowledge? There is some intuition that seems sensible here, namely that we're using $1/2^n$ to achieve some notiong of bits rather than quantities of information, making it somewhat logarithmic perhaps. Although, $1/2^n$ is not exactly a logarithm at all. So perhaps it has something to do with undoing the probability issue. Moreover, the fact we have a division and negation means that communication and distinguishability go up together, which is good, since a more distinguishable set ensembles intuitively communicate more. But when I consider a protocol that communicates n bits of information, and I imagine a 1 bit string, that implies our ensembles are at most $1-1/2^1=1/2$ distinguishable, or rather, for all distinguishers, the difference between the chance of those outputs is less than 1/2. How does that imply that 1 bit is communicated? If we had a 1 bit string and 1 bit is communicated, surely we'd need the at most distinction to be 1. Well, actually maybe that doesn't follow. Certainly if the distinction were 1 we'd communicate 1 bit, but perhaps we communicate a whole bit for a 1/2 distinction. Nonetheless, it's hard to think of how there could be a 1/2 distinction where 1 bit is communicated.
	* ??? does it matter that $f(n)$ is non-decreasing?

$A$ communicates at most $f(n)$ bits of knowledge to $B$ if . . . ?
?
There exists a probabilstic polynomial-time machine M such that the I-c-ensembles $M[\cdot]$ and $(A,B)[\cdot]$ are at most $1-1/2^{f(n)}$ distinguishable.
<!--SR:2022-06-16,4,150-->

$A$ communicates at most $f(n)$ bits of knowledge if . . . ?
?
For all polynomial time ITMs B', A communicates at most $f(n)$ bits of knowledge to B'
<!--SR:2022-06-17,21,190-->

What is my analogy for determining the knowledge conveyed from a prover to a verifier?
?
An apprentice wizard takes a lesson in esoteric knowledge.
At home he tries to extract the esoteric knowledge.
First he imitates the lesson as best he can.
Then he scrutinizes, as best he can, the difference between his imitation and the lesson.
To the degree that they are different, some knowledge has leaked.
<!--SR:2022-08-08,74,250-->

How do I extend my analogy for determining knowledge to cover all the knowledge conveyed by a prover?
?
Consider the most malicious student aiming to get whatever lessons he can from the wizard, even by tricking him during the lesson.
<!--SR:2022-08-17,81,250-->

* The imitator M tries to select as string "as undistinguishable as possible" from a computation randomly selected from $(A,B)[\cdot]$.
	* No information is hidden from M
		* A, B, and x are all inputs of M
		* A's program may not help M since it might not be feasible to compute polynomially
		* ??? How is it actually justifiable that M has all the programs as input? Feels kinda like cheating. I guess the confusion here is that we feel the prover's program should be private, but really it's only the knowledge that it generates that's private.

What does the imitator machine M try to do?
?
Select as string as undistinguishable as possible from a computation randomly selected from $(A,B)[\cdot]$
<!--SR:2022-08-23,86,250-->

What are the inputs of imitator M?
?
A's program, B's program, and the input x. That is, nothing in the interactive proof is hidden.
<!--SR:2022-09-03,94,250-->

Can imitator M run A's program?
?
Not necessarily, as A's program may be absolutely inefficient, and M is polynomially bounded.
<!--SR:2022-08-04,71,250-->


#### Reporter and Policeman
*  GMR's analogy for communication complexity is a reporter and policeman
	*  Police understands the rights of the press but wanna keep things private
	*  Either the reporter already knows what the cop will say
		*  i.e., the reporter's chance of generating the police's statements is 1
	*  Or the reporter kinda knows
		*  i.e., the reporter's chance of generating the police's statements is 3/4
	*  Or the reporter doesn't know at all
		*  i.e., the reporter's chance of generating the police's statements is, say, 1/2^100

What is GMR's analogy for communication complexity?
?
A reporter trying to get information from a policeman who wants to keep most information private.
<!--SR:2022-08-06,73,250-->

What are the cases in GMR's communication complexity analogy?
?
The reporter knows what the cop will say - i.e., their chance of generating the police's statements is 1. i.e., zero knowledge.
The reporter knows some of what the cop will say - i.e., their chance '' '' is, say 3/4, i.e., some knowledge
The reporter doesn't know what the cop will say - i.e., their chance '' '' is 0, i.e., a lot of knowledge is communicated
<!--SR:2022-09-22,116,270-->

#### KC of naive QNR
 
 * In naive QNR, A communicates at most 0 its to B
	 * M simulates B since B is polynomial
	 * M can simulate A by just looking at B's coin tosses directly
 * If $QNR \notin NP$ A communicates more than 0 bits
	 * B' can learn the unknown residuosity of some $t_i$ by sending it to A

How much information does A communicate to B in naive QNR IP? (Multi round version, not just NP version).
?
Zero.
<!--SR:2022-07-26,64,250-->

How does M simulate (A,B) in naive QNR?
?
M can simply simulate B since B is polynomial.
M can simulate A by just looking at B's coin tosses directly, since B knows the residuosity of each number.
<!--SR:2022-08-20,83,250-->

How much information does A communicate in naive QNR?
?
More than Zero if $QNR \notin PP$, namely the residuosity of each $t_i$
<!--SR:2022-06-18,33,230-->

How does B' work in naive QNR?
?
B' is an adversarial verifier trying to learn additional knowledge. B' can learn the unknown residuosity of some $t_i$ by sending it to A.
<!--SR:2022-08-22,85,250-->
### Knowledge Complexity
#### Knowledge conveyed by a Theorem Proof

 * We can measure the additional knowledge conveyed when proving a theorem
	 * We are particularly interested in when the additional knowledge is 0
	 * Usually we convey more information than the truth of the theorem
		 * NP style QR conveys a square root of x in additional to deciding $x \in QR$

What additional information does the super basic NP style algorithm for proving $x \in QR$ convey?
?
A square root of x, in addition to showing $x \in QR$
<!--SR:2022-07-01,41,230-->

How much knowledge do traditional proofs of theorems convey?
?
More than language membership, think NP style QR.
<!--SR:2022-09-01,90,250-->

What is the notion of "$L$ has $f(n$) knowledge complexity" meant to capture?
?
The the prover conveys $f(n)$ addition knowledge to the verifier during a proof.
<!--SR:2022-08-03,70,250-->

#### Definition of Knowledge Complexity
Note: by restricting to the strings in the language we can use the notion of zero knowledge communication, but still let the one bit membership notion "slip through."

* We say that L has knowledge complexity f(n)
	* If, when restricting the inputs of (A,B) to the strings in L, A communicates at most f(n) bits of knowledge
	* We say that $L \in KC(f(n))$

How do we denote that $L$ has knowledge complexity $f(n)$?
?
$L \in KC(f(n))$
<!--SR:2022-08-25,85,250-->

$L$ has knowledge complexity $f(n)$ if . . . ?
?
When restricting inputs of $(A, B)$ to the strings in $L$, A communicates at most $f(n)$ bits of knowledge.
<!--SR:2022-07-04,41,230-->

#### Zero *extra* knowlege
 * ??? Is it reasonable to call the text of a zero knowledge computation "irrelevant" for any other purpose? It may be useful for speeding up polynomial computations.
 * ??? How can we construct a zero knowledge proof of a polynomial computation? Like, that we know the preimage of a hash that can be computed in polynomial time? Is it because computing the preimage is actually not polynomial? Is this an inherent restriction on real world proofs - that since we measure knowledge with respect to a polynomial computation, proving a polynomial computation with an IP etc is nonsense? Is this made more sensible with succintness? Is privacy only possible for already super-polynomial calculations? What about an x^10000 calculation? Does zk give us protection knowledge leak there?

* We can break knowledge complexity down informally
	* We focus on members of the language because if $x \notin L$ A gives up or is caught out, and the communication is not worth analysing
	* If $x \in L$
		* The verifier is rightly convinced that $x \in L$
		* The verifier has the text of the computation
			* But the text contains no more than f(n) extra knowledge, for any possible verifier
				* That is, we can always make texts (1-1/2^f(n))-distinguishable from the "real" texts
					* ??? why is "real" in quotes in the paper? There really are real texts that are formed from interactive proofs. Is the point to say that the actual texts are the same and there is no particularly real one; that only their origin is different?
* If $L \in KC(0)$, B learns $x \in L$ but the text is of no other use, and can be generated easily.

What how much knowledge is conveyed by an interactive proof if $x \notin L$?
?
Interactive proofs are only defined for "yes-instances", and their complexity of a false proof is not analysed. The prover would "give up" or be "caught out", so the possible knowledge conveyed is not meaningful.
<!--SR:2022-07-27,65,250-->

What is the verifier left with at the end of an interactive proof?
?
The knowledge that $x \in L$.
The text of the computation with the prover, containing no more than $f(n)$ extra knowledge, no matter how cleverly and maliciousy the verifier operates
<!--SR:2022-06-16,31,210-->

What does it mean practically that the verifier's text has at most $f(n)$ extra knowledge after an interactive proof?
?
That we can always make texts $(1-1/2^{f(n)})$-distinguishable from the "real" text.
<!--SR:2022-07-10,35,230-->

If $L \in KC(0)$, the verifier learns . . . ?
?
That $x \in L$, but the text is of no other use, and could in fact the text could easily have been generated without the prover.
<!--SR:2022-06-28,43,230-->

#### Applications of Knowledge Complexity

* Languages, or equivalently, theorem proving procedures are intended to communicate knowledge, and are naturally classed by their knowledge complexity for GMR.
* Knowledge complexity is defined for NP, since they're a special class of IP.
* Knowledge complexity allows us to prove the correctness of cryptographic protocols in a modular way.
	* ??? How though?

For GMR, what is the theoretical application for knowledge complexity and why?
?
Classifying languages. Languages, or equivalently, theorem proving procedures are intended to communicate knowledge, and are naturally classed by their knowledge complexity, for GMR.
<!--SR:2022-06-26,26,210-->

For which well known complexity class, known prior to the notion of knowledge complexity, is knowledge complexity defined for?
?
NP, since it's a special class of interactive proofs.
<!--SR:2022-07-30,68,250-->

How can knowledge complexity be used for cryptography?
?
For proving the correctness of cryptographic protocols in a modular way.
<!--SR:2022-07-08,50,230-->




## Languages in KC(0)
### Why QNR is interesting
#### KC(0)-BPP

* We want to characterise the languages in KC(0)
	* We want to characterise KC(0)'s relationship to other known complexity classes like P, NP, BPP, RP etc.
	* Triviallys, KC(0) includes P, RP, and BPP
		* Because all those languages can be decided with a polynomial machine. Meaning the verifier can just calculate everything themselves, forming an interactive proof system where $(A,B)[\cdot]$ is identical to the empty string.
	* Any NP style proof system for a language not in BPP releases some additional knowledge
		* An NP prover sends one message. If the message released no knowledge then it would be imitiable by a probabilistic turning machine, and therefore the language would be in BPP.
		* ??? how can non-interactive proofs be possible in light of this fact? How can access to a random string suffice?
	* Is KC(0)-BPP a fancy name for the empty set?
		* Analogously, is RP-P a fancy name for the empty set?
			* Primality testing is in RP and seems not to be in P. But we don't know, seince we don't yet know how to prover the lower bounds of possible solutions to decision problems.

How, in an abstract sense, can we study the characteristics of KC(0)?
?
By comparing it to other language classes.
<!--SR:2022-06-14,32,230-->

What are the trivial relationships between KC(0) and polynomial languages and how do we know?
?
$P \subseteq KC(0),\ RP \subseteq KC(0),\ BPP \subseteq KC(0)$
Intuitively, polynomial computation is defined as "easy" and not containing knowledge.
All these languages can be decided with a probabilistic polynomial machine. Hence a trivial polynomial imitator machine can be constructed with an identical ouput, thus communicating zero knowledge.
<!--SR:2022-09-18,101,250-->

How much knowledge does an NP proof for a language not in BPP communicate and how do we know?
?
More than zero.
An NP prover sends one message. If the message released no knowledge then it would be imitable by a probabilistic turing machine, and therefore the language would be in BPP.
<!--SR:2022-08-24,73,230-->

Why is KC(0)-BPP of interest to GMR?
?
If KC(0)-BPP is non empty, then there are non-trivial zero knowledge proofs.
<!--SR:2022-07-22,60,250-->

What set (subtraction) preceding GMR, is analogous to KC(0)-BPP for GMR and why?
?
RP-P, there appears to be a language, namely primality testing, which may be in RP-P (it is certainly in RP, and maybe P). A similar language would be useful to distinguish KC(0) and BPP.
<!--SR:2022-07-16,38,230-->

#### Known languages in KC(0)-BPP
* There are 2 languages known to be in KC(0)-BPP
	* BL
		* BL is proposed by Blum when he designed a means for a two party coin flip. He gaves all the essential ingredients to show that $BL \in KC(0)$.
		* Let n be a number with prime factorisation $n = p_1^{h_1}...p_k^{h_k}$. Then $n \in BL$ if the number of different primes congruent to 3 mod 4 is even.
	* QNR
		* The quadratic residuosity predicate $\mathcal{Q}_m(y)$ is 0 if y is a quadratic residue and 1 otherwise
		* $QNR = L = \{ (y,m)|\mathcal{Q}_m(y) = 1 \}$
		* The proof that $L \in KC(0)$ doesn't rely on any unproven complexity assumptions.

What languages did GMR know to be in $KC(0)-BPP$?
?
QNR and BL.
<!--SR:2022-07-25,63,250-->

Who invented the language BL?
?
Manuel Blum.
<!--SR:2022-09-04,90,250-->

Why was the language BL interesting to GMR?
?
Because it was presented with all the ingredients required to prove that $BL \in KC(0)$
<!--SR:2022-09-15,98,250-->

Why was the language BL invented?
?
To solve the problem of flipping a coin over the telephone.
<!--SR:2022-08-02,70,250-->

What is the definition of the BL language?
?
Let n be a number with prime factorization $p_1^{h_1}...p_k^{h_k}$. Then $n \in L$ if the number of different primes congruent to 3 mod 4 is even.
<!--SR:2022-07-02,32,230-->

What is the definition of the quadratic predicate?
?
$\mathcal{Q}_m(y) = 0$ if y is quadratic residue mod m, and $1$ otherwise.
<!--SR:2022-07-28,65,250-->

What is the definition of the language QNR?
?
$QNR = \{(y, m) | \mathcal{Q}_m(y) = 1\}$
<!--SR:2022-06-17,35,230-->

GMR's proof that $QNR \in KC(0)$ relies on . . . ?
?
No unproven computational complexity assumptions.
<!--SR:2022-09-05,90,250-->


### The Quadratic Residuosity Problem
#### Difficulty of the QRP
* The QRP is a key discussion point in Gauss's Disquisitiones Arithmeticae, along with primality testing, integer factorization, and diophantine equations.

*   Solving the QRP for $m \in \mathbb{N}$ an $x \in \mathbb{Z}^*_m$, consists of computing $\mathcal{Q}_m(x)$
	* If the factorization of $m$ are known, it's trivial to compute $\mathcal{Q}_m$
	* If the factorization of $m$ is unknown, there is no known efficient procedure for computing $\mathcal{Q}_m$
	* A polynomial time solution to the QRP would imply a probabilistic polynomial time solution for other open problems in Number Theory such as deciding whether a composite integer is the product of 2 or 3 primes.

#### Jacobi Symbol
* The Jacobi symbol $\genfrac(){}{0}{x}{m}$ evaluates to 1 or -1 and gives information on the residuosity of x in $\mathbb{Z}^*_m$.
	* If $\genfrac(){}{0}{x}{m} = -1$ then $\mathcal{Q}_m(x) = 1$
		* ??? how do we know?
	* If $\genfrac(){}{0}{x}{m} = 1$ then computing $\mathcal{Q}_m(x)$ is hard
		* In fact, it is not even known how to efficiently produce a single "guaranteed" quadratic non-residue mod $m$ with Jacobi symbol 1
			* ??? what exactly does this mean? Is it that there is no efficient procedure for generating such numbers? Obviously there's the trivial method, which is that 2 is apparently a quadratic non residue mod 9 with a jacobi symbol of 1, so we can efficiently generate (2,9) in constant time lmao. Oh! It's that given $m$ we can't find a qnr with jacobi 1, right? So it's that an efficient algorithm taking m can't find such a number. OK!
	* ??? But what is the Jacobi symbol though?

What is the Jacobi symbol?
?
$\genfrac(){}{0}{x}{m}$ is a polynomial time computable function that evaluates to 1 or -1 and gives information on the residuosity of x in $\mathbb{Z}^*_m$
<!--SR:2022-06-30,17,210-->

If $\genfrac(){}{0}{x}{m} = -1$ . . . ?
?
$\mathcal{Q}_m(x) = 1$, i.e., x is non residue mod m
<!--SR:2022-06-27,22,170-->

If $\genfrac(){}{0}{x}{m} = 1$ . . . ?
?
Computing $\mathcal{Q}_m(x)$ is a hard problem.
<!--SR:2022-07-01,36,210-->

The algorithm for generating $x$ with $\mathcal{Q}_m(x) = 1$ and $\genfrac(){}{0}{x}{m} = 1$ . . . ?
?
Is not known to exist, efficiently.
<!--SR:2022-08-11,75,250-->

### zk QNR IP
#### Overview
* Asides on the nature of GMR's zk QNR IP
	* It only requires the verifier A to be a probabilistic polynomial time machine with the additional power to evaluate $\mathcal{Q}_m$
	* It only considers the case where $\genfrac(){}{0}{x}{m} = 1$, since the other case is uninteresting, since residuosity can be computed in polynomial time.
* The idea of GMR's zk QNR IP
	* B generates numbers $xr^2$ and $r^2$ with random r.
		* $r^2$ is called type 1
		* $xr^2$ is called type 2
	* If $y \in L$ then A can tell the types of these numbers
	* If $y \notin L$ then A cannot tell the types of the numbers and they'll fail the quizzes with high probability
* The zk part
	* A may release the quadratic residuosity of another $x \in \mathbb{Z}_m^*$ chosen by a cheating $B'$
	* We overcome this by having A make sure B "knows" the types of numbers it quizzes A about.

For which $x \in \mathbb{Z}_m^*$ is GMR's zk QNR IP defined?
?
$x \in QNR$ (since we're only interested in "yes instances") where $\genfrac(){}{0}{x}{m} = 1$ (since $\genfrac(){}{0}{x}{m} = -1$ directly implies $x$ is a quadratic non residue)
<!--SR:2022-06-28,34,210-->

How powerful does the A have to be in GMR's zk QNR IP?
?
It can just be probabilistic polynomial time turing machine with the additionalpower to compute $\mathcal{Q}_m$.
<!--SR:2022-07-12,55,250-->

What are type 1 numbers in GMR's zk QNR IP?
?
$r^2$ where $r \in \mathbb{Z}_m^*$ is randomly selected.
<!--SR:2022-08-01,68,250-->

What are type 2 numbers in GMR's zk QNR IP?
?
$y \cdot r^2$ where $r \in \mathbb{Z}_m^*$ is randomly selected.
<!--SR:2022-06-14,17,230-->

What is the basic (pre zk) idea of GMR's zk QNR IP?
?
B generates type 1 and 2 numbers.
If $y \in QNR$ A can tell the types of these numbers.
If $y \notin QNR$ A cannot tell the types of the numbers and A will fail the quizzes with high probability.
<!--SR:2022-06-28,18,130-->

What is the problem with the naive QNR IP?
?
$A$ may release the quadratic residuosity of another $x\in \mathbb{Z}_m^*$chosen by a cheating $B'$
<!--SR:2022-07-23,63,250-->

How (roughly) do we change the naive QNR IP to make it zero knowledge?
?
We have $A$ make sure $B$ "knows" the types of the numbers it quizzes $A$ about.
<!--SR:2022-07-09,53,250-->

What is the relationship between types and quadratic residuosity?
?
Type 1 numbers are always quadratic residues.
But type 2 numbers are quadratic residues if and only if $y$ is a quadratic residue.
<!--SR:2022-07-01,46,250-->

#### Protocol
##### Step 1

What is the input to the zk QNR IP?
?
$(y, m) \in \mathcal{L}$ such that $\genfrac(){}{0}{y}{m} = 1$ and $n = log_2m$
<!--SR:2022-06-22,30,210-->

What happens in step 1?
?
$B$ constrcuts $x$ and $T \cup S$ and sends both to $A$
<!--SR:2022-06-25,44,250-->

###### x

What is $x$ in the zk QNR IP?
?
The random residuosity number B quizzes A about.
<!--SR:2022-06-19,31,210-->

How is $x$ defined in the zk QNR IP?
?
In step 1, $B$ chooses a random $r_0$ from $\mathbb{Z}_m^*$ and then tosses a coin $C_x$.
If $C_x = 0$ then B sets $x = r_0^2 \mod n$,  else if $C_x = 1$, $B$ sets $x = y \cdot r^2 \mod n$
<!--SR:2022-07-09,43,230-->

If $C_x = 0$, what are $x$ and the type of $x$?
?
$x = r_0^2 \mod n$
Type 1
<!--SR:2022-08-06,60,230-->

If $C_x = 0$, what are $x$ and the type of $x$?
?
$x = r_0^2 \mod n$
$x$ is of  type 1
<!--SR:2022-06-23,42,250-->

If $C_x = 1$, what are $x$ and the type of $x$?
?
$x = y \cdot r_0^2 \mod n$
$x$ is of  type 2
<!--SR:2022-06-29,44,250-->

###### T and S

What is $T \cup S$ for?
?
The set of random numbers used to convince $A$ that $B$ knows the residuosity of $x$ without revealing it.
<!--SR:2022-06-18,15,210-->

What is the size of $T \cup S$?
?
$2n$, since $T$ and $S$ both have size $n$.
<!--SR:2022-07-05,50,250-->

How is $T$ constructed?
?
$T = \{t_1, ..., t_n\ |\ t_i = r_i^2\}$
<!--SR:2022-06-21,40,250-->

How is $S$ constructed?
?
$S = \{t_{n+1},...,t_{2n}\ |\ t_i = y\cdot r_i^2\}$
<!--SR:2022-06-18,38,250-->


What type are each $t_i$?
?
Type 1
<!--SR:2022-07-19,48,230-->

What type are each $s_i$?
?
Type 2
<!--SR:2022-06-20,40,250-->

How does $B$ send $T$ and $S$ to $A$?
?
As $T \cup S$ in a random order.
<!--SR:2022-07-02,47,250-->

##### Step 2

What happens in step 2?
?
$A$ constructs $Z$ and sends it to $B$.
<!--SR:2022-06-24,43,250-->

What is $Z$ for?
?
Requiring $B$ to prove it knows the type 1 and type 2 roots of each $t_i \in T \cup S$.
<!--SR:2022-08-05,60,230-->

How is $Z$ constructed?
?
$A$ randomly selects a subset of $T \cup S$ of size $n$
<!--SR:2022-06-23,15,150-->

How large is $Z$?
?
$n$
<!--SR:2022-06-19,39,250-->

How does $A$ send $Z$ to $B$?
?
However it pleases - no restriction.
<!--SR:2022-06-17,37,230-->

??? why is $x$ chosen $mod\ n$ rather than $mod\ m$?

##### Step 3

What happens in step 3?
?
B reveals the random $r$ values in $Z$.
B makes equally sized sets of opposite secret residuosity $X$ and $Y$.
B reveals the random values left over.
B ties $X$ and $Y$ to  the residuosity of $x$ with sets $X'$ and $Y'$.
B sends $X' \cup Y'$ to A.
<!--SR:2022-07-08,35,190-->

How does B reveal the random $r$ values in $Z$?
?
For each $z \in Z$ $B$ sends to $A$ some $r$ such that $z = r^2 \mod m$ or $z = y \cdot r^2 \mod m$
<!--SR:2022-07-27,49,230-->

What is $d$?
?
The difference in size between $T - Z$ and $S - Z$.
<!--SR:2022-06-30,35,230-->

What set does $B$ reveal other than $Z$, and how is it created?
?
$D$. A set randomly chosen by $B$ with $d$ elements from the larger set of $T - Z$ or $S -Z$.
<!--SR:2022-06-24,31,210-->

How is $D$ notated?
?
$\{t_{i_1},...,t_{i_d}\}$.
<!--SR:2022-06-14,19,190-->

How does $B$ reveal $D$?
?
$B$ sends $r_{i_1},...,r_{i_d}$,  where $t_{i_j} = r_{i_j}^2$ or $t_{i_j} = y \cdot r_{i_j}^2 \mod m$ for some $1 \leq i_j \leq 2n$.
<!--SR:2022-07-04,32,190-->

How is $X$ defined?
?
$T - Z - D$
<!--SR:2022-07-15,47,250-->

How is $Y$ defined?
?
$S - Z - D$
<!--SR:2022-06-23,26,190-->

What is the purpose of $X' \cup Y'$?
?
Tying the residuosity of $x$ to that of each $t_i$, such that $B'$ "knows" $\sqrt{x}$. That is, so that a simulator $M$ can calculate $\sqrt{x}$ using $B'$.
<!--SR:2022-06-17,19,150-->

If $x$ is type 1, how do we form $\sqrt{x \cdot t_i}$?
?
Let $t_i \in X$, then $\sqrt{x \cdot t_i} = \sqrt{r_0^2 \cdot r_i^2} = r_0 \cdot r_i$
<!--SR:2022-07-04,22,170-->

If $x$ is type 1, how do we form $\sqrt{y \cdot x \cdot t_i}$?
?
Let $t_i \in Y$, then $\sqrt{y \cdot x \cdot t_i} = \sqrt{y \cdot r_0^2 \cdot y \cdot r_i^2} = \sqrt{y^2 \cdot r_0 ^2 \cdot r_i^2} = y \cdot r_0 \cdot r_i$
<!--SR:2022-06-21,12,210-->

If $x$ is type 2, how do we form $\sqrt{y \cdot x \cdot t_i}$?
?
Let $t_i \in X$, then $\sqrt{y \cdot x \cdot t_i} = \sqrt{y \cdot y \cdot r_0^2 \cdot r_i^2} = \sqrt{y^2 \cdot r_0^2 \cdot r_i^2} = y \cdot r_0 \cdot r_i$
<!--SR:2022-06-19,9,190-->

If $x$ is type 2, how do we form $\sqrt{x \cdot t_i}$?
?
Let $t_i \in Y$, then $\sqrt{x \cdot t_i} = \sqrt{y \cdot r_0^2 \cdot y \cdot r_i^2} = \sqrt{y^2 \cdot r_0^2 \cdot r_i^2} = y \cdot r_0 \cdot r_i$
<!--SR:2022-07-04,37,230-->

What are the two forms of numbers in $X' \cup Y'$?
?
$\sqrt{y \cdot x \cdot t_i}$ and $\sqrt{x \cdot t_i}$
<!--SR:2022-06-29,35,230-->

How is $X' \cup Y'$ defined?
?
If $x = r^2_0 \mod m$:
$X' = \{r_0 \cdot r_i = \sqrt{x \cdot t_i} \mod n\ |\ t_i \in X\}$ 
$Y' = \{y \cdot r_0 \cdot r_i = \sqrt{y \cdot x \cdot t_i} \mod n\ |\ t_i \in Y\}$ 
else:
$X' = \{y \cdot r_0 \cdot r_i = \sqrt{y \cdot x \cdot t_i} \mod n\ |\ t_i \in X\}$ 
$X' = \{y \cdot r_0 \cdot r_i = \sqrt{x \cdot t_i} \mod n\ |\ t_i \in Y\}$
<!--SR:2022-07-20,49,230--> 

??? why $\mod n$ rather than $\mod m$???

How is $X' \cup Y'$ sent?
?
$B$ sends $X' \cup Y'$ to $A$ in a random order.
<!--SR:2022-06-22,32,250-->
<!--SR:2022-05-05,2,230-->

##### Step 4

What happens in step 4?
?
$A$ checks the form and size of $X' \cup Y'$. If those are invalid halts and rejects, otherwise, $A$ computes and sends $\mathbb{Q}_m(x)$.
<!--SR:2022-06-16,27,230-->

What is $v$?
?
$\mathbb{Q}_m(x)$ calculated by $A$
<!--SR:2022-08-07,56,230-->

What should $|X' \cup Y'|$ be?
?
$|X' \cup Y'| \gt \frac{n}{3}$
<!--SR:2022-06-14,25,230--> 

What form should the values in $X' \cup Y'$  be?
?
$\forall w \in X' \cup Y', w^2 = t_i \cdot x \mod m\ \lor\ w^2 = y \cdot t_i \cdot x \mod m$ for some $t_i \in X \cup Y$
<!--SR:2022-06-15,11,210-->

How is $X' \cup Y'$ sent?
?
$B$ sends $X' \cup Y'$ to $A$ in a random order.
<!--SR:2022-06-22,32,250-->

??? why does it matter that $X' \cup Y'$ is sent in a random order?

##### Step 5

What happens in step 5?
?
$B$ checks $v$, halts if it detects cheating, updates $iteration$, accepts if finished, or starts again at step 1.
<!--SR:2022-06-17,28,230-->

How does $B$ check $v$?
?
$B$ checks that $v = C_x$, i.e., that $A$ has predicted the coin flip.
<!--SR:2022-06-14,26,230-->

When does $B$ accept?
?
If $iteration \geq n$
<!--SR:2022-06-27,36,250-->

When does $B$ increment $iteration$?
?
After checking $v$
<!--SR:2022-08-01,52,230-->

What does $B$ do if $iteration \lt n$?
?
Goes back to step 1.
<!--SR:2022-08-10,58,230-->
#### It is a Proof System
##### Remark 2
###### Working it out
??? Do I have my ideas on why remark 2 is correct right?
First I transform the probability that we halt into a geometric picture.
Then I transform the marble choosing into a permutation problem.
Then I roughly calculate that the probability is factorial in N.

Here is an image roughly showing that $X' \cup Y' = n/3 \implies d = 2n/3$. Then we just do a mental transformation in our mind and imagine $Z$ as the first half of the string, composed of $5n/6$ from $S$ and $n/6$ from $T$.

Thus we see that our probability of halting is equivalent to picking n marbles from a bag of n yellow marbles and n red marbles (S and T), and finding that we have only n/6 or less of one colour.
![[279212529_746449463187274_2038915978639506292_n 1.jpg]]

If we pick a random permutation of a string containing n As and n Bs, what’s the chance that the first half of the string contains $\leq n/6$ of one letter?

I believe there are $(2n)!/2(n!)$ permutations of the string. $2n!$ for permutations of $n$ distinct characters, divided by $n!$ for the permutations of each identical character.

But how many of those have at most n/6 of one letter? Let’s consider the ones that have exactly $n/6$ As. There are $n!/(5n/6)!(n/6)!$ ways to arrange the first half of the string, and and equal number for the second, giving $(n!/(5n/6)!(n/6)!)^2$. Then we consider the case where there are fewer than $n/6$ As. The amount becomes $\sum_{i=0}^{n/6} n!/i!(n-i)!$, then we just double it for the case where we have fewer Bs, giving $2\sum_{i=0}^{n/6} n!/i!(n-i)!$

GMR's claim is that the program halts with probability $\lt \frac{1}{2^{cn}}$ for $0 \lt c \leq 1$. Well, this seems like it's probably true if the probability is 1 over some factorial. Then we just that $(2n)!/2(n!)$ is greater than $2\sum_{i=0}^{n/6} n!/i!(n-i)!$ by some factorial factor. Well, $2\sum_{i=0}^{n/6} n!/i!(n-i)! <= (n+2)!/2(n/2)!$ since the multiplication by 2 is way less than an extra value in the factorial, and the sum is equivalent to multiplying by $n/6$ which is less than an extra factorial. But now we see that $(n+2)!/2(n/2)!$ is factorially larger than $(2n)!/2(n!)$ for some n by virtue of a much higher value in the numerator. Hence it's at least exponentially bigger, proving GMR's proposition (roughly at least). This seems like a lot of work to show an offhanded remark, especially one that can probably been seen quite intuitively. But it is what it is.

###### Scrapped

Scrapping a bunch of detailed cards because they don't really matter for the overall understanding of GMR.

What are the relevant facts for calculating the sizes of $X$ and $Y$ if we halt given honest $A$ and $B$?
%%%%?
$|X' \cup Y'| = n - d$
We halt if $|X' \cup Y'| \leq n/3$
$|X| - |Y| = d$
$|X| + |Y| = n$

How do we know that $|X' \cup Y'| = n - d$?
%%%%?
It's made of two $n$ size sets, with sets of size $n$ and $d$ taken away.

$|X| - |Y| = ...$? How do we know?
?%%%%
$d$ by the definition of $d$.

$|X| + |Y| = ...$? How do we know?
?%%%%
??? this seems wrong, isn't it $n-d$?
$n$
Since $|X| + |Y| = |T| + |S| - |Z|$ where $|T| = |S| = |Z| = n$

How large are sets $X$ and $Y$ if we halt and reject for honest $A$ and $B$ and how do we know?
%%%%?
$\leq n/6$ and $\geq 5n/6$.
$|X' \cup Y'| = n - d \implies n - d \leq n/3 \implies d \geq 2n/3$ 
Assume $|X| \gt |Y|$ wlog
$|X| - |Y| \geq 2n/3$
Therefore $|X| \geq 2n/3 + |Y| = 2n/3 + n - |X| = 5n/3 \implies |X| \geq = 5n/6$

What is the probability of choosing $Z$ such that an honest ITM halts? How do we know? Assume $|X|$ and $|Y|$ boundaries are known.
%%%%?
$[2\sum_{i=0}^{n/6} n!/i!(n-i)!]/[(2n)!/2(n!)]$
The total ways of chosing $Z$ is equivalent to the permutations of a $2n$ length string with $n$ $A$ characters and $n$ $B$ characters, i.e., $(2n)!/2(n!)$.
Assume $|X|\ or\ |Y| \leq n/6$.
The ways where exactly $n/6$ of the first $n$ are A is $n!/(n/6)!(5n/6)!$.
The ways where at most $n/6$ of the first $n$ are A is $2\sum_{i=0}^{n/6} n!/i!(n-i)!$.
The ways where at most $n/6$ of the first $n$ are one letter is $2\sum_{i=0}^{n/6} n!/i!(n-i)!$.

How do we show that the exact probability that we halt for an honest ITM is less than GMR's upper bound?
asdf?
$P = Q/R$ where $Q = 2\sum_{i=0}^{n/6} n!/i!(n-i)!$ and $R =(2n)!/2(n!)$
$Q < (n+2)!/2(n/2)!$ so $O(P) = 1/n! \implies \Omega(P) = 1/2^{cn}$


###### Questions

What is remark 2?
?
If $A$ and $B$ both operate according to the specification, then each iteration of the program will be completed with probability $> 1 - 1/2^{cn}$ for some $0 < c \leq 1$
<!--SR:2022-06-23,16,190-->

What are my steps for proving the upper bound for the chance that we halt and reject if $A$ and $B$ are honest?
?
Show that $X$ or $Y \leq n/6$ if we halt. 
Show the chance of that is some factorial expression using a string permutation argument.
Show that chance is less than the bound given by GMR.
<!--SR:2022-06-16,28,250-->

Based on what condition might we halt given honest $A$ and $B$?
?
If $|X' \cup Y'| \leq n/3$
<!--SR:2022-06-15,27,250-->

If $A$ and $B$ behave well, what is a useful lower bound for the chance that any given iteration will complete?
?
$1 - \frac{1}{2^{cn}}$ for $0 < c \leq 1$
<!--SR:2022-06-23,33,250-->

##### Claim 1

What is claim 1?
?
If $(y, m) \notin QNR$ then $A$ (or any $A'$) correctly guessed $C_x$ with probability exactly $1/2$
<!--SR:2022-07-05,31,190-->

How does the proof for claim 1 work?
?
$P[C_x = 0] = 1/2$, and even with infinite computation power $A'$ can't tell the two types in $X' \cup Y'$ apart since they're all random square roots of random squares. We run through all 4 cases of $C_x$ and $w$ showing that they're random square roots of random squares.
<!--SR:2022-07-13,41,230-->

What cases do we have to prove to show that all $w \in X' \cup Y'$ are random square roots of random squares if $(y, m) \notin QNR$?
?
$C_x = 0$ and $w \in X'$
$C_x = 0$ and $w \in Y'$
$C_x = 1$ and $w \in X'$
$C_x = 1$ and $w \in Y'$
<!--SR:2022-06-23,33,250-->

How do we show $w \in X'$ is a random square root of a random square if $C_x = 0$ and $(y, m) \notin QNR$?
?
$w = r_0r_i = \sqrt{t_ix} = \sqrt{r_0^2r_i^2}$
<!--SR:2022-07-15,42,230-->

How do we show $w \in Y'$ is a random square root of a random square if $C_x = 0$ and $(y, m) \notin QNR$?
asdf

How do we show $w \in X'$ is a random square root of a random square if $C_x = 1$ and $(y, m) \notin QNR$?
asdf

How do we show $w \in Y'$ is a random square root of a random square if $C_x = 1$ and $(y, m) \notin QNR$?
asdf

Why is important to show that $w$ is a random square root of a random square, not just a random square root?
asdf

##### Theorem 1

What is claim 2?
asdf

How do we know claim 2 is true?
asdf

What is theorem 1?
asdf

#### It is Zero Knowledge
The crux of the proof is we have $B$ prove that it gives some information on each $t_i$, and that infromation is of one of two types. If we only give one piece of knowledge for each $t_i$ there is no way to calculate $\mathbb{Q}_m(x)$. However, if we have both pieces of information we can calculate $mathbb{Q}_m(x)$. We can get both pieces by having the simulator run $B$ twice, and choose different values for $Z$.

In particular, we have some $r_i$ such that $r_i^2 = x$ and some $w$ where $w = \sqrt{xt_i}$ or $w = \sqrt{xt_iy}$. Using basic algebra we can calculate that $r_0 = \frac{w}{r_i}$ or $r_0 = \frac{w}{y \cdot r_i}$. We can then check which case is true by verifying that $r_0^2 = x$ or $y \cdot r_0^2 = x$.

We only have to run the machine $B'$ twice, since there's a very good (exponentially good) chance that there is some overlap, and we only need to run the above calculation for each pair of $r_i$ and $w$, which only takes $O(n^2)$ steps.

## What it means to know
There is an stronger notion of knowledge complexity where $B'$ is not bounded, but the simulator has access to $B'$'s random tape and can communicate with $B'$.

This means that when analysing a machine with some additional power other than polynomial computations, that we don't accidentally think it can only compute with polynomial power.

## Oblivious Transfer

Oblivious transfer is a protocol by Rabin where you transfer some knowledge (about the factorisation of a prime) with 50% chance, but never know if you transfered it. Apparently that's useful, for some reason. The original paper didn't prove correctness wrt a complexity framework, and it's perfectly possible that some adversarial algorithm exists that can learn the factorisation with a higher probability.

An altered version of the OT protocol can be proven valid (given the intractability assumption) using ideas similar to the QNR ZKP, i.e., proving knowledge of the root of a value before an adversary uses it.

Thus a sub protocol (OT) is proven correct in a modular fashion, making it easier to construct larger protocols.s outputs, since all $w \in X' \cup Y'$ are random squares roots of random squares, and $x$ is a random square.
<!--SR:2022-05-09,4,250-->

What cases do we have to prove to show that all $w \in X' \cup Y'$ are random square roots of random squares if $(y, m) \notin QNR$?
?
$C_x = 0$ and $w \in X'$
$C_x = 0$ and $w \in Y'$
$C_x = 1$ and $w \in X'$
$C_x = 1$ and $w \in Y'$
<!--SR:2022-06-23,33,250-->

How do we show $w \in X'$ is a random square root of a random square if $C_x = 0$ and $(y, m) \notin QNR$?
?
$w = r_0r_i = \sqrt{t_ix} = \sqrt{r_0^2r_i^2}$
<!--SR:2022-07-15,42,230-->

How do we show $w \in Y'$ is a random square root of a random square if $C_x = 0$ and $(y, m) \notin QNR$?
asdf

How do we show $w \in X'$ is a random square root of a random square if $C_x = 1$ and $(y, m) \notin QNR$?
asdf

How do we show $w \in Y'$ is a random square root of a random square if $C_x = 1$ and $(y, m) \notin QNR$?
asdf

Why is important to show that $w$ is a random square root of a random square, not just a random square root?
asdf

##### Theorem 1

What is claim 2?
asdf

How do we know claim 2 is true?
asdf

What is theorem 1?
asdf

#### It is Zero Knowledge
The crux of the proof is we have $B$ prove that it gives some information on each $t_i$, and that infromation is of one of two types. If we only give one piece of knowledge for each $t_i$ there is no way to calculate $\mathbb{Q}_m(x)$. However, if we have both pieces of information we can calculate $mathbb{Q}_m(x)$. We can get both pieces by having the simulator run $B$ twice, and choose different values for $Z$.

In particular, we have some $r_i$ such that $r_i^2 = x$ and some $w$ where $w = \sqrt{xt_i}$ or $w = \sqrt{xt_iy}$. Using basic algebra we can calculate that $r_0 = \frac{w}{r_i}$ or $r_0 = \frac{w}{y \cdot r_i}$. We can then check which case is true by verifying that $r_0^2 = x$ or $y \cdot r_0^2 = x$.

We only have to run the machine $B'$ twice, since there's a very good (exponentially good) chance that there is some overlap, and we only need to run the above calculation for each pair of $r_i$ and $w$, which only takes $O(n^2)$ steps.

## What it means to know
There is an stronger notion of knowledge complexity where $B'$ is not bounded, but the simulator has access to $B'$'s random tape and can communicate with $B'$.

This means that when analysing a machine with some additional power other than polynomial computations, that we don't accidentally think it can only compute with polynomial power.

## Oblivious Transfer

Oblivious transfer is a protocol by Rabin where you transfer some knowledge (about the factorisation of a prime) with 50% chance, but never know if you transfered it. Apparently that's useful, for some reason. The original paper didn't prove correctness wrt a complexity framework, and it's perfectly possible that some adversarial algorithm exists that can learn the factorisation with a higher probability.

An altered version of the OT protocol can be proven valid (given the intractability assumption) using ideas similar to the QNR ZKP, i.e., proving knowledge of the root of a value before an adversary uses it.

Thus a sub protocol (OT) is proven correct in a modular fashion, making it easier to construct larger protocols.