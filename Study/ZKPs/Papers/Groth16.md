#flashcards/zkps/Groth16
# Abstract

What makes SNARGs succinct?
?
Small size and low verification complexity.
<!--SR:2022-11-15,118,230-->

What is a SNARG?
?
Succinct non-interactive argument
<!--SR:2023-01-21,176,270-->

What is a SNARK?
?
Succinct non-interactive argument of knowledge
<!--SR:2022-09-18,83,250-->

What does a pairing based SNARG consist of?
?
A number of group elements.
<!--SR:2022-09-21,85,250-->

What is the central question of Groth16?
?
How efficient can pairing based SNARGs be?
<!--SR:2022-10-19,94,230-->

What language is Groth16's SNARG for, and what is that language's most important property?
?
Circuit satisfiability, that it is NP-complete.
<!--SR:2022-12-13,131,250-->

What kind of pairings does Groth16 use and why?
?
Assymetric pairings for higher efficiency.
<!--SR:2023-03-18,211,270-->

What does a Groth16 SNARG consist of?
?
3 group elements.
<!--SR:2023-02-25,200,270-->

What does verifying a Groth16 SNARG require?
?
Checking a single pairing product equation using 3 pairings in total.
<!--SR:2022-11-05,57,150-->

What is the knowledge complexity of the Groth16 SNARG?
?
It is zero knowledge.
<!--SR:2023-02-19,163,230-->

What is the second contribution of Groth16 and how is it shown?
?
That SNARGs using generic symmetric bilinear group operations can't consist of a single element.
By showing that linear interactive proofs cannot have a linear decision procedure.
<!--SR:2022-12-01,109,210-->

What would extending the lower bound in Groth16 prove?
?
Extending the lower bound to 2 elements would prove the optimality of the 3 element SNARG.
<!--SR:2023-02-28,180,250-->

??? How do we know that the lower bound actually applies - is a LIP really the only information theoretic model that could yield pairing based SNARKs?

Who posed the question answered by Groth16's second contribution?
?
Nir Bitansky, Allesandro Chisea, Yuval Ishai, Rafail Ostrovsky, and Omer Paneth.
<!--SR:2022-10-19,76,170-->

# Introduction

## Prior Work

Who introduced zero-knowledge proofs?
?
Shafi Goldwasser, Silvio Micali, and Charles Rackoff.
<!--SR:2022-09-28,93,270-->

What are the 3 core properties of zero knowledge proofs?
?
Completeness, Soundness, and Zero-Knowledge.
<!--SR:2022-10-23,103,250-->

Describe the completeness property.
?
Given a statement and a witness, the prover can convince the verifier.
<!--SR:2022-11-27,115,210-->

Describe the soundness property.
?
A malicious prover cannot convince the verifier of a false statement.
<!--SR:2022-10-18,98,250-->

Describe the zero knowledge property.
?
The proof does not reveal anything but the truth of the statement, in particular it does not reveal the prover's witness.
<!--SR:2022-10-21,77,190-->

How did Blum, Feldman, and Micali extend the notion of interactive proofs?
?
To non-interactive zero knowledge proofs (NIZK) in the common reference string model.
<!--SR:2023-02-11,167,250-->

Where are NIZKs useful, according to Groth16?
?
The construction of non-interactive cryptographic schemes, e.g., digital key signatures, and CCA-secure public key encryption.
<!--SR:2022-10-31,78,190-->

Where was the first sub-linear communication zero-knowledge argument, sending fewer bits than the size of the statement given?
?
Kili92, by Joe Kilian.
<!--SR:2022-12-07,101,190-->

What did Micali00 propose?
?
Sublinear size NIZK arguments by letting the prover in a communication efficient zero-knowledge argument compute the verifier's challenges using a cryptographic function.
<!--SR:2022-10-15,57,150-->

Which papers introduced pairing based NIZKs, and what did this yield?
?
Groth et al: GOS12, GOS06, Gro06, GS12.
The first linear sized proofs based on standard assumptions.
<!--SR:2022-10-07,23,130-->

What did Gro10 achieve wrt communication complexity and how?
?
The first constant size NIZK arguments, by combining pairing based NIZKs with ideas from interactive zero-knowledge.
<!--SR:2022-09-27,54,190-->

What did Lip12 achieve wrt communication complexity?
?
Constant size NIZK arguments based on progression-free sets to reduce the size of the common reference string.
<!--SR:2022-10-28,57,170-->

What is Groth's constant size NIZK based on?
?
Constructing a set of polynomial equations and using pairings to efficiently verify these equations.
<!--SR:2022-10-18,35,170-->

UNFINISHED

## Our Contribution

UNFINISHED

# Preliminaries
## Notation

What does $\approx$ mean, roughly?
?
That two functions approach each other exponentially.
<!--SR:2022-12-21,121,250-->

??? Wait, is this right? It appears to only mean that they approach each other polynomially.

What is the definition of $\approx$?
?
Given two function $f, g : \mathbb{N} \rightarrow [0,1]$, we write $f(\lambda) \approx g(\lambda)$ when $| f(\lambda) - g(\lambda)| = \lambda^{-\omega(1)}$
<!--SR:2022-09-17,6,150-->

What is the limit definition of $\omega$?
?
$f(n) = \omega(g(n)) \iff lim_{n \rightarrow \infty} |f(n)|/g(n) = \infty$
<!--SR:2022-12-13,110,250-->

What is the formal definition of $\omega$?
?
$\forall k > 0\ \exists n_0 \forall n > n_0 : f(n) > k \cdot g(n)$
<!--SR:2022-12-14,99,230-->

What does $\lambda$ represent, and what do its values mean?
?
$\lambda$ is the security parameter, and as it grows we want higher security.
<!--SR:2022-12-10,123,270-->

What does $y = A(x;r)$ mean?
?
That the algorithm $A$ outputs $y$ on the input $x$ with randomness $r$.
<!--SR:2022-10-04,78,270-->

What does $y \leftarrow A(x)$ mean?
?
We pick randomness $r$ at random and set $y = A(x;r)$.
<!--SR:2022-10-17,88,270-->

What does $y \leftarrow S$ mean?
?
We pick $y$ uniformly at random from set $S$.
<!--SR:2022-11-28,111,250-->

