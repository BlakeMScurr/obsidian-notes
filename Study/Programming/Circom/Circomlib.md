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
<!--SR:!2023-06-16,144,170-->

### binsum

What is binsum?
?
Creates a constraint specifying that some binary inputs add to some binary output.
<!--SR:!2024-02-27,400,250-->

What is `ops` in binsum?
?
The parameter specifying the number of operands. I.e., the number of binary numbers being added together.
<!--SR:2023-03-18,183,250-->

What is `n` in binsum?
?
The parameter specifying the number of bits in each operand (binary number being added together).
<!--SR:2023-06-18,243,250-->

What does `e` specifiy in the binsum constraints?
?
The number of carries required. I.e, the possible number of extra bits required to store the output compared to each input number.
<!--SR:!2023-07-16,174,210-->

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
<!--SR:2023-06-13,238,250-->

What is the secondary constraint in binsum and what is it for?
?
Ensuring the output is in binary.
```
out[0] * (out[0] - 1) === 0;
out[1] * (out[1] -	1) === 0;
...
out[n+e-1] * (out[n+e-1] - 1) === 0;
```
<!--SR:!2023-08-26,215,230-->

What are the top level constructions in the binsum.circom file?
?
The `nbits` function and the `BinSum` template.
<!--SR:2023-04-01,193,250-->

Does `BinSum` check that inputs are binary?
?
No.
<!--SR:2023-04-22,181,230-->

What does `nbits` do?
?
Calculates the number of bits in the output required to hold a given value, namely the largest possible sum.
<!--SR:!2024-02-11,375,250-->

What do `a`, `r`, and `n` represent in `nbits`?
?
`a` is the number we're trying to represent in binary
`r` is the number of bits required
`n` is `2^r`
<!--SR:!2023-03-27,63,230-->

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
<!--SR:!2023-03-28,112,230-->

What is `nout` in `Binsum`?
?
The number of bits required to represent the output of the sum.
<!--SR:2023-06-11,237,250-->

What are `in` and `out` in `Binsum`?
?
`in` is a 2D array of bits representing binary numbers.
`out` is an array bits representing a number, namely the sum of the numbers in `in`.
<!--SR:2023-04-09,194,250-->

What are `lin` and `lout` in `Binsum`?
?
`lin` is the algebraic expression for the sum of the numbers in `in`.
`lout` is the algebraic expression for the value of `out`
<!--SR:!2023-07-13,219,230-->

??? does the l in lin and lout represent "algebra?"

What are `k` and `j` in `Binsum`?
?
`k` is the index variable used to count through the `n` digits of each `in` number, and the `nout` digits of `out`.
`j` is the index variable used to count through the `ops` operands in `in`.
<!--SR:2023-06-19,244,250-->

What is `e2` in `Binsum`?
?
`e2` is the variable that keeps track of the power of 2 represented by each digit to save exponentiations.
<!--SR:2023-06-20,245,250-->

What are the knowns and unknowns in `Binsum`?
?
`n`, `ops`, `nout`, `k`, `j`, and `e2` are known.
`in`, `lin`, `out`, and `lout` are unknown
<!--SR:!2023-02-13,7,150-->

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
<!--SR:!2023-03-21,57,210-->

### binsub

What is binsub?
?
Creates a constraint specifying that A - B = C for A, B, C binary numbers
<!--SR:2023-02-23,185,270-->

### compconstant

What is compconstant?
?
Returns 1 if the binary input signal is greater than some constant.
<!--SR:2023-06-14,239,250-->

What are the sections in compconstant?
?
Initialisation
Buliding a part
looping along the bitstring
Checking the 127th bit
Output
<!--SR:!2024-02-06,375,250-->

What are the signals in compconstant?
?
```
signal input in[254];
signal output out;
signal parts[127];
signal sout;
```
<!--SR:!2023-04-04,71,130-->

What are the variables in compconstant?
?
```
var clsb;
var cmsb;
var slsb;
var smsb;
var sum = 0;
var b = (1 << 128) - 1;
var a = 1;
var e = 1;
var i;
```
<!--SR:2023-02-18,155,230-->

What do `clsb` etc represent?
?
Constant/signal least/most significant bit.
<!--SR:2023-03-25,184,250-->

How do we calculate `clsb` etc?
?
```
clsb = (ct >> (i*2) & 1;
cmsb = (ct >> (i*2+1)) & 1;
slsb = in[i*2];
smsb = in[i*2+1];
```
<!--SR:!2023-03-15,116,230-->

What does each part resolve to, and when?
?
`a` if the constant is larger, `b` if the signal is larger, `0` if they are equal.
<!--SR:2023-04-06,170,250-->

