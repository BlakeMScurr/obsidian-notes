#flashcards/halo2

# Concepts

## Proof Systems

What does a prover need to create a proof of a statement?
?
Private inputs and intemediate values called advice values.
<!--SR:2022-07-27,4,250-->

What is advice?
?
Intermediate values used to create the proof
<!--SR:2022-07-26,3,250-->

What is the witness?
?
The advice and the private inputs.
<!--SR:2022-08-07,13,270-->

## PLONKish Arithmetization

What does the configuration of a circuit include?
?
Finite field.
Number of columns and specification for each column.
Column subset that participate in equality constrains.
Maximum consraint degree.
Constraints.
Lookup arguments.
<!--SR:2022-07-26,1,190-->

What are the possible specifications for each column?
?
Fixed
Advice
Instance
<!--SR:2022-08-01,7,230-->

What is a fixed column?
?
A column whose values are fixed by the circuit.
<!--SR:2022-07-27,5,270-->

What is an advice column?
?
A column that corresponds to witness values.
<!--SR:2022-07-26,3,230-->

What is an instance column?
?
It's for elements shared between the prover and verifier, typeically public inputs.
<!--SR:2022-07-26,4,250-->

What are the constraints?
?
Multivariate polynomails over F.
<!--SR:2022-08-06,12,270-->

What do the constraints require?
?
They must evaluate to zero *for each row*.
<!--SR:2022-07-30,5,230-->

What do the variables in a polynomial constraint refer to?
?
A cell in a given column of the current row, or a given column of another row relative to the current one (with wrap-around, i.e., taken modulo n).
<!--SR:2022-07-29,4,210-->

What is the maximum degree of each polynomial?
?
The maximum constraint degree.
<!--SR:2022-07-31,6,230-->

What are lookup arguments defined over?
?
Tuples of input expressions (i.e., multivariate polynomial constraints) and table columns.
<!--SR:2022-07-26,4,250-->

What does a PLONKish circuit define in addition to the configuration?
?
The number of rows in the matrix $n$.
Equality constraints.
The values of fixed columns at each row.
<!--SR:2022-07-26,1,190-->

What keys do we genererate from the circuit description?
?
The proving key and the verification key.
<!--SR:2022-07-27,5,270-->

What is a selector?
?
A value defined in a fixed column that allows polynomial constraints to be turned on or off.
<!--SR:2022-07-30,5,250-->

How, roughly are gates implemented?
?
Sets of constraints like $q_i \cdot p(...)$, along with a set of selector columns are called a gate.
<!--SR:2022-08-02,8,250-->

??? Why is it not just a single constraint along with a selector column? Intuitively that's what a gate would be, to me.

What kinds of gates are there?
?
Standard gates that support generic field operations like multiplication and addition, and custom gates for more specialized operations.
<!--SR:2022-07-27,5,270-->

## Chips

What is the purpose of a chip?
?
To create a higher level API than the matrix view of a PLONKish circuit, offering auditability, efficiency, modularity, and expressiveness.
<!--SR:2022-07-27,5,270-->

What are some examples of things chips might do?
?
Cryptographic primitives like hash functions or ciphers, or algorithms like scalar multiplication or pairings.
<!--SR:2022-07-26,4,250-->

What is the advantage of using custom gates?
?
Efficiency. It's possible to do arbitrary logic with standard gates, but that is not the most efficient way.
<!--SR:2022-07-26,4,270-->

## Gadgets