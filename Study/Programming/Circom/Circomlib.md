#flashcards/circom/circomlib

# Circuits
## a-c

What are the files starting with a-c?
?
aliascheck
babyjub
binsub
binsum
bitify
comparators
compconstant
<!--SR:2022-05-24,1,170-->

What is aliascheck?
?

### Aliascheck

What is aliascheck?
?
Checks that a binary number is positive.

### binsum

What is binsum?
?
Creates a constraint specifying that some binary inputs add to some binary output.
<!--SR:2022-05-24,3,230-->

What is `ops` in binsum?
?
The parameter specifying the number of operands. I.e., the number of binary numbers being added together.
<!--SR:2022-05-24,4,250-->

What is `n` in binsum?
?
The parameter specifying the number of bits in each operand (binary number being added together).
<!--SR:2022-05-24,4,250-->

What does `e` specifiy in the binsum constraints?
?
The number of carries required. I.e, the possible number of extra bits required to store the output compared to each input number.
<!--SR:2022-05-24,4,250-->

What is the main constraint in binsum and what is it for?
?
Confirming the inputs sum to the output.
```
in[0][0]*2^0 + i[0][1]*2^1 + ... in[0][n-1]*2^(n-1) +
in[1][0]*2^0 + i[1][1]*2^1 + ... in[1][n-1]*2^(n-1) +
...
in[ops-1][0]*2^0 + i[ops-1][1]*2^1 + ... in[ops-1][n-1]*2^(n-1)
===
out[0]+2^0 + out[1]^2^1 + ..... + out[n+e-1]*2^(n+e-1)
```
<!--SR:2022-05-24,4,250-->

What is the secondary constraint in binsum and what is it for?
?
Ensuring the output is in binary.
```
out[0] * (out[0] - 1) === 0;
out[1] * (out[1] -	1) === 0;
...
out[n+e-1] * (out[n+e-1] - 1) === 0;
```
<!--SR:2022-05-24,4,250-->

What are the top level constructions in the binsum.circom file?
?
The `nbits` function and the `BinSum` template.
<!--SR:2022-05-24,4,250-->

Does `BinSum` require binary inputs?
?
No.
<!--SR:2022-05-24,4,250-->

What does `nbits` do?
?
Calculates the number of bits in the output required to hold a given value, namely the largest possible sum.
<!--SR:2022-05-24,4,250-->

What do `a`, `r`, and `n` represent in `nbits`?
?
`a` is the number we're trying to represent in binary
`r` is the number of bits required
`n` is the `2^r`
<!--SR:2022-05-24,4,250-->

What is the code for `nbits`?
?
```
function nbits(a) {
	var r = 0;
	var n = 1;
	while (n-1<a) {
		r++;
		n *= 2;
	}
	return r;
}
```
<!--SR:2022-05-24,4,250-->

What is `nout` in `Binsum`?
?
The number of bits required to represent the output of the sum.
<!--SR:2022-05-24,4,250-->

What are `in` and `out` in `Binsum`?
?
`in` is a 2D array of bits representing binary numbers.
`out` is an array bits representing a number, namely the sum of the numbers in `in`.
<!--SR:2022-05-24,4,250-->

What are `lin` and `lout` in `Binsum`?
?
`lin` is the algebraic expression for the sum of the numbers in `in`.
`lout` is the algebraic expression for the value of `out`
<!--SR:2022-05-24,4,250-->

??? does the l in lin and lout represent "algebra?"

What are `k` and `j` in `Binsum`?
?
`k` is the index variable used to count through the `n` digits of each `in` number, and the `nout` digits of `out`.
`j` is the index variable used to count through the `ops` operands in `in`.
<!--SR:2022-05-24,4,250-->

What is `e2` in `Binsum`?
?
`e2` is the variable that keeps track of the power of 2 represented by each digit to save exponentiations.
<!--SR:2022-05-24,4,250-->

What are the knowns and unknowns in `Binsum`?
?
`n`, `ops`, `nout`, `k`, `j`, and `e2` are known.
`in`, `lin`, `out`, and `lout` are unknown
<!--SR:2022-05-24,4,250-->

What is the code for `BinSum`?
?
```
template BinSum(n, ops) {
	var nout = nbits((2**n - 1) * ops);
	signal in[ops][n];
	signal out[nout];
	
	var lin = 0;
	var lout = 0;
	
	var k;
	var j;
	
	var e2 = 1;
	for(k=0; k<n; k++) {
		for (j=0; j<ops; j++) {
			lin += in[j][k] * e2;
		}
		e2 *= 2;
	}
	
	e2 = 1;
	for (k=0; k<nout; k++) {
		out[k] <-- (lin >> k) & 1;
		out[k] * (out[k] - 1) === 0;
		lout += out[k] * e2;
		e2 *= 2;
	}
	
	lin === lout;
}
```
<!--SR:2022-05-24,4,250-->

### binsub

What is binsub?
?
Creates a constraint specifying that A - B = C for A, B, C binary numbers

### compconstant

What is compconstant?
?
Returns 1 if the binary input signal is greater than some constant.

## e

What are the files starting with e?
?
eddsa
eddsamimc
eddsamimcsponge
eddsaposeidon
escalarmul
escalarmulany
escalarmulfix
escalarmulw4table
<!--SR:2022-05-24,1,230-->

## g-m

What are the files starting with g-m?
?
gates
mimc
mimcsponge
montgomery
multiplexer
mux1
mux2
mux3
mux4
<!--SR:2022-05-24,4,250-->

## p-s

What are the files starting with p-s?
?
pedersen
pedersen_old
pointbits
poseidon
poseidon_constants
poseidon_constants_old
poseidon_old
sign
switcher
<!--SR:2022-05-24,1,170-->