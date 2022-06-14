#flashcards/zkps/Groth16
# Abstract

What makes SNARGs succinct?
?
Small size and low verification complexity.
<!--SR:2022-07-20,40,210-->

What is a SNARG?
?
Succinct non-interactive argument
<!--SR:2022-07-29,50,250-->

What is a SNARK?
?
Succinct non-interactive argument of knowledge
<!--SR:2022-06-27,33,250-->

What does a pairing based SNARG consist of?
?
A number of group elements.
<!--SR:2022-06-28,34,250-->

What is the central question of Groth16?
?
How efficient can pairing based SNARGs be?
<!--SR:2022-07-17,39,230-->

What language is Groth16's SNARG for, and what is that language's most important property?
?
Circuit satisfiability, that it is NP-complete.
<!--SR:2022-08-03,52,250-->

What kind of pairings does Groth16 use and why?
?
Assymetric pairings for higher efficiency.
<!--SR:2022-06-17,25,250-->

What does a Groth16 SNARG consist of?
?
3 group elements.
<!--SR:2022-08-09,57,250-->

What does verifying a Groth16 SNARG require?
?
Checking a single pairing product equation using 3 pairings in total.
<!--SR:2022-06-15,5,130-->

What is the knowledge complexity of the Groth16 SNARG?
?
It is zero knowledge.
<!--SR:2022-06-30,31,230-->

What is the second contribution of Groth16 and how is it shown?
?
That SNARGs using generic symmetric bilinear group operations can't consist of a single element.
By showing that linear interactive proofs cannot have a linear decision procedure.
<!--SR:2022-07-02,18,190-->

What would extending the lower bound in Groth16 prove?
?
Extending the lower bound to 2 elements would prove the optimality of the 3 element SNARG.
<!--SR:2022-06-21,28,250-->

Who posed the question answered by Groth16's second contribution?
?
Nir Bitansky, Allesandro Chisea, Yuval Ishai, Rafail Ostrovsky, and Omer Paneth.
<!--SR:2022-07-01,19,150-->

# Introduction

## Prior Work

Who introduced zero-knowledge proofs?
?
Shafi Goldwasser, Silvio Micali, and Charles Rackoff.
<!--SR:2022-06-26,34,270-->

What are the 3 core properties of zero knowledge proofs?
?
Completeness, Soundness, and Zero-Knowledge.
<!--SR:2022-07-12,41,250-->

Describe the completeness property.
?
Given a statement and a witness, the prover can convince the verifier.
<!--SR:2022-06-23,21,190-->

Describe the soundness property.
?
A malicious prover cannot convince the verifier of a false statement.
<!--SR:2022-07-10,40,250-->

Describe the zero knowledge property.
?
The proof does not reveal anything but the truth of the statement, in particular it does not reveal the prover's witness.
<!--SR:2022-06-18,9,170-->

How did Blum, Feldman, and Micali extend the notion of interactive proofs?
?
To non-interactive zero knowledge proofs (NIZK) in the common reference string model.
<!--SR:2022-06-19,28,250-->

Where are NIZKs useful, according to Groth16?
?
The construction of non-interactive cryptographic schemes, e.g., digital key signatures, and CCA-secure public key encryption.
<!--SR:2022-06-23,10,170-->

Where was the first sub-linear communication zero-knowledge argument, sending fewer bits than the size of the statement given?
?
Kili92, by Joe Kilian.
<!--SR:2022-07-06,30,190-->

What did Micali00 propose?
?
Sublinear size NIZK arguments by letting the prover in a communication efficient zero-knowledge argument compute the verifier's challenges using a cryptographic function.
<!--SR:2022-06-19,15,150-->

Which papers introduced pairing based NIZKs, and what did this yield?
?
Groth et al: GOS12, GOS06, Gro06, GS12.
The first linear sized proofs based on standard assumptions.
<!--SR:2022-06-20,6,130-->

What did Gro10 achieve wrt communication complexity and how?
?
The first constant size NIZK arguments, by combining pairing based NIZKs with ideas from interactive zero-knowledge.
<!--SR:2022-06-24,19,190-->

What did Lip12 achieve wrt communication complexity?
?
Constant size NIZK arguments based on progression-free sets to reduce the size of the common reference string.
<!--SR:2022-07-03,19,170-->

What is Groth's constant size NIZK based on?
?
Constructing a set of polynomial equations and using pairings to efficiently verify these equations.
<!--SR:2022-07-14,34,190-->

UNFINISHED

## Our Contribution

UNFINISHED