What do we assume about random sampling?
?
That it's possible to randomly sample from sets such as $\mathbb{Z}_p$
<!--SR:2022-12-27,127,250-->

What does $(y;z) \leftarrow (\mathcal{A} || X_{\mathcal{A}})(x)$ mean?
?
$\mathcal{A}$ outputs $y$ on input $x$ and $X_{\mathcal{A}}$ outputs $z$ on the same input (including random coins).
<!--SR:2023-01-03,124,250-->

## Bilinear Groups

What are the parts of a bilinear group?
?
$(p, \mathbb{G}_1, \mathbb{G}_2, \mathbb{G}_T, e)$
<!--SR:2022-11-08,54,230-->

What is $p$?
?
A prime number.
<!--SR:2022-12-19,115,250-->

What are $\mathbb{G}_1, \mathbb{G}_2, \mathbb{G}_T$
?
Groups of prime order $p$.
<!--SR:2022-12-22,132,270-->

What is $e$ and what is its definition?
?
$e : \mathbb{G}_1 \times \mathbb{G}_2 \rightarrow \mathbb{G}_T$ is a bilinear map, i.e., $e(U^a, V^b) = e(U, V)^{ab}$
<!--SR:2022-11-29,117,270-->

What is a property of generators of our bilinear group?
?
if $G$ is a generator of $\mathbb{G}_1$ and $H$ is a generator of $\mathbb{G}_2$ then $e(G, H)$ is a generator of $\mathbb{G}_T$.
<!--SR:2022-10-04,55,250-->

What are the generic bilinear group operations?
?
Group operations for the groups.
Evaluating the bilinear map.
Deciding the equality of group elements.
Sampling generators of the groups.
<!--SR:2022-12-06,124,270-->

What do we assume about the bilinear group operations?
?
That there are efficient algorithms for computing them.
<!--SR:2022-12-04,122,270-->

What are the names for the types of bilinear groups?
?
Type I, Type II, and Type III
<!--SR:2022-11-30,118,270-->

Who classified the types of bilinear groups?
?
Galbraith et al GPS08
<!--SR:2022-09-22,46,190-->

What is a Type I bilinear group?
?
Where $\mathbb{G}_1 = \mathbb{G}_2$
<!--SR:2022-12-03,121,270-->

What are Type II bilinear groups?
?
Where $\mathbb{G}_1 \neq \mathbb{G}_2$ and there is an efficiently computable non-trivial homomorphism $\psi : \mathbb{G}_1 \rightarrow \mathbb{G}_2$
<!--SR:2022-10-02,69,250-->

What are Type III bilinear groups?
?
Where there is no efficiently computable non-trivial homomorphism in either direction between $\mathbb{G}_1$ and $\mathbb{G}_2$.
<!--SR:2023-01-02,137,250-->

What is special about Type III bilinear groups?
?
They are the most efficient type of bilinear groups, and hence the most relevant for practical applications.
<!--SR:2022-10-12,84,270-->

For which type of bilinear group is the lower bound given?
?
Type III
<!--SR:2022-12-23,118,250-->

For which type of bilinear group does the construction work?
?
All 3 types
<!--SR:2022-11-20,89,230-->

## Non-interactive Zero-Knowledge Arguments of Knowledge

### Algorithms

What is $\mathcal{R}$?
?
A relation generator that, given $\lambda$ in unary returns a polynomial time decidable binary relation $R$.
<!--SR:2022-09-25,65,250-->

??? Why is lambda in unary?

What is $\phi$?
?
The statement.
<!--SR:2022-10-10,75,250-->

What is $w$?
?
The witness.
<!--SR:2022-12-22,118,250-->

What kinds of pairs are in $R$?
?
$(\phi, w)$, i.e., statement and witness
<!--SR:2022-12-01,119,270-->

What is $\mathcal{R}_\lambda$?
?
The set of possible relations $\mathcal{R}$ might output given $1^\lambda$.
<!--SR:2022-11-18,111,270-->

What is $z$?
?
Auxilliary information that the relation generator might output, which will be given to the adversary.
<!--SR:2022-12-31,117,230-->

What is an efficient prover publicly verifiable non-interactive argument for $\mathcal{R}$?
?
A quadruple of polynomial time algorithms $(\textbf{Setup, Prove, Vfy, Sim})$
<!--SR:2022-10-26,69,210-->

What is the definition of $\textbf{Setup}$?
?
$(\sigma, \tau) \leftarrow \textbf{Setup}(R)$
The setup takes as input the security paramater $\lambda$ and a relation $R \in R_\lambda$ and returns a common reference string $\sigma$ and a simulation trapdoor $\tau$ for the relation $R$.
<!--SR:2022-10-26,95,270-->

??? why don't we write the setup as explicitly taking the security parameter?

What is the definition of $\textbf{Prove}$?
?
$\pi \leftarrow\textbf{Prove}(R, \sigma, \phi, w)$
The prover algorithm takes as input the common reference string and $(\phi, w) \in R$ and outputs the argument $\pi$.
<!--SR:2022-12-07,125,270-->

??? Why do we say the prover algorithm accepts the relation?

What is $\sigma$?
?
The common reference string.
<!--SR:2022-12-05,123,270-->

What is $\tau$?
?
The simulation trapdoor.
<!--SR:2022-10-30,97,270-->

What is $tau$ used for?
?
The simulator gets access to $tau$ so it can generate proofs indistinguishable from actual proofs, so that we can prove that an argument is zero knowledge.
<!--SR:2022-10-05,70,250-->

What is $\pi$?
?
The argument.
<!--SR:2022-11-15,95,250-->

What is the definition of $\textbf{Vfy}$?
?
$0/1 \leftarrow \textbf{Vfy}(R, \sigma, \phi, \pi)$
The verification algorithm takes as input the common reference string, the statement, and the argument, and returns 0 (reject) or 1 (accept).
<!--SR:2022-12-08,105,250-->

What is the definition of $\textbf{Sim}$?
?
$\pi \leftarrow \textbf{Sim}(R, \tau, \phi)$
The simulator takes as input a simulation trapdoor and statement $\phi$, and outputs an argument.
<!--SR:2022-11-17,90,210-->

