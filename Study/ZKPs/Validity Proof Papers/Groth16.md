#flashcards/zkps/Groth16
# Abstract

What makes SNARGs succinct?
?
Small size and low verification complexity.
<!--SR:2022-05-24,8,210-->

What is a SNARG?
?
Succinct non-interactive argument
<!--SR:2022-05-20,8,250-->

What is a SNARK?
?
Succinct non-interactive argument of knowledge
<!--SR:2022-05-25,12,250-->

What does a pairing based SNARG consist of?
?
A number of group elements.
<!--SR:2022-05-25,12,250-->

What is the central question of Groth16?
?
How efficient can pairing based SNARGs be?
<!--SR:2022-05-23,7,230-->

What language is Groth16's SNARG for, and what is that language's most important property?
?
Circuit satisfiability, that it is NP-complete.
<!--SR:2022-05-22,9,250-->

What kind of pairings does Groth16 use and why?
?
Assymetric pairings for higher efficiency.
<!--SR:2022-05-23,10,250-->

What does a Groth16 SNARG consist of?
?
3 group elements.
<!--SR:2022-05-21,9,250-->

What does verifying a Groth16 SNARG require?
?
Checking a single pairing product equation using 3 pairings in total.
<!--SR:2022-05-26,10,210-->

What is the knowledge complexity of the Groth16 SNARG?
?
It is zero knowledge.
<!--SR:2022-05-30,12,230-->

What is the second contribution of Groth16 and how is it shown?
?
That SNARGs using generic symmetric bilinear group operations can't consist of a single element.
By showing that linear interactive proofs cannot have a linear decision procedure.
<!--SR:2022-05-22,6,210-->

What would extending the lower bound in Groth16 prove?
?
Extending the lower bound to 2 elements would prove the optimality of the 3 element SNARG.
<!--SR:2022-05-24,11,250-->

Who posed the question answered by Groth16's second contribution?
?
Nir Bitansky, Allesandro Chisea, Yuval Ishai, Rafail Ostrovsky, and Omer Paneth.
<!--SR:2022-05-19,3,150-->

# Introduction

Who introduced zero-knowledge proofs?
?
Shafi Goldwasser, Silvio Micali, and Charles Rackoff.
<!--SR:2022-05-23,11,270-->

What are the 3 core properties of zero knowledge proofs?
?
Completeness, Soundness, and Zero-Knowledge.
<!--SR:2022-06-01,15,250-->

Describe the completeness property.
?
Given a statement and a witness, the prover can convince the verifier.
<!--SR:2022-05-21,5,190-->

Describe the soundness property.
?
A malicious prover cannot convince the verifier of a false statement.
<!--SR:2022-05-31,15,250-->

Describe the zero knowledge property.
?
The proof does not reveal anything but the truth of the statement, in particular it does not reveal the prover's witness.
<!--SR:2022-05-24,8,190-->

How did Blum, Feldman, and Micali extend the notion of interactive proofs?
?
To non-interactive zero knowledge proofs (NIZK) in the common reference string model.
<!--SR:2022-05-22,10,250-->

Where are NIZKs useful, according to Groth16?
?
The construction of non-interactive cryptographic schemes, e.g., digital key signatures, and CCA-secure public key encryption.
<!--SR:2022-05-25,9,190-->

Where was the first sub-linear communication zero-knowledge argument, sending fewer bits than the size of the statement given?
?
Kili92, by Joe Kilian.
<!--SR:2022-05-23,7,190-->

What did Micali00 propose?
?
Sublinear size NIZK arguments by letting the prover in a communication efficient zero-knowledge argument compute the verifier's challenges using a cryptographic function.
<!--SR:2022-05-19,3,150-->

Which papers introduced pairing based NIZKs, and what did this yield?
?
Groth et al: GOS12, GOS06, Gro06, GS12.
The first linear sized proofs based on standard assumptions.
<!--SR:2022-05-19,1,130-->

What did Gro10 achieve wrt communication complexity?
?
Combined pairing based NIZKs with ideas from interactive zero-knowledge to give the first constant size NIZK arguments.
<!--SR:2022-05-19,2,210-->

What did Lip12 achieve wrt communication complexity?
?
Constant size NIZK arguments based on progression-free sets to reduce the size of the common reference string.
<!--SR:2022-05-19,1,130-->

What is Groth's constant size NIZK based on?
?
Constructing a set of polynomial equations and using pairings to efficiently verify these equations.
<!--SR:2022-05-24,8,190-->

UNFINISHED

# Preliminaries
## Notation
UNFINISHED
## Bilinear Groups
UNFINISHED
## Non-interactive Zero-Knowledge Arguments of Knowledge
UNFINISHED
## Quadratic Arithmetic Programs

### Circuits

What does our arithmetic circuit consist of?
?
Addition and multiplication gates over a finite field.
<!--SR:2022-05-27,11,250-->

What represents the statement in our arithmetic circuit? Why?
?
Some subset of the the input/ouput wires. Requiring input and output wires allows the other wires to act as a constraint on the possible statements that can be proven.
<!--SR:2022-05-21,5,210-->

What represents the witness in our arithmetic circuit?
?
The wires that aren't the statement.
<!--SR:2022-05-20,4,210-->

What does binary relation of our arithmetic circuit consist of?
?
Statement wires and witness wires that satisfy the arithmetic circuit.
<!--SR:2022-05-28,12,250-->

### Arithmetic Constraints

What is the generalisation for circuits?
?
Arithmetic constraints - relations described by equations over a set of variables.
<!--SR:2022-05-28,12,250-->

What corresponds to the statement in our arithmetic constraints?
?
A subset of the variables.
<!--SR:2022-05-28,12,250-->

What corresponds to the witness in our arithmetic constraints?
?
The variables not in the statement.
<!--SR:2022-05-26,10,250-->

What is the binary relation of our arithmetic constraints?
?
WItnesses and statements that satisfy all the equations.
<!--SR:2022-05-27,11,250-->

What are our arithmetic constraints over?
?
$a_0 = 1$ and $a_1,...,a_m \in \mathbb{F}$
<!--SR:2022-05-20,4,210-->

What is the form of our arithmetic constraints?
?
$\sum a_iu_{i,q}\sum a_iv_{i,q}=\sum a_iw_{i,q}$,
where $u_{i,q},v_{i,q},w_{i,q}$ are constants specifying the $q$th equation.
<!--SR:2022-05-26,10,250-->

### Generalising Circuits

How do we know arithmetic constraints generalise circuits?
?
Multiplication and addition gates are special cases of constraint equations.
<!--SR:2022-05-28,12,250-->

How can a multiplication gate be described as a constraint?
?
$a_i \cdot a_j = a_k$, i.e, and equation where $u_i = v_j = w_k = 1$ and the remaining constants for the equation are $0$.
<!--SR:2022-05-25,9,250-->

How can an addition gate be described as a constraint?
?
$(a_i + a_j) \cdot a_0 = a_k$ where $u_i = u_j = v_0 = w_k = 1$, since $a_0 = 1$ by definition.
<!--SR:2022-05-27,11,250-->

In what sense are addition gates handled "for free?"
?
If $a_i + a_j = a_k$ and $a_k$ is multiplied by $a_l$, we write $(a_i + a_j) \cdot a_l$ and skip the calculation of $a_k$.
<!--SR:2022-05-27,11,250-->

UNFINISHED
## Linear Interactive Proofs
UNFINISHED