# Preliminaries
## Notation

What does $\approx$ mean, roughly?
?
That two functions approach each other exponentially.
<!--SR:2022-06-16,3,250-->

What is the definition of $\approx$?
?
Given two function $f, g : \mathbb{N} \rightarrow [0,1]$, we write $f(\lambda) \approx g(\lambda)$ when $| f(\lambda) - g(\lambda)| = \lambda^{-\omega(1)}$
<!--SR:2022-06-17,4,250-->

What is the limit definition of $\omega$?
?
$lim_{n \rightarrow \infty} |f(n)|/g(n) = \infty$
<!--SR:2022-06-15,2,250-->

What is the formal definition of $\omega$?
?
$\forall k > 0\ \exists n_0 \forall n > n_0 : f(n) > k \cdot g(n)$
<!--SR:2022-06-16,3,250-->

What does $\lambda$ represent, and what do its values mean?
?
$\lambda$ is the security parameter, and as it grows we want higher security.
<!--SR:2022-06-15,2,250-->

What does $y = A(x;r)$ mean?
?
That the algorithm $A$ outputs $y$ on the input $x$ with randomness $r$.
<!--SR:2022-06-18,4,250-->

What does $y \leftarrow A(x)$ mean?
?
We pick randomness $r$ at random and set $y = A(x;r)$.
<!--SR:2022-06-16,3,250-->

What does $y \leftarrow S$ mean?
?
We pick $y$ uniformly at random from set $S$.
<!--SR:2022-06-16,2,230-->

What do we assume about random sampling?
?
That it's possible to randomly sample from sets such as $\mathbb{Z}_p$
<!--SR:2022-06-15,1,230-->

What does $(y;z) \leftarrow (\mathcal{A} || X_{\mathcal{A}})(x)$ mean?
?
$\mathcal{A}$ outputs $y$ on input $x$ and $X_{\mathcal{A}}$ outputs $z$ on the same input (including random coins).
This includes the input of both algorithms $(R, z, \sigma)$.
<!--SR:2022-06-16,3,250-->

## Bilinear Groups

What are the parts of a bilinear group?
?
$(p, \mathbb{G}_1, \mathbb{G}_2, \mathbb{G}_T, e)$
<!--SR:2022-06-15,2,250-->

What is $p$?
?
A prime number.
<!--SR:2022-06-15,2,250-->

What are $\mathbb{G}_1, \mathbb{G}_2, \mathbb{G}_T$
?
Groups of prime order $p$.
<!--SR:2022-06-15,2,250-->

What is $e$?
?
$e : \mathbb{G}_1 \times \mathbb{G}_2 \rightarrow \mathbb{G}_T$ is a bilinear map, i.e., $e(U^a, V^b) = e(U, V)^{ab}$
<!--SR:2022-06-15,1,230-->

What is a property of generators of our bilinear group?
?
if $G$ is a generator of $\mathbb{G}_1$ and $H$ is a generator of $\mathbb{G}_2$ then $e(G, H)$ is a generator of $\mathbb{G}_T$.
<!--SR:2022-06-17,4,250-->

What are the generic bilinear group operations?
?
Group operations for the groups.
Evaluating the bilinear map.
Deciding the equality of group elements.
Sampling generators of the groups.
<!--SR:2022-06-15,2,250-->

What do we assume about the bilinear group operations?
?
That there are efficient algorithms for computing them.
<!--SR:2022-06-17,4,250-->

What are the names for the types of bilinear groups?
?
Type I, Type II, and Type III
<!--SR:2022-06-15,2,250-->

Who classified the types of bilinear groups?
?
Galbraith et al GPS08
<!--SR:2022-06-17,3,230-->

What is a Type I bilinear group?
?
Where $\mathbb{G}_1 = \mathbb{G}_2$
<!--SR:2022-06-17,4,250-->

What are Type II bilinear groups?
?
Where $\mathbb{G}_1 \neq \mathbb{G}_2$ and there is an efficiently computable non-trivial homomorphism $\psi : \mathbb{G}_1 \rightarrow \mathbb{G}_2$
<!--SR:2022-06-17,4,250-->

What are Type III bilinear groups?
?
Where there is no efficiently computable non-trivial homomorphism in either direction between $\mathbb{G}_1$ and $\mathbb{G}_2$.
<!--SR:2022-06-16,2,230-->

What is special about Type III bilinear groups?
?
They are the most efficient type of bilinear groups, and hence the most relevant for practical applications.
<!--SR:2022-06-18,4,250-->