What does `a` look like and what is its formula?
?
00000010000, where the 1 is at the ith digit
2^i
<!--SR:!2024-01-21,363,250-->

What does `b` look like and what is its formula?
?
1111110000 where the last 1 is the ith digit.
(2^127-1) - (2^(i-1) - 1)
<!--SR:2023-02-26,172,270-->

What does `a` do from a bitwise perspective and how?
?
Zeroes each `jth` left hand bit where `i < j <= 127`.
Either they're all 0, in which case it has no effect, or they're all 1, and they cascade to zero, leaving some value in bits 128 and above.
<!--SR:2023-06-05,230,250-->

What does `b` do from a bitwise perspective and how?
?
Turns each `jth` left hand bit to `1`, where `i < j <= 127`.
If they're all 0, simply by adding a 1 to each bit.
If they'll all 1, then we turn them all to `0` in a cascade by adding 1 to the `ith` bit in the same way as `a`, then we add 1 to each following bit up to `127`.
<!--SR:!2024-07-08,525,290-->

What are the 4 cases for defining parts?
?
```
cmsb == 0 && clsb == 0
cmsb == 0 && clsb == 1
cmsb == 1 && clsb == 0
cmsb == 1 && clsb == 1
```
<!--SR:!2024-03-29,431,270-->

What is `part[i]` if `cmsb == 0 && clsb == 0`, how do we know?
?
`-b*smsb*slsb + b*smsb + b*slsb`
It must be `0` if `smsb == slsb == 0`
`b` otherwise.
<!--SR:2023-02-07,158,250-->

What is `part[i]` if `cmsb == 0 && clsb == 1`, how do we know?
?
`a*smsb*slsb - a*slsb + b*smsb - a*smsb + a`
It must be `a` if `smsb == slsb == 0`
It must be `0` if `smsb == 0` and `slsb == 1`
It must be `b` if `smsb == 1` and `slsb == 0`
It must be `b` if `smsb == 1` and `slsb == 1`
<!--SR:!2023-03-26,110,230-->


What is `part[i]` if `cmsb == 1 && clsb == 0`, how do we know?
?
`b*smsb*slsb - a*smsb + a`
It must be `a` if `smsb == 0` and `slsb == 0`
It must be `a` if `smsb == 0` and `slsb == 1`
It must be `0` if `smsb == 1` and `slsb == 0`
It must be `b` if `smsb == 1` and `slsb == 1`
<!--SR:!2023-12-25,336,230-->

What is `part[i]` if `cmsb == 1 && clsb == 1`, how do we know?
?
`-a*smsb*slsb + a`
It must be `a` if `smsb == 0` and `slsb == 0`
It must be `a` if `smsb == 0` and `slsb == 1`
It must be `a` if `smsb == 1` and `slsb == 0`
It must be `0` if `smsb == 1` and `slsb == 1`
<!--SR:2023-04-04,188,250-->

What is the updating code for each loop?
?
```
sum = sum + parts[i];
b = b -e;
a = a+e;
e = e*2;
```
<!--SR:2023-02-13,116,210-->

What is the code for the final check and output?
?
```
sout <== sum;
component num2bits = Num2Bits(135);
num2bits.in <== sout;
out <== num2bits.out[127];
```
<!--SR:!2023-03-23,59,210-->

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
<!--SR:!2023-02-16,14,130-->

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
<!--SR:!2023-02-10,18,150-->

### Mux1

What are the top level constructs in Mux1?
?
`template MultiMux1` and `template Mux1`
<!--SR:2023-04-28,221,270-->

What does `MultiMux1` do?
?
Selects 1 of 2 length n arrays.
<!--SR:!2024-01-22,364,250-->

What does `Mux1` do?
?
Selects 1 of 2 values.
<!--SR:2023-06-12,237,250-->

What is the code for MultiMux1?
?
```
template MultiMux2(n) {
	signal input in[n][2];
	signal input s;
	signal out[n];
	
	for (var i = 0; i < n; i++) {
		out[i] <== (in[i][1] - in[i][0])*s + in[i][0];
	}
}
```
<!--SR:2023-02-08,105,210-->

What is the code for Mux1?
?
```
template Mux1() {
	signal input in[2];
	signal input s;
	signal output out;
	
	component mux = MultiMux1(1);
	for(var i = 0; i < 2; i++) {
		mux.in[0][i] <== in[i];
	}
	
	mux.s <== s;
	out <== mux.out[0];
}
```
<!--SR:!2023-07-07,165,170-->

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
<!--SR:!2023-03-22,51,150-->