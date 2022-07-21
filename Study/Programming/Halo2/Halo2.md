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

What is the maximum degree of each polynomial?
?
The maximum constraint degree.

## Chips

## Gadgets