For which type of bilinear group is the lower bound given?
?
Type III
<!--SR:2022-06-15,2,250-->

For which type of bilinear group does the construction work?
?
All 3 types
<!--SR:2022-06-17,4,250-->

## Non-interactive Zero-Knowledge Arguments of Knowledge

### Algorithms

What is $\mathcal{R}$?
?
A relation generator that, given $\lambda$ in unary returns a polynomial time decidable binary relation $R$.
<!--SR:2022-06-16,3,250-->

??? Why is lambda in unary?

What is $\phi$?
?
The statement.
<!--SR:2022-06-17,4,250-->

What is $w$?
?
The witness.
<!--SR:2022-06-16,3,250-->

What kinds of pairs are in $R$?
?
$(\phi, w)$, i.e., statement and witness
<!--SR:2022-06-15,2,250-->

What is $\mathcal{R}_\lambda$?
?
The set of possible relations $\mathcal{R}$ might output given $1^\lambda$.
<!--SR:2022-06-17,4,250-->

What is $z$?
?
Auxilliary information that the relation generator might output, which will be given to the adversary.
<!--SR:2022-06-17,3,230-->

What is an efficient prover publicly verifiable non-interactive argument for $\mathcal{R}$?
?
A quadruple of polynomial time algorithms $(\textbf{Setup, Prove, Vfy, Sim})$
<!--SR:2022-06-17,4,250-->

What is the definition of $\textbf{Setup}$?
?
$(\sigma, \tau) \leftarrow \textbf{Setup}(R)$
The setup takes as input the security paramater $\lambda$ and a relation $R \in R_\lambda$ and returns a common reference string $\sigma$ and a simulation trapdoor $\tau$ for the relation $R$.
<!--SR:2022-06-16,3,250-->

??? why don't we write the setup as explicitly taking the security parameter?

What is the definition of $\textbf{Prove}$?
?
$\pi \leftarrow\textbf{Prove}(R, \sigma, \phi, w)$
The prover algorithm takes as input the common reference string and $(\phi, w) \in R$ and outputs the argument $\pi$.
<!--SR:2022-06-18,4,250-->

??? Why do we say the prover algorithm accepts the relation?

What is $\sigma$?
?
The common reference string.
<!--SR:2022-06-18,4,250-->

What is $\tau$?
?
The simulation trapdoor.
<!--SR:2022-06-16,3,250-->

What is $tau$ used for?
?
The simulator gets access to $tau$ so it can generate proofs indistinguishable from actual proofs, so that we can prove that an argument is zero knowledge.
<!--SR:2022-06-18,4,250-->

What is $\pi$?
?
The argument.
<!--SR:2022-06-15,2,250-->

What is the definition of $\textbf{Vfy}$?
?
$0/1 \leftarrow \textbf{Vfy}(R, \sigma, \phi, \pi)$
The verification algorithm takes as input the common reference string, the statement, and the argument, and returns 0 (reject) or 1 (accept).
<!--SR:2022-06-15,2,250-->

What is the definition of $\textbf{Sim}$?
?
$\pi \leftarrow \textbf{Sim}(R, \tau, \phi)$
The simulator takes as input a simulation trapdoor and statement $\phi$, and outputs an argument.
<!--SR:2022-06-16,2,230-->

??? Why does the simulator not get the common reference string? Is it because it's efficiently computable from the trapdoor?

### Properties

What is a non-interactive argument?
?
We say $(\textbf{Setup, PRove, Vfy)})$ is a non-interactive for $\mathcal{R}$ if it has perfect completeness and computation soundness.
<!--SR:2022-06-15,2,250-->

What is a perfect non-interactive zero-knowledge argument of knowledge?
?
We say that $(\textbf{Setup, Prove, Vfy, Sim})$ is a perfect non-interactive zero-knowledge argument of knowledge for $\mathcal{R}$ if it has perfect completeness, perfect zero knowledge, and computational knowledge soundness.
<!--SR:2022-06-17,4,250-->

What is perfect completeness, roughly?
?
Completeness says that, given any true statement, an honest prover should be able to convince an honest verifier.
<!--SR:2022-06-16,3,250-->

What is the definition of perfect completeness?
?
For all $\lambda \in \mathbb{N}, R \in \mathcal{R}_\lambda, (\phi, w) \in R$:
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R);$
$\pi \leftarrow \textbf{Prove}(R, \sigma, \phi, w):$
$\textbf{Vft}(R, \sigma, \phi, \pi) = 1] = 1$
<!--SR:2022-06-17,3,230-->