??? Why does the simulator not get the common reference string? Is it because it's efficiently computable from the trapdoor?

### Properties

What is a non-interactive argument?
?
We say $(\textbf{Setup, Prove, Vfy)}$ is a non-interactive argument for $\mathcal{R}$ if it has perfect completeness and computational soundness.
<!--SR:2022-10-20,48,230-->

What is a perfect non-interactive zero-knowledge argument of knowledge?
?
We say that $(\textbf{Setup, Prove, Vfy, Sim})$ is a perfect non-interactive zero-knowledge argument of knowledge for $\mathcal{R}$ if it has perfect completeness, perfect zero knowledge, and computational knowledge soundness.
<!--SR:2022-12-10,128,270-->

What is perfect completeness, roughly?
?
Completeness says that, given any true statement, an honest prover should be able to convince an honest verifier.
<!--SR:2022-12-21,115,250-->

What is the definition of perfect completeness?
?
For all $\lambda \in \mathbb{N}, R \in \mathcal{R}_\lambda, (\phi, w) \in R$:
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R);$
$\pi \leftarrow \textbf{Prove}(R, \sigma, \phi, w):$
$\textbf{Vft}(R, \sigma, \phi, \pi) = 1] = 1$
<!--SR:2022-12-04,108,230-->

What is perfect zero knowledge, roughly?
?
An argument is zero knowledge if it does not leak any information besides the truth of the statement.
<!--SR:2022-11-15,109,270-->

What is the definition of perfect zero-knowledge?
?
We say $(\textbf{Setup, Prove, Vfy, Sim})$ is a perfect zero-knowledge if for all $\lambda \in \mathbb{N}, (R, z) \leftarrow \mathcal{R}(1^\lambda), (\phi, w) \in R$ and adversaries $\mathcal{A}$:
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R); \pi \leftarrow \textbf{Prove}(R, \sigma, \phi, w): \mathcal{A}(R, z, \sigma, \tau, \pi) = 1] =$
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R); \pi \leftarrow \textbf{Sim}(R, \tau, \phi) : \mathcal{A}(R, z, \sigma, \tau, \pi) = 1]$
<!--SR:2022-09-23,42,190-->

??? Why does the adversary not get phi as well? Does that represent a weakening of the definition? Is it because phi can somehow be inferred from the other arguments? Is it because the same phi is being given to both the simulator and the prover?

??? Why does the definition of perfect zero-knowledge not include the relation generation in the probability expressions? Whereas it does in the definitions of soundness. Would it make a difference here?

What does the adversary represent in the definition of perfect zero knowledge?
?
A malicious verifier trying to learn extra information from the proof.
<!--SR:2022-10-29,96,270-->

What does the adversary in the definition of perfect zero knowledge do?
?
Tries to distinguish between the proof from prover and the proof from simulator.
<!--SR:2022-10-16,87,270-->

What inputs does the adversary in the definition of perfect zero knowledge get?
?
The relation, the auxillary output from the relation generator, the common reference string, the simulation trapdoor and the proof (from either the prover or the simulator).
$R, z, \sigma, \tau, \pi$
<!--SR:2022-09-26,17,150-->

??? Why does this adversary get so much information including z and tau?

??? Why does this adversary not get the statement? Does this mean that possibly with the statement they'd be able to deduce some knowledge?

What is computational soundness, roughly?
?
We say a set of algorithms is sound if it is not possible to prove a false statement, i.e., convince the verifier if no witness exists.
<!--SR:2022-10-14,78,250-->

What is the definition of computational soundness?
?
Let $L_R$ be the language consisting of statements for which there exist matching witnesses in R. Formally, we require that for all non-uniform polynomial time adversaries $\mathcal{A}$:
$Pr[(R,z) \leftarrow \mathcal{R}(1^\lambda); (\sigma, \tau) \leftarrow \textbf{Setup}(R); (\phi, \pi) \leftarrow \mathcal{A}(R, z, \sigma) : \phi \notin L_R \land \textbf{Vfy}(R, \sigma, \phi, \pi) = 1] \approx 0$
<!--SR:2023-01-04,135,250-->

What does the adversary represent in the definition of computational soundness?
?
A malicious prover trying to find a proof and statement that the verifier will accept where the statement has no possible witness.
<!--SR:2022-11-02,90,230-->

What inputs does the adversary in the definition of computational soundness accept?
?
The relation, the auxilary input, and the common reference string.
$(R, z, \sigma)$
<!--SR:2022-10-22,92,270-->

??? Why does it not also accept the simulation trapdoor? Is it because then it could create any proof it likes.

??? Why does it have the auxilary input? What's the point of the auxilary input, in fact?

What is computational knowledge soundness, roughly?
?
A strengthening of the notion of soundness, where there is an extractor that can compute a witness whenver an adversary produces a valid argument.
<!--SR:2022-11-07,102,270-->

??? Why does the extractor in the definition for computational knowledge soundness not need the simulation trapdoor?

??? Why does the adversary in the definition for computational knowledge soundness need the auxillary information?

??? Does the definition of computational knowledge soundness imply that any valid prover also has their witness extracted? How can this be compatible with zero knowledge? Is this because we don't actually have access to any adversary's random coins? 

What does the extractor in the definition of computational knowledge soundness have access to?
?
Full access to the adversary's state, including any random coins.
It operates on the same inputs too, $(R, z, \sigma)$
<!--SR:2022-09-20,26,170-->
Note, this is already implicit in its access to the adversaries state.


What is the definition of computational knowledge soundness?
?
For all non-uniform polynomial time adversaries $\mathcal{A}$ there exists a non-uniform polynomial time extractor $\mathcal{X_A}$ such that:
$Pr[(R, z) \leftarrow \mathcal{R}(1^\lambda);$
$(\sigma, \tau) \leftarrow \textbf{Setup}(R);$
$((\phi, \pi); w) \leftarrow (\mathcal{A} || \mathcal{X_A})(R, z, \sigma):$
$(\phi, w) \notin R \land \textbf{Vfy}(R, \sigma, \phi, \pi) = 1] \approx 0$
<!--SR:2022-10-28,71,210-->

