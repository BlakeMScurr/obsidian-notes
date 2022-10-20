#flashcards/cryptography/keccak_paar

# Hash Functions

## Motivating Examples

What is the motiviating example for hash functions?
?
Hashing a message to be signed
<!--SR:2022-10-22,2,250-->

What's the naive approach to signing long messages?
?
Signing each chunk individually.
<!--SR:2022-10-22,2,250-->

What are the main problems with the naive approach to signing long messages?
?
Rearrangement.
Cost.
Overheard.
<!--SR:2022-10-23,3,250-->

What's the non naive approach to signing long messages?
?
Hash the message then sign the hash.
<!--SR:2022-10-24,4,250-->

## Properties of Hash Functions

What are our length requirements for a hash function for messages?
?
Arbitrary length inputs.
Fixed small length outputs.
<!--SR:2022-10-22,2,250-->

What are the efficiency requirements for a message hash function?
?
Should be fast (much faster than signatures).
<!--SR:2022-10-24,4,250-->

What are the security requirements for a message hash function?
?
Preimage resistance.
Second preimage resistance.
Collision resistance.
<!--SR:2022-10-21,1,230-->

What is preimage resistance also known as?
?
One-wayness
<!--SR:2022-10-21,1,230-->

What does preimage resistance mean?
?
That we can't compute $x$ from $h(x)$.
<!--SR:2022-10-24,4,250-->

What does preimage mean, simply?
?
Input
<!--SR:2022-10-23,3,250-->

What does second preimage resistance mean?
?
An attacker can't compute $x_2$ such that $h(x_2) = z$ given $x_1$ such that $h(x_1) = z$
<!--SR:2022-10-24,4,250-->

What's the online banking example where second preimage resistance is important?
?
Bob signs that he gives $10 to Oscar, if Oscar can find a message that hashes to the same value as the signed message, he can get the bank to accept that instead.
<!--SR:2022-10-25,5,270-->

What is another phrase for second preimage resistant?
?
Weak collision resistance.
<!--SR:2022-10-24,4,250-->

What is the difference between collision resistance and second preimage resistance?
?
in second preimage resistance we have a fixed message we're trying to find a collision for.
<!--SR:2022-10-22,2,250-->

??? Does collision resistance imply second preimage resistance?

### Collision Attack