What is perfect zero knowledge, roughly?
?
An argument is zero knowledge if it does not leak any information besides the truth of the statement.
<!--SR:2022-06-17,4,250-->

What is the definition of perfect zero-knowledge?
?
We say $(\textbf{Setup, Prove, Vfy, Sim})$ is a perfect zero-knowledge if for all $\lambda \in \mathbb{N}, (R, z) \leftarrow \mathcal{R}(1^\lambda), (\phi, w) \in R$ and adversaries $\mathcal{A}$:
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R); \pi \leftarrow \textbf{Prove}(R, \sigma, \phi, w): \mathcal{A}(R, z, \sigma, \tau, \pi) = 1] =$
$Pr[(\sigma, \tau) \leftarrow \textbf{Setup}(R); \pi \leftarrow \textbf{Sim}(R, \tau, \phi) : \mathcal{A}(R, z, \sigma, \tau, \pi) = 1]$
<!--SR:2022-06-15,1,210-->

What does the adversary represent in the definition of perfect zero knowledge?
?
A malicious verifier trying to learn extra information from the proof.
<!--SR:2022-06-16,3,250-->

What does the adversary in the definition of perfect zero knowledge do?
?
Tries to distinguish between the proof from prover and the proof from simulator.
<!--SR:2022-06-18,4,250-->

What inputs does the adversary in the definition of perfect zero knowledge get?
?
The relation, the auxillary output from the relation generator, the common reference string, the simulation trapdoor and the proof (from either the prover or the simulator).
$R, z, \sigma, \tau, \pi$
<!--SR:2022-06-15,1,210-->

??? Why does this adversary get so much information including z and tau?

What is computational soundness, roughly?
?
We say a set of algorithms is sound if it is not possible to prove a false statement, i.e., convince the verifier if no witness exists.
<!--SR:2022-06-17,4,250-->

What is the definition of computational soundness?
?
Let $L_R$ be the language consisting of statements for which there exist matching witnesses in R. Formally, we require that for all non-uniform polynomial time adversaries $\mathcal{A}$:
$Pr[(R,z) \leftarrow \mathcal{R}(1^\lambda); (\sigma, \tau) \leftarrow \textbf{Setup}(R); (\phi, \pi) \leftarrow \mathcal{A}(R, z, \sigma) : \sigma \notin L_R \land \textbf{Vfy}(R, \sigma, \phi, \pi) = 1] \approx 0$
<!--SR:2022-06-16,2,230-->

What does the adversary represent in the definition of computational soundness?
?
A malicious prover trying to find a proof and statement that the verifier will accept where the statement has no possible witness.
<!--SR:2022-06-15,1,210-->

What inputs does the adversary in the definition of computational soundness accept?
?
The relation, the auxilary input, and the common reference string.
$(R, z, \sigma)$
<!--SR:2022-06-16,3,250-->

??? Why does it not also accept the simulation trapdoor? Is it because then it could create any proof it likes.

??? Why does it have the auxilary input? What's the point of the auxilary input, in fact?

What is computational knowledge soundness, roughly?
?
A strengthening of the notion of soundness, where there is an extractor that can compute a witness whenver an adversary produces a valid argument.
<!--SR:2022-06-18,4,250-->

??? Why does the extractor in the definition for computational knowledge soundness not need the simulation trapdoor?

??? Why does the adversary in the definition for computational knowledge soundness need the auxillary information?

??? Does the definition of computational knowledge soundness imply that any valid prover also has their witness extracted? How can this be compatible with zero knowledge? Is this because we don't actually have access to any adversary's random coins? 

What does the extractor in the definition of computational knowledge soundness have access to?
?
Full access to the adversary's state, including any random coins.
<!--SR:2022-06-15,1,210-->

What is the definition of computational knowledge soundness?
?
For all non-uniform polynomial time adversaries $\mathcal{A}$ there exists a non-uniform polynomial time extractor $\mathcal{X_A}$ such that:
$Pr[(R, z) \leftarrow \mathcal{R}(1^\lambda);$
$(\sigma, \tau) \leftarrow \textbf{Setup}(R);$
$((\phi, \pi); w) \leftarrow (\mathcal{A} || \mathcal{X_A})(R, z, \sigma):$
$(\phi, w) \notin R \land \textbf{Vfy}(R, \sigma, \phi, \pi) = 1] \approx 0$
<!--SR:2022-06-15,1,210-->

### Definitions
#### Verifiability