??? Why doesn't the adversary and extractor get the trapdoor? Is that because then it could definitely make such a proof without a witness?

### Definitions
#### Verifiability

What are the two types of verifiability for proofs?
?
Public verifiability and designated verifier proofs.
<!--SR:2022-11-22,87,230-->

How do we genaralise the definition of a non-interactive argument to create a designated verifier proof?
?
We split $\sigma$ into two parts $\sigma_P$ and $\sigma_V$, used by the prover and the verifier respectively.
<!--SR:2022-11-02,99,270-->

When is a non-interactive argument publicly verifiable?
?
When $\sigma_V$ can be deduced from $\sigma_P$.
<!--SR:2022-12-05,123,270-->

When is a non-interactive argument a designated verifier proof?
?
When $\sigma_V$ cannot be deduced from $\sigma_P$.
<!--SR:2022-11-26,94,230-->

We can relax the definitions of some properties of non-interactive arguments for designated verifier proofs. Which, and how?
?
We can relax soundness and knowledge soundness such that the adversary only sees $\sigma_P$ but not $\sigma_V$.
<!--SR:2022-10-22,91,270-->

#### SNARKs and SNARGs

What is the definition of succinctness for SNARKs and SNARGs?
?
A non-interactive argument where the verifier runs in polynomial time in $\lambda + |\phi|$ and the proof size is polynomial in $\lambda$ is called succinct.
<!--SR:2022-10-07,32,190-->

What is the difference between SNARKs and SNARGs?
?
A SNARG is sound, a SNARK is knowledge sound.
<!--SR:2022-12-28,137,270-->

What is the full expanded acronym for SNARK and SNARG?
?
Preprocessing succinct non-interactive argument of knowledge
Preprocessing succinct non-interactive argument
<!--SR:2022-12-11,129,270-->

What does fully succinct mean?
?
A SNARK or SNARG is fully succinct if the common reference string is polynomial in $\lambda$, as well as having succinct verification.
<!--SR:2022-09-18,21,210-->

What is the relationship between preprocessing and fully succinct SNARKs, and who showed it?
?
You can compile a preprocessing SNARK into a fully succinct SNARK.
<!--SR:2022-10-04,70,250-->

Who showed the relationship between preprocessing and fully succinct SNARKs?
?
Bitansky et al BCCT13.
<!--SR:2022-09-18,39,270-->

Does Groth16 focus on preprocessing SNARKs or fully succinct SNARKs?
?
Preprocessing SNARKs.
<!--SR:2022-10-17,79,250-->

#### Benign Relation Generators

What was the first danger discovered that was implied by indistinguishability obfuscation?
?
Indisginguishability obfuscation implies that for every candidate SNARK there are auxiliary output distributions that enable the adversary to create a valid proof without it being possible to extract the witness.
<!--SR:2022-12-25,135,270-->

Who discovered the first danger that was implied by indistinguishability obfuscation?
?
Bitansky et al BCPR14
<!--SR:2022-09-24,49,190-->

What is the strongest negative consequence of indistinguishability obfuscation?
?
Assuming public coin differing input obfuscation and other cryptographic assumptions, there is an auxiliary output distribution that defeats witness extraction for all candidate SNARKs.
<!--SR:2022-09-23,63,230-->

Who showed the strongest negative consequence of indistinguishability obfuscation?
?
Boyle and Pass BP15
<!--SR:2022-10-24,59,210-->

How do we get around impossibility results about relation generators' auxiliary input, and witness extraction? How do we know this works?
?
Since those results rely on specific auxiliary input distributions, we can assume that the relationship generator is benign in the sense that the relation and the auxiliary input are distributed in such a way that SNARKs can exist.
<!--SR:2022-11-09,102,270-->

## Quadratic Arithmetic Programs

### Circuits

What does our arithmetic circuit consist of?
?
Addition and multiplication gates over a finite field.
<!--SR:2022-11-11,81,230-->

What represents the statement in our arithmetic circuit?
?
Some subset of the the input/ouput wires.
<!--SR:2023-01-25,138,210-->

%% Why? Requiring input and output wires allows the other wires to act as a constraint on the possible statements that can be proven.%%

What represents the witness in our arithmetic circuit?
?
The wires that aren't the statement.
<!--SR:2023-01-09,150,230-->

What does binary relation of our arithmetic circuit consist of?
?
Statement wires and witness wires that satisfy the arithmetic circuit.
<!--SR:2023-03-22,190,250-->

### Arithmetic Constraints

What is the generalisation for circuits?
?
Arithmetic constraints - relations described by equations over a set of variables.
<!--SR:2022-09-24,86,250-->

What corresponds to the statement in our arithmetic constraints?
?
A subset of the variables.
<!--SR:2022-09-17,80,250-->

What corresponds to the witness in our arithmetic constraints?
?
The variables not in the statement.
<!--SR:2023-01-15,136,230-->

What is the binary relation of our arithmetic constraints?
?
WItnesses and statements that satisfy all the equations.
<!--SR:2022-09-17,81,250-->

What are our arithmetic constraints over?
?
$a_0 = 1$ and $a_1,...,a_m \in \mathbb{F}$
<!--SR:2022-10-17,60,210-->

What is the form of our arithmetic constraints?
?
$\sum a_iu_{i,q}\sum a_iv_{i,q}=\sum a_iw_{i,q}$,
where $u_{i,q},v_{i,q},w_{i,q}$ are constants specifying the $q$th equation.
<!--SR:2022-11-04,85,230-->

### Generalising Circuits

How do we know arithmetic constraints generalise circuits?
?
Multiplication and addition gates are special cases of constraint equations.
<!--SR:2022-09-27,88,250-->

How can a multiplication gate be described as a constraint?
?
$a_i \cdot a_j = a_k$, i.e, and equation where $u_i = v_j = w_k = 1$ and the remaining constants for the equation are $0$.
<!--SR:2023-02-26,197,270-->

How can an addition gate be described as a constraint?
?
$(a_i + a_j) \cdot a_0 = a_k$ where $u_i = u_j = v_0 = w_k = 1$, since $a_0 = 1$ by definition.
<!--SR:2022-12-25,127,250-->