What is an example of a collision attack (where a hash function doesn't have collision resistance)?
?
Suppose an attacker (think of a malicious crypto site) gets someone to sign the hash of a benign transaction, i.e., a swap they want to do. The malicious site gets metamask to show the benign transaction. However, there is another malicious transaction that hashes to the same value, so the malicious site can send that to the blockchain instead (racing metamask and the user to the chain).
<!--SR:2022-10-24,4,250-->

Which is easier to perform, a collision attack, or a second preimage attack, and by how much?
?
Collision attacks take the square root of the amount of steps as a preimage attack.
<!--SR:2022-10-23,3,250-->

Can you build a hash function without collisions?
?
No.
<!--SR:2022-10-23,3,250-->

Why do all hash functions have collisions?
?
Because the input space is of arbitrary length, and the output is fixed.
<!--SR:2022-10-24,4,250-->

if all hash functions have collisions, how can we show collision/preimage resistance etc?
?
By making it *hard* to create collisions, rather than impossible.
<!--SR:2022-10-24,4,250-->

Suppose a hash function has a range of size n = 2^b, what is the *approximate and natural* number of times that an attacker needs to run the hash to brute force a second preimage collision? If they do that, what is the exact probability they have  a collision, and the limit of that probability as n approaches infinity?
?
Run the hash $~n$ times
Giving an exact probability of $1 - [\frac{(n-1)}{n}]^n$ 
With a limit of $1 - \frac{1}{e} \approx 1 - 0.3679 = 0.6321$
<!--SR:2022-10-21,1,230-->

How does the birthday problem apply to hash functions?
?
It's equivalent to the problem of finding a hash collision.
<!--SR:2022-10-22,2,250-->

What is the probability:
That 2 people in a room share a birthday?
That 3 people in a room share a birthday?
That t people in a room share a birthday?
?
$1 - \frac{1}{365}$
$(1 - \frac{1}{365})(1 - \frac{2}{365})$
$\Pi_{i=1}^{t-1}(1 - \frac{i}{365})$
<!--SR:2022-10-21,1,230-->

What is the exact formula for number of hashes required to achieve a collision, given the number of bits in the output, and the probability with which a collision should be achieved?
?
$t = 2^{\frac{n+1}{2}}\sqrt{ln(\frac{1}{1-\lambda})}$
Where: 
	$t$ is the number of hashes
	$n$ is the number of bits in the output
	$\lambda$ is the probability with which at least one collision occurs between at least two values
<!--SR:2022-10-21,1,230-->


# SHA-3

## Background

What standards and defacto standards preceeded SHA-3?
?
MD4, MD5, SHA-1, and SHA-2
<!--SR:2022-10-22,2,250-->

What is the name of the hash that won the SHA-3 competition?
?
Keccak
<!--SR:2022-10-24,4,250-->

What are the possible SHA-3 output lengths?
?
224, 256, 384, and 512
<!--SR:2022-10-21,1,230-->

Why are 224 and 384 chosen as SHA-3 output lengths?
?
224 bits has the same strength as triple DES
The other security levels have the same strength as forms of AES
<!--SR:2022-10-24,4,250-->

## Keccak Sponge

What kind of construction does keccak use?
?
A sponge construction.
<!--SR:2022-10-22,2,250-->

Why is it called a "sponge" construction?
?
Because it has an absorbtion phase (like absorbing the water), and a squeezing phase (like squeezing water out).
<!--SR:2022-10-22,2,250-->

What are the phases of a sponge construction?
?
Absorbtion (taking in input bits)
Squeezing (output is produced)
<!--SR:2022-10-22,2,250-->

What are the internal parameters of keccak?
?
The state length $b$ 
The number of rounds $n_r$
The bitrate, or output block size $r$
The capacity $c$
<!--SR:2022-10-21,1,230-->

What are the parameters of SHA-3?
?
$b = 1600$
$n_r = 24$
output length $\in \{224, 256, 348, 512\}$
$r \in \{1152, 1085, 832, 576\}$
$c \in \{448, 512, 768, 1024\}$
<!--SR:2022-10-21,1,230-->

What does $b$ represent?
?
The state length.
<!--SR:2022-10-24,4,250-->

What formula does $b$ follow, and what are its possible values?
?
$b = 25 * 2^l$ where $l \in {0,1,2,3,4,5,6}$
${25, 50, 100, 200, 400, 800, 1600}$
<!--SR:2022-10-21,1,230-->

What is the relationship between keccak and SHA-3?
?
Keccak is a family of functions that includes SHA-3, namely for SHA-3, $b=1600$
<!--SR:2022-10-24,4,250-->

What does $n_r$ represent?
?
The number of rounds
<!--SR:2022-10-24,4,250-->

What is the relationship between $b$, $c$, and $r$?
?
$b = r + c$
<!--SR:2022-10-23,3,250-->

How do you make keccak into a PRNG?
?
By continuing to squeeze to create arbitrary length outputs.
<!--SR:2022-10-22,2,250-->

What is the main purpose of the preprocessing step in keccak?
?
Padding.
<!--SR:2022-10-22,2,250-->

How many times do we run the absorbtion phase (i.e., run the $f$ function and `XOR` the new input)?
?
As many times as required to get the entire input in.
I.e., for an input with $m$ bits, it takes $m/r$ rounds.
<!--SR:2022-10-23,3,250-->

If we output too many bits from the end of the absorbtion phase, how do we reduce the number to the appropriate length, (like is required in SHA-3)?
?
Just truncate it.
<!--SR:2022-10-24,4,250-->

## Keccak-f

What is the keccak-f function broken down into?
?
Rounds.
<!--SR:2022-10-24,4,250-->

How many rounds in the keccak-f function?
?
$r$ (24 in SHA-3)
<!--SR:2022-10-23,3,250-->

What is the input and output size of keccak-f?
?
$b$ for bouth input and output (1600 in SHA-3)
<!--SR:2022-10-23,3,250-->

What is the round function of keccak-f broken down?
?
5 atomic functions:
$\theta, \rho, \pi, \chi, \iota$
Theta, rho, pi, chi, and iota
<!--SR:2022-10-21,1,230-->

What is the input and output size of the sub functions of the keccak-f round functions?
?
Same as the round function, $b$ for both input and output (1600 for SHA-3)
<!--SR:2022-10-23,3,250-->

How should we view the $b = 1600$ bit state, to make sense of the $\theta ... \iota$ functions?
?
As a 3-dimensional array
A cube with a 5x5 face and a depth of 64 where each sub-cube has 1 bit
<!--SR:2022-10-22,2,250-->

#### Greek Functions

What does $theta$ do, roughly?
?
Each of the $b$ (think $1600$) state bits is replaced by the XOR sum of 11 bits.
<!--SR:2022-10-21,1,230-->

Which 11 bits are used by $theta$ and how are they combined?
?
The original bit, the 5 bit column "to the left" of the bit  , and the 5 bit column "to the right and one position to the front" of the bit
original plus/XOR left plus/XOR
<!--SR:2022-10-23,3,250-->

What do $\rho$ and $\pi$ operate on?
?
64 bit words
<!--SR:2022-10-23,3,250-->

 What are the inputs and outputs of $\rho$ and $\pi$?
 ?
 An array of $[x,y]$ coordinates where $x,y \in 0,1,2,3,4$
The input is called $A$ and the output is called $B$

Why is $\rho$ named $\rho$?
?
Because it involves rotation
<!--SR:2022-10-23,3,250-->

What does $rho$ do?
?
Rotates each word by a fixed number of positions (defined by a fairly arbitrary looking table).
<!--SR:2022-10-22,2,250-->

What do they call a word in the keccak document?
?
A lane
<!--SR:2022-10-23,3,250-->

What does $\pi$ do?
?
Permutes all the words using a simple relation
<!--SR:2022-10-22,2,250-->

What does $\chi$ do?
?
Combines each 3 adjacent bits of each words using `AND, NOT, and XOR`
<!--SR:2022-10-23,3,250-->

What does $\iota$ do?
?
Adds constants from a constant table to $A[0,0]$, where there is a different constant for each round
<!--SR:2022-10-21,1,230-->