What are the two types of verifiability for proofs?
?
Public verifiability and designated verifier proofs.
<!--SR:2022-06-18,4,250-->

How do we genaralise the definition of a non-interactive argument to create a designated verifier proof?
?
We split $\sigma$ into two parts $\sigma_P$ and $\sigma_V$, used by the prover and the verifier respectively.
<!--SR:2022-06-18,4,250-->

When is a non-interactive argument publicly verifiable?
?
When $\sigma_V$ can be deduced from $\sigma_P$.
<!--SR:2022-06-18,4,250-->

When is a non-interactive argument a designated verifier proof?
?
When $\sigma_V$ cannot be deduced from $\sigma_P$.
<!--SR:2022-06-17,3,250-->

We can relax the definitions of some properties of non-interactive arguments for designated verifier proofs. Which, and how?
?
We can relax soundness and knowledge soundness such that the adversary only sees $\sigma_P$ but not $\sigma_V$.
<!--SR:2022-06-18,4,250-->

#### SNARKs and SNARGs

What is the definition of succinctness for SNARKs and SNARGs?
?
A non-interactive argument where the verifier runs in polynomial time in $\lambda + |\phi|$ and the proof size is polynomial in $\lambda$ is called succinct.
<!--SR:2022-06-15,1,230-->

What is the difference between SNARKs and SNARGs?
?
A SNARG is sound, a SNARK is knowledge sound.
<!--SR:2022-06-16,2,250-->

What is the full expanded acronym for SNARK and SNARG?
?
Preprocessing succinct non-interactive argument of knowledge
Preprocessing succinct non-interactive argument
<!--SR:2022-06-18,4,250-->

What does fully succinct mean?
?
A SNARK or SNARG is fully succinct if the common reference string is polynomial in $\lambda$, as well as having succinct verification.
<!--SR:2022-06-18,4,250-->

What is the relationship between preprocessing and fully succinct SNARKs, and who showed it?
?
You can compile a preprocessing SNARK into a fully succinct SNARK.
Bitansky et al BCCT13.
<!--SR:2022-06-18,4,250-->

Does Groth16 focus on preprocessing SNARKs or fully succinct SNARKs?
?
Preprocessing SNARKs.
<!--SR:2022-06-18,4,250-->

#### Benign Relation Generators

What danger does indistinguishability obfuscation imply and who initially showed it?
?
Bitansky et al BCPR14 show that indisginguishability obfuscation implies that for every candidate SNARK there are auxiliary output distributions that enable the adversary to create a valid proof without it being possible to extract the witness.
<!--SR:2022-06-15,1,230-->

What is the strongest negative consequence of indistinguishability obfuscation and who showed it?
?
Assuming public coin differing input obfuscation and other cryptographic assumptions, Boyle and Pass BP15 show that there is an auxiliary output distribution that defeats witness extraction for all candidate SNARKs.
<!--SR:2022-06-15,1,230-->

How do we get around impossibility results about relation generators' auxiliary input, and witness extraction?
?
Since those results rely on specific auxiliary input distributions, we can assume that the relationship generator is benign in the sense that the relation and hte auxiliary input are distributed in such a way that SNARKs can exist.
<!--SR:2022-06-16,2,250-->

## Quadratic Arithmetic Programs

### Circuits

What does our arithmetic circuit consist of?
?
Addition and multiplication gates over a finite field.
<!--SR:2022-06-27,31,250-->

What represents the statement in our arithmetic circuit?
?
Some subset of the the input/ouput wires.
<!--SR:2022-07-02,29,210-->

%% Why? Requiring input and output wires allows the other wires to act as a constraint on the possible statements that can be proven.%%

What represents the witness in our arithmetic circuit?
?
The wires that aren't the statement.
<!--SR:2022-06-23,24,210-->

What does binary relation of our arithmetic circuit consist of?
?
Statement wires and witness wires that satisfy the arithmetic circuit.
<!--SR:2022-06-29,32,250-->

### Arithmetic Constraints

What is the generalisation for circuits?
?
Arithmetic constraints - relations described by equations over a set of variables.
<!--SR:2022-06-30,33,250-->

What corresponds to the statement in our arithmetic constraints?
?
A subset of the variables.
<!--SR:2022-06-29,32,250-->

What corresponds to the witness in our arithmetic constraints?
?
The variables not in the statement.
<!--SR:2022-07-04,25,230-->

What is the binary relation of our arithmetic constraints?
?
WItnesses and statements that satisfy all the equations.
<!--SR:2022-06-28,32,250-->