In what sense are addition gates handled "for free?"
?
If $a_i + a_j = a_k$ and $a_k$ is multiplied by $a_l$, we write $(a_i + a_j) \cdot a_l$ and skip the calculation of $a_k$.
<!--SR:2022-12-12,116,250-->

### Formulating QAPs

What can we reformulate arithmetic constraints as, and what assumption do we have to make?
?
As a quadratic arithmetic program.
That the field $\mathbb{F}$ is large enough.
<!--SR:2022-10-03,70,250-->

??? Is this because the modular rearrangement doesn't work for tiny fields? Maybe fields with fewer elements than the number of roots in the polynomial?

Who introduced the idea of quadratic arithmetic programs?
?
Gennaro et al GGPR13.
<!--SR:2022-09-30,57,190-->

What are the steps in reformulating arithmetic constraints as a quadratic arithmetic program?
?
Picking a random vector.
Forming $t(x)$.
Creating the $u_i(x), v_i(x), w_i(x)$ polynomials.
Expressing the constraints as an evaluation of a single polynomial.
Refomulating the polynomial evaluation over values mod $t(x)$.
<!--SR:2022-11-18,84,210-->

What is the random vector?
?
Given $n$ equations, we pick arbitrary distinct $r_1,...,r_n \in \mathbb{F}$
<!--SR:2023-01-26,133,250-->

How is $t(x)$ defined?
?
$t(x) = \prod_{q=1}^n(x-r_q)$
<!--SR:2022-09-29,66,250-->

What are $u_i(x), v_i(x), w_i(x)$ and how are they defined?
?
They are degree $n-1$ polynomials such that for $i=0,...,m, q=1,...n$:
$u_i(r_q) = u_{i,q}$
$v_i(r_q) = v_{i,q}$
$w_i(r_q) = w_{i,q}$
<!--SR:2022-09-26,53,190-->

??? why does q start at 1 but i starts at 0? Is it that there are m+1 variables and n equations?

What is the condition that follows from an arithmetic constraint's constants being replaced by polynomials?
?
$a_0 = 1$ and the variables $a_1, ..., a_m$ satisfy the n equations if and only if at each point $r_1, ..., r_q$
$$\sum_{i=0}^ma_iu_i(r_q)\cdot \sum_{i=0}^ma_iv_i(r_q) = \sum_{i=0}^ma_iw_i(r_q)$$
<!--SR:2022-09-20,6,130-->

??? is it supposed to say "each $r_1, ..., r_n$?"

What is the final form of a quadratic arithmetic program?
?
$$\sum_{i=0}^ma_iu_i(X)\cdot \sum_{i=0}^ma_iv_i(X) \equiv \sum_{i=0}^ma_iw_i(X)\pmod{t(X)}$$
<!--SR:2022-12-13,115,230-->

How do we know that the condition evaluated at each $r_q$ is equivalent to the condition evaluated at every $t(X)$ all $\pmod{t(X)}$?
?
$t(X)$ is the lowest degree monomial with $t(r_q) = 0$ for each $r_q$.
Let $LHS = a(x)$ and $RHS = b(x)$
$a(X) \equiv b(X) \pmod{t(X)} \implies \exists k \in \mathbb{N} : a(X) + k \cdot t(X) = b(X)$ from the definition of mod
Which is true when $k \cdot t(X)$ is $0$, i.e., at each point $r_q$.
<!--SR:2022-11-08,102,270-->

### QAP Definition

What is the formal description of a whole quadratic arithmetic program? (Use independent elements describing the relation, not set builder notation for the pairs in the relation).
?
$R = (\mathbb{F}, aux, \mathscr{l}, \{u_i(X), v_i(X),w_i(X)\}_{i=0}^m, t(X))$
<!--SR:2022-10-15,40,230-->

??? Why are u, v, w described by their evaluations, but not t(X)?

What is $\mathbb{F}$?
?
A finite field.
<!--SR:2022-12-02,117,270-->

What is $aux$?
?
Auxiliary information.
<!--SR:2022-11-28,116,270-->

What is the $\mathscr{l}$ for?
?
Delineating the variables for the statement and the witness.
<!--SR:2022-12-14,126,270-->

What is the definition of $\mathscr{l}$?
?
$1 \leq \mathscr{l} \leq m$
<!--SR:2022-09-20,15,190-->

How do the degrees of $u_i(X), v_i(X), w_i(X), t(X)$ relate to each other?
?
$u_i(X), v_i(X), w_i(X), t(X) \in \mathbb{F}[X]$ and $u_i(X), v_i(X), w_i(X)$ have strictly lower degree than $n$, the degree of $t(X)$.
<!--SR:2022-12-30,130,250-->

What is the setbuilder notation for a quadratic arithmetic program as a relation?
?
$$
\begin{aligned}
R = \{ \\
(\phi, w) | \\
\phi = (a_1, ..., a_{\mathscr{l}}) \in \mathbb{F}^{\mathscr{l}} \\
w = (a_{\mathscr{l}+1}, ..., a_m) \in \mathbb{F}^{m - \mathscr{l}} \\
\sum_{i=0}^ma_iu_i(X)\cdot \sum_{i=0}^ma_iv_i(X) \equiv \sum_{i=0}^ma_iw_i(X)\pmod{t(X)} \\
\}
\end{aligned}
$$
<!--SR:2022-11-25,84,210-->

What is the definition of $\phi$ in a QAP?
?
$\phi = (a_1, ..., a_{\mathscr{l}}) \in \mathbb{F}^{\mathscr{l}}$
<!--SR:2022-09-16,52,210-->

What is the definition of $w$ in a QAP?
?
$w = (a_{\mathscr{l}+1}, ..., a_m) \in \mathbb{F}^{m - \mathscr{l}}$
<!--SR:2022-10-16,79,250-->

When is $\mathcal{R}$ a QAP generator?
?
If it generates relations of the appropriate form with fields of size larger than $2^{\lambda-1}$.
<!--SR:2022-09-21,48,210-->

How might relation generators vary in practice?
?
Deterministic vs randomised.
Field generated the rest of the relation is built on the field vs polynomials specified first then a random field is chosen.
<!--SR:2022-09-24,66,250-->

