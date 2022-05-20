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

# binsum

What is binsum?
?
Creates a constraint specifying that some binary inputs add to some binary output.

What is `ops` in binsum?
?
The parameter specifying the number of operands. I.e., the number of binary numbers being added together.

What is `n` in binsum?
?
The parameter specifying the number of bits in each operand (binary number being added together).

What does `e` specifiy in the binsum constraints?
?
The number of carries required. I.e, the possible number of extra bits required to store the output compared to each input number.

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

What is the secondary constraint in binsum and what is it for?
?
Ensuring the output is in binary.
```
out[0] ** (out[0] - 1) === 0;
out[1] ** (out[1] -	1) === 0;
...
out[n+e-1] ** (out[n+e-1] - 1) === 0;
```

What are the top level constructions in the binsum.circom file?
?
The `nbits` function and the `BinSum` template.

Does `BinSum` require binary inputs?
?
No.

What does `nbits` do?
?
Calculates the number of bits in the output required to hold a given value, namely the largest possible sum.

What do `a`, `r`, and `n` represent in `nbits`?
?
`a` is the number we're trying to represent in binary
`r` is the number of bits required
`n` is the `2^r`

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

What is `nout` in `Binsum`?
?
The number of bits require

What are `in` and `out` in `Binsum`?
?

What are `lin` and `lout` in `Binsum`?
?

What are `k` and `j` in `Binsum`?
?

What is `e2` in `Binsum`?
?

What are the knowns and unknowns in `Binsum`?
?

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

## g-m

What are the files starting with g-m?
?
gates
mimc
mimcsponce
montgomery
multiplexer
mux1
mux2
mux3
mux4

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