What are our arithmetic constraints over?
?
$a_0 = 1$ and $a_1,...,a_m \in \mathbb{F}$
<!--SR:2022-06-16,19,210-->

What is the form of our arithmetic constraints?
?
$\sum a_iu_{i,q}\sum a_iv_{i,q}=\sum a_iw_{i,q}$,
where $u_{i,q},v_{i,q},w_{i,q}$ are constants specifying the $q$th equation.
<!--SR:2022-06-20,25,250-->

### Generalising Circuits

How do we know arithmetic constraints generalise circuits?
?
Multiplication and addition gates are special cases of constraint equations.
<!--SR:2022-07-01,34,250-->

How can a multiplication gate be described as a constraint?
?
$a_i \cdot a_j = a_k$, i.e, and equation where $u_i = v_j = w_k = 1$ and the remaining constants for the equation are $0$.
<!--SR:2022-06-18,24,250-->

How can an addition gate be described as a constraint?
?
$(a_i + a_j) \cdot a_0 = a_k$ where $u_i = u_j = v_0 = w_k = 1$, since $a_0 = 1$ by definition.
<!--SR:2022-06-26,30,250-->

In what sense are addition gates handled "for free?"
?
If $a_i + a_j = a_k$ and $a_k$ is multiplied by $a_l$, we write $(a_i + a_j) \cdot a_l$ and skip the calculation of $a_k$.
<!--SR:2022-06-24,28,250-->

### Formulating QAPs

What can we reformulate arithmetic constraints as, and what assumption do we have to make?
?
As a quadratic arithmetic program.
That the field $\mathbb{F}$ is large enough.
<!--SR:2022-06-17,3,250-->

Who introduced the idea of quadratic arithmetic programs?
?
Gennaro et al GGPR13.
<!--SR:2022-06-15,1,230-->

What are the steps in reformulating arithmetic constraints as a quadratic arithmetic program?
?
Picking a random vector.
Forming $t(x)$.
Creating the $u_i(x), v_i(x), w_i(x)$ polynomials.
Expressing the constraints as an evaluation of a single polynomial.
Refomulating the polynomial evaluation over values mod $t(x)$.
<!--SR:2022-06-15,1,230-->

What is the random vector?
?
Given $n$ equations, we pick arbitrary distinct $r_1,...,r_n \in \mathbb{F}$
<!--SR:2022-06-17,3,250-->

How is $t(x)$ defined?
?
$t(x) = \prod_{q=1}^n(x-r_q)$
<!--SR:2022-06-18,4,250-->

What are $u_i(x), v_i(x), w_i(x)$ and how are they defined?
?
They are degree $n-1$ polynomials such that for $i=0,...,m, q=1,...n$:
$u_i(r_q) = u_{i,q}$
$v_i(r_q) = v_{i,q}$
$w_i(r_q) = w_{i,q}$
<!--SR:2022-06-15,1,230-->

??? why does q start at 1 but i starts at 0? Is it that there are m+1 variables and n equations?

What is the condition that follows from an arithmetic constraint's constants being replaced by polynomials?
?
$a_0 = 1$ and the variables $a_1, ..., a_m$ satisfy the n equations if and only if at each point $r_1, ..., r_q$
$$\sum_{i=0}^ma_iu_i(r_q)\cdot \sum_{i=0}^ma_iv_i(r_q) = \sum_{i=0}^ma_iw_i(r_q)$$
<!--SR:2022-06-15,1,230-->

??? is it supposed to say "each $r_1, ..., r_n$?"

What is the final form of a quadratic arithmetic program?
?
$$\sum_{i=0}^ma_iu_i(X)\cdot \sum_{i=0}^ma_iv_i(X) \equiv \sum_{i=0}^ma_iw_i(X)\pmod{t(X)}$$
<!--SR:2022-06-15,1,230-->

How do we know that the condition evaluated at each $r_q$ is equivalent to the condition evaluated at every $t(X)$ all $\pmod{t(X)}$?
?
$t(X)$ is the lowest degree monomial with $t(r_q) = 0$ for each $r_q$.
Let $LHS = a(x)$ and $RHS = b(x)$
$a(X) \equiv b(X) \pmod{t(X)} \implies \exists k \in \mathbb{N} : a(X) + k \cdot t(X) = b(X)$ from the definition of mod
Which is true when $k \cdot t(X)$ is $0$, i.e., at each point $r_q$.
<!--SR:2022-06-18,4,250-->

UNFINISHED
## Linear Interactive Proofs
UNFINISHED