Why are the definitions of relation generators agnostic wrt the exact way the field and relation are generated?
?
To get the maximum flexibility, so that all different options can be modelled by the appropriate choices of relation generators.
<!--SR:2022-11-14,107,270-->

In pairing based NIZK arguments, what does aux specify and why?
?
The bilinear group. To provide a better model of settings where the relation is build on top of an already existing group.
<!--SR:2022-10-31,95,270-->

Why does chosing the group in the auxiliary information not lose generality?
?
Because we can think of the tradition setting where the relation is chosen first, then the bilinear group is chosen at random as the special case where the relation generator works in two steps, first choosing the relation and then picking a random bilinear group.
<!--SR:2022-11-04,98,270-->

What assumption does chosing the binlinear group as auxiliary information force?
?
That the relation generator is benign.
<!--SR:2022-10-22,78,250-->

Why do we have to assume the relation generator is benign?
?
Because indistinguishability obfuscation implies there is some auxiliary information for which witness extraction is impossible.
And because the relation generator picks the bilinear group to give our generator definition flexibility.
<!--SR:2022-09-30,74,270-->

## Linear Interactive Proofs

### Structure of a LIP

What does LIP stand for?
?
Linear interactive proof
<!--SR:2022-11-01,85,250-->

What is the purpose of a LIP?
?
It is a useful characterisation of the information theoretic underpinning of various SNARK constructions.
<!--SR:2022-11-10,98,250-->

Who invented LIPs?
?
Bitansky et al. BCI+13
<!--SR:2022-12-29,137,270-->

How do we denote the degree of a LIP?
?
$(d_Q, d_D)$
<!--SR:2022-12-19,131,270-->

What are the (top level) algorithms for a LIP?
?
Setup
Prove
Vfy
<!--SR:2022-10-24,91,270-->

What is a LIP generated by, and what do we assume about it?
?
A relation generator $\mathcal{R}$, where we assume the relations specify a finite field $\mathbb{F}$.
<!--SR:2022-09-17,39,190-->

What, broadly, is a LIP?
?
A non inteactive argument system where the (Setup, Prove, Vfy) algorithms work with matrices.
<!--SR:2022-11-12,93,250-->

What does Setup do in a LIP?
?
It creates an arithmetic circuit of multiplicative depth $d_Q$ that takes as input randomness $\textbf{r} \in \mathbb{F}^\mu$ and returns vectors $\sigma \in \mathbb{F}^m$ and $\tau \in \mathbb{F}^n$.
<!--SR:2022-09-17,44,190-->

??? Why does it have to *create* a circuit? Why can't it just use a fixed circuit? Is this to create flexibility? But surely we have enough flexibility from the randomness vector that is given to the circuit.

What do we assume for notational simplicity regarding the Setup algrotitm in a LIP?
?
That $\sigma$ always contains 1 as an entry such that there is no distinction between affine and linear functions of $\sigma$
<!--SR:2022-10-24,41,210-->

??? What does affine mean? What does linear mean in this context, since these are circuits, not matrixes? What is the difference between affine and linear? How does this assumption make sure there's no difference between them? Is this a merited assumption, or could someone somehow create a LIP where $\sigma$ doesn't contain 1, invalidating the result?

What does the Prove do in a LIP?
?
It operates in two stages.
First it runs $\Pi \leftarrow \textbf{ProofMatrix}(R, \phi, w)$ where ProofMatrix is a probabilistic polynomial time algorithm that generates a matrix $\Pi \in \mathbb{F}^{k \times m}$
Then it computes the proof as $\boldsymbol{\pi} = \Pi \boldsymbol{\sigma}$
<!--SR:2022-09-16,40,170-->

What is ProofMatrix, broadly?
?
A probabilistc polynomial time algorithm used in Prove in a LIP that produces a matrix.
<!--SR:2022-10-25,62,230-->

What is the output of ProofMatrix?
?
A matrix $\Pi \in \mathbb{F}^{k \times m}$
<!--SR:2023-01-15,130,250-->

What is $k$ in a LIP?
?
The number of rows in the matrix from ProofMatrix
<!--SR:2022-10-29,50,230-->

What arguments does ProofMatrix accept?
?
$(R, \phi, w)$
<!--SR:2022-09-29,17,170-->

What does Vfy do in a LIP?
?
The verifier runs in two stages.
First is runs a deterministic polynomial time algorithm $t \leftarrow \textbf{Test}(R, \phi)$ to get an arithmetic circuit $t : \mathbb{F}^{m+k} \rightarrow \mathbb{F}^\eta$ of multiplicative depth $d_D$
It then accepts the proof if and only if $t(\sigma, \pi) = \textbf{0}$, i.e., the zero vector.
<!--SR:2022-10-01,74,270-->

What is Test?
?
A deterministic polynomial time algorithm.
<!--SR:2022-10-19,88,270-->

What are the inputs of Test?
?
$(R, \phi)$
<!--SR:2022-10-11,30,210-->

What does Test output?
?
An arithmetic circuit $t$.
<!--SR:2022-10-30,95,270-->

What is the definition of $t$?
?
An arithmetic circuit $t : \mathbb{F}^{m+k} \rightarrow \mathbb{F}^\eta$
<!--SR:2022-12-20,132,270-->

What arguments is $t$ passed?
?
$(\sigma, \pi)$
<!--SR:2022-09-25,34,190-->

When does Vfy accept in a LIP?
?
If $t(\sigma, \pi) = \textbf{0}$, i.e., the zero vector.
<!--SR:2022-11-11,99,250-->

What are the degrees and dimensions of a LIP?
?
$d_Q, d_D, \mu, m, n, k, \eta$
<!--SR:2022-11-23,97,230-->

What kinds of values can the degrees and dimensions of a LIP take?
?
They may be constants or polynomials in the security parameter $\lambda$
<!--SR:2022-12-09,94,250-->

What is $d_Q$?
?
The multiplicative depth of the setup circuit.
<!--SR:2022-10-29,58,210-->

What is $d_D$?
?
The multiplicative depth of the verifier circuit output by Test.
<!--SR:2022-11-01,95,270-->

What is $\mu$?
?
The dimension of the randomness vector used in Setup.
<!--SR:2022-12-28,118,250-->

