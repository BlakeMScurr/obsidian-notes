#flashcards/halo2

# Concepts

## Proof Systems

What does a prover need to create a proof of a statement?
?
Private inputs and intemediate values called advice values.

What is advice?
?
Intermediate values used to create the proof

What is the witness?
?
The advice and the private inputs.

## PLONKish Arithmetization

What does the configuration of a circuit include?
?
Finite field.
Number of columns and specification for each column.
Column subset that participate in equality constrains.
Maximum consraint degree.
Consrains.
Lookup arguments.

What are the possible specifications for each column?
?
Fixed
Advice
Instance

What is a fixed column?
?
A column whose values are fixed by the circuit.

What is an advice column?
?
A column that corresponds to witness values.

What is an instance column?
?
It's for elements shared between the prover and verifier, typeically public inputs.

What are the constraints?
?
Multivariate polynomails over F.

What do the constraints require?
?
The must evaluate to zero *for each row*.

What do the variables in a polynomial constraint refer to?
?
A cell in a given column of the current row, or a given column of another row relative to the current one (with wrap-around, i.e., taken modulo n).
<!--SR:2022-07-23,1,230-->

What is the maximum degree of each polynomial?
?
The maximum constraint degree.

What are lookup arguments defined over?
?
Tuples of input expressions (i.e., multivariate polynomial constraints) and table columns.

What does a PLONKish circuit define in addition to the configuration?
?
The number of rows in the matrix $n$.
Equality constraints.
The values of fixed columns at each row.

What keys do we genererate from the circuit description?
?
The proving key and the verification key.

What is a selector?
?
A value defined in a fixed column that allows polynomial constraints to be turned on or off.

How, roughly are gates implemented?
?
Sets of constraints like $q_i \cdot p(...)$, along with a set of selector columns are called a gate.

??? Why is it not just a single constraint along with a selector column? Intuitively that's what a gate would be, to me.

What kinds of gates are there?
?
Standard gates that support generic field operations like multiplication and addition, and custom gates for more specialized operations.

## Chips

What is the purpose of a chip?
?
To create a higher level API than the matrix view of a PLONKish circuit, offering auditability, efficiency, modularity, and expressiveness.

What are some examples of things chips might do?
?
Cryptographic primitives like hash functions or ciphers, or algorithms like scalar multiplication or pairings.

What is the advantage of using custom gates?
?
Efficiency. It's possible to do arbitrary logic with standard gates, but that is not the most efficient way.

## Gadgets