What is $m$ in a LIP?
?
The dimension in the crs vector $\sigma$ made in Setup.
<!--SR:2022-11-03,98,270-->

??? Why is this called m? Is this equivalent to the number of variables in a QAP or constraint, or inputs in a circuit?

What is $n$ in a LIP?
?
The dimension of the simulation trapdoor vector $\tau$ made in Setup.
<!--SR:2022-10-08,81,270-->

What is $\eta$ in a LIP?
?
The dimension of the vector output by $t$.
<!--SR:2022-12-10,100,230-->

??? Why are the algorithms in Setup and Vfy circuits, but the one in Prove is a polynomial time algorithm?

### Definition of a LIP

What is the definition of a LIP?
?
The tuple $(\textbf{Setup, Prove, Vfy})$ is a linear interactive proof for $\mathcal{R}$ if it has perfect completeness and statistical knowledge soundness against affine prover strategies.
<!--SR:2022-10-09,50,230-->

What, roughly, does statistical knowledge soundness against affine prover strategies mean?
?
That a witness can be extracted from a proof matrix.
<!--SR:2022-12-04,119,270-->

What is the definition of statistical knowledge soundness against affine prover strategies?
?
There is an extractor $\mathcal{X}$ such that for all adversaries $\mathcal{A}$:
$$
\begin{align}
Pr[
(R,z) \leftarrow \mathcal{R}(1^\lambda); \\
(\sigma, \tau) \leftarrow \textbf{Setup}(R); \\
(\phi, \Pi) \leftarrow \mathcal{A}(R,z); \\
w \leftarrow \mathcal{X}(R, \phi, \Pi): \\
\Pi \in \mathbb{F}^{m \times k} \land \textbf{Vfy}(R, \sigma, \phi, \Pi\sigma) = \textbf{0} \land (\phi, w) \notin R \\
] \approx 0
\end{align}
$$
<!--SR:2022-09-19,40,190-->

??? Is there a mistake here, should it me that Pi in kxm rather than mxk?

??? Why does the adversary not accept sigma? Is that because it doesn't need to, since it implicitly takes this argument since we're requiring that Vfy works with sigma. Does the extractor not accept sigma for the same reasons?

??? Why is there a single extractor, whereas in computational knowledge soundness each adversary has its own extractor?

??? Why are LIPs called interactive??? The don't seem interactive at all.

### LIPs to non-interactive arguments

What can LIPs be compiled into and how?
?
Publicly verifiable non-interactive by using pairings.
Designated verifier non-interactive arguments using Paillier encryption.
<!--SR:2022-11-02,70,210-->

What kind of LIP compiles to a non-interactive argument and how (roughly) is it executed?
?
An alegebraic LIP of degree $(d_Q, 2)$ can be executed "in the exponents."
<!--SR:2022-12-02,79,230-->

What does the crs of a compiled LIP contain, roughly?
?
Exponentiations of the field elements in $\boldsymbol{\sigma}$, (the crs of the LIP).
<!--SR:2022-10-25,78,210-->

How does the prover in a compiled LIP compute the proof?
?
With multi-exponentiations of group elements, corresponding to linear operations on the field elements in $\sigma$ (where $\sigma$ refers to the crs of the LIP).
<!--SR:2022-10-12,35,170-->

How does the verifier in a compiled LIP check the argument?
?
By verifying a number of pairing product equations, which corresponds to checking quadratic equations in the exponents.
<!--SR:2022-10-22,63,190-->

What are pairing product equations?
?
Equations formed by multiplying together the results of pairings.
<!--SR:2022-10-26,83,250-->
# Constructions

What kind of language does our pairing based NIZK construction prove?
?
Quadratic Arithmetic Programs.
<!--SR:2022-11-30,86,230-->

What does a proof in our NIZK construction consist of?
?
3 group elements.
<!--SR:2022-12-06,120,270-->

What are the (very broad) steps for consructing the Groth16 NIZK argument?
?
Construct a LIP.
Convert the LIP into a pairing-based NIZK argument.
<!--SR:2022-11-23,109,270-->

### LIPs for QAPs

What is $h(x)$?
?
The quotient polynomial, i.e, the number of times we add $t(X)$ to make each side of the QAP equation equal, given equality $\mod t(X)$.
<!--SR:2022-11-24,110,270-->

What is the degree of $h(X)$?
?
$n-2$
<!--SR:2022-11-25,111,270-->

How do we know the degree of $h(X)$?
?
$u_i(X), v_i(X), w_i(X)$ are degree $n-1$ polynomials, and $t(X)$ is a degree $n$ polynomial. 
Since, roughly, $h$ = $(u \cdot v - w)/t$ then the degree of is $(n-1) + (n-1) - n = n - 2$
<!--SR:2022-12-07,120,270-->

#### Setup

What are the steps in Setup for a LIP for a QAP, roughly?
?
Pick parameters
Set $\boldsymbol{\tau}$
Set $\boldsymbol{\sigma}$
<!--SR:2023-01-13,121,250-->

What are the parameters selected in the Setup for a LIP for a QAP?
?
$\alpha, \beta, \gamma, \delta, x$
<!--SR:2022-10-16,55,250-->

What is $\boldsymbol{\tau}$ in a LIP for a QAP?
?
$(\alpha, \beta, \gamma, \delta, x)$
<!--SR:2022-10-29,83,250-->


What set are the parameters in Setup for a LIP for a QAP selected from?
?
$\mathbb{F}^*$
<!--SR:2022-12-26,104,230-->

??? How is it possible that they are selected from this? They appear to just be single elements?

##### Sigma

What, broadly are the parts of $\sigma$ in a LIP for a QAP?
?
The $\tau$ part
The exponentiations of $x$
The linear combinations for $\phi$
The linear combinations for $w$
The evaluations of $t(x)$
<!--SR:2022-09-20,19,230-->

What is "the $\tau$ part" of $\sigma$ for a QAPLIP?
?
$\alpha, \beta, \gamma, \delta$
<!--SR:2023-01-04,117,270-->

What is the "exponentiations of $x$" part of $\sigma$ for a QAPLIP?
?
$\{x^i\}_{i=0}^{n-1}$
<!--SR:2022-11-17,64,230-->

What is the "linear combinations for $\phi$" part of $\sigma$ for a QAPLIP?
?
$$\Bigl\{ 
\frac{
\beta u_i(x) + \alpha v_i(x) + w_i(x)
}{\gamma}
\Bigl\}^\mathscr{l}_{i=0}$$
<!--SR:2022-09-21,20,230-->

What is the "linear combinations for $w$" part of $\sigma$ for a QAPLIP?
?
$$\Bigl\{ 
\frac{
\beta u_i(x) + \alpha v_i(x) + w_i(x)
}{\delta}
\Bigl\}^m_{i=\mathscr{l}+1}$$
<!--SR:2022-10-02,19,210-->

What is the "evaluations of $t(x)$" part of $\sigma$ for a QAPLIP?
?
$$\Bigl\{ 
\frac{
x^it(x)
}{\delta}
\Bigl\}^{n-2}_{i=0}$$
<!--SR:2022-09-17,26,190-->

##### Prove

What is the function signature of Prove for a QAPLIP?
?
$\pi \leftarrow$Prove$(R, \sigma, a_1, ..., a_m)$
<!--SR:2022-11-16,88,250-->

What are the steps involved in Prove for a QAP LIP?
?
Choosing random values.
Calculating the elements $(A, B, C)$.
Calculating the matrix $\Pi$.
<!--SR:2022-10-27,70,270-->

What is the dimension of $\Pi$ in a QAPLIP?
?
$3 \times (m + 2n + 4)$
<!--SR:2022-11-14,70,230-->

??? Why is the number of columns $m + 2n + 4$? It should be $m + 2n + 3$, since there are 4 elements on their own, the witness and statement parts have m, and there are n exponeitations of x and n-1 evaluations of t(x), giving $4 + m + n + n - 1 = m + 2n + 3$.

What is the definition of $\pi$ in a QAPLIP?
?
$\pi = \Pi\sigma = (A, B, C)$
<!--SR:2022-12-17,107,270-->

What is the definition of $A$ in a QAPLIP?
?
$A = \alpha + \sum_{i=0}^m a_iu_i(x) + r\delta$
<!--SR:2022-09-21,15,170-->

What is the definition of $B$ in a QAPLIP?
?
$B = \beta + \sum_{i=0}^m a_iv_i(x) + s\delta$
<!--SR:2022-11-02,48,170-->

How is $C$ computed by Prove in a QAPLIP?
?
$$
C = 
\frac{
\sum_{i=\mathscr{l}+1}^m
a_i(\beta u_i(x) + \alpha v_i(x) + w_i(x)) + h(x)t(x)
}
{\delta}
+ As + rB - rs\delta
$$
<!--SR:2022-09-21,11,150-->

##### Vfy

What is the signature of Vfy in a QAPLIP?
?
$0/1 \leftarrow$Vfy$(R, \boldsymbol{\sigma}, a_1, ..., a_{\mathscr{l}})$
<!--SR:2022-09-19,39,230-->

What kind of thing is $\boldsymbol{t}$ in a QAPLIP?
?
A quadratic multi-variate polynomial.
<!--SR:2022-09-29,54,250-->

What is the short form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$\boldsymbol{t}(\boldsymbol{\sigma}, \boldsymbol{\pi}) = 0$
<!--SR:2022-09-29,40,250-->

What is the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$$
A \cdot B =
\alpha \cdot \beta +
\frac{
\sum_{i=0}^\mathscr{l} a_i(\beta u_i(x) + \alpha v_i(x) + w_i(x))
}{\gamma}
\cdot \gamma + C \cdot \delta
$$
<!--SR:2022-09-18,26,210-->

??? Why are we dividing by gamma then multiplying by it again?

What are the "parts" of the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
Proof element product
CRS product
Statement sum
Proof CRS product
<!--SR:2022-10-30,77,270-->

What is in the "proof element product" part of the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$A \cdot B$
<!--SR:2022-10-07,55,250-->

What is in the "CRS product" part of the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$\alpha \cdot \beta$
<!--SR:2022-11-29,95,270-->

What is in the "statement sum" part of the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$$
\frac{
\sum_{i=0}^\mathscr{l} a_i(\beta u_i(x) + \alpha v_i(x) + w_i(x))
}{\gamma} \cdot \gamma 
$$
<!--SR:2022-12-03,84,230-->

What is in the "proof CRS product" part of the long form equation $\boldsymbol{t}$ should satisfy in a QAPLIP?
?
$C \cdot \delta$
<!--SR:2022-10-30,64,230-->

When does Vfy accept in a QAPLIP?
?
When the polynomial test passes.
<!--SR:2023-01-11,124,270-->

##### Sim

What is the function signature of Sim for a QAPLIP?
?
$\pi \leftarrow Sim(R, \boldsymbol{\tau}, a_1, ..., a_\mathscr{l})$
<!--SR:2022-09-17,29,250-->

What, roughly, are the steps of Sim in a QAPLIP?
?
Pick A and B.
Compute C.
Return proof.
<!--SR:2022-09-23,46,290-->

How does the simulator pick A and B in a QAPLIP?
?
Randomly from $\mathbb{F}$
<!--SR:2022-12-22,104,290-->

How does the simulator in a QAPLIP compute C?
?
$$
C =
\frac{AB - \alpha\beta - \sum^{\mathscr{l}}_{i=0} a_i(\beta ui(x) + \alpha v_i(x) + w_i(x))}{\delta}
$$
<!--SR:2022-10-25,50,210-->

What is the definition of the proof that the simulator returns in a QAPLIP?
?
$\boldsymbol{\pi} = (A,B,C)$
<!--SR:2023-01-02,113,290-->










??? "at significant computational cost though" seems like an ugly sentence.

## NIZK for QAP

??? Why don't we have h(x) in the definition of the relation?

??? How can we construct A, B, and C without alpha, beta, r, and delta? Is it possible to do with the other group elements, i.e, you don't have to do it by exponentiating the generator?

??? Shouldn't we be subtracting $rs\delta$ in the compiled LIP too?

??? How is the verification pairing equation equivalent to the QAPLIP's verification equation?