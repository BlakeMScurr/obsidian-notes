#flashcards/cryptography/keccak_paar

# Hash Functions

## Motivating Examples

What is the motiviating example for hash functions?
?
Hashing a message to be signed

What's the naive approach to signing long messages?
?
Signing each chunk individually.

What are the main problems with the naive approach to signing long messages?
?
Rearrangement.
Cost.
Overheard.

What's the non naive approach to signing long messages?
?
Hash the message then sign the hash.

## Properties of Hash Functions

What are our length requirements for a hash function for messages?
?
Arbitrary length inputs.
Fixed small length outputs.

What are the efficiency requirements for a message hash function?
?
Should be fast (much faster than signatures).

What are the security requirements for a message hash function?
?
Preimage resistance.
Second preimage resistance.
Collision resistance.

What is preimage resistance also known as?
?
One-wayness

Whatdoes preimage resistance mean?
?
That we can't compute $x$ from $h(x)$.

What does preimage mean, simply?
?
Input

What does second preimage resistance mean?
?
An attacker can't compute $x_2$ such that $h(x_2) = z$ given $x_1$ such that $h(x_1) = z$

What's the online banking example where second preimage resistance is important?
?
Bob signs that he gives $10 to Oscar, if Oscar can find a message that hashes to the same value as the signed message, he can get the bank to accept that instead.

What is another phrase for second preimage resistant?
?
Weak collision resistance.

What is the difference between collision resistance and second preimage resistance?
?
in second preimage resistance we have a fixed message we're trying to find a collision for.

??? Does collision resistance imply second preimage resistance?

### Collision Attack

What is an example of a collision attack (where a hash function doesn't have collision resistance)?
?
Suppose an attacker (think of a malicious crypto site) gets someone to sign the hash of a benign transaction, i.e., a swap they want to do. The malicious site gets metamask to show the benign transaction. However, there is another malicious transaction that hashes to the same value, so the malicious site can send that to the blockchain instead (racing metamask and the user to the chain).

Which is easier to perform, a collision attack, or a second preimage attack, and by how much?
?
Collision attacks take the square root of the amount of steps as a preimage attack.

Can you build a hash function without collisions?
?
No.

Why do all hash functions have collisions?
?
Because the input space is of arbitrary length, and the output is fixed.

if all hash functions have collisions, how can we show collision/preimage resistance etc?
?
By making it *hard* to create collisions, rather than impossible.

Suppose a hash function has a range of size n = 2^b, what is the *approximate and natural* number of times that an attacker needs to run the hash to brute force a second preimage collision? If they do that, what is the exact probability they have  a collision, and the limit of that probability as n approaches infinity?
?
Run the hash $~n$ times
Giving an exact probability of $1 - [\frac{(n-1)}{n}]^n$ 
With a limit of $1 - \frac{1}{e} \approx 1 - 0.3679 = 0.6321$

How does the birthday problem apply to hash functions?
?
It's equivalent to the problem of finding a hash collision.

What is the probability:
That 2 people in a room share a birthday?
That 3 people in a room share a birthday?
That t people in a room share a birthday?
?
$1 - \frac{1}{365}$
$(1 - \frac{1}{365})(1 - \frac{2}{365})$
$\Pi_{i=1}^{t-1}(1 - \frac{i}{365})$

What is the exact formula for number of hashes required to achieve a collision, given the number of bits in the output, and the probability with which a collision should be achieved?
?
$t = 2^{\frac{n+1}{2}}\sqrt{ln(\frac{1}{1-\lambda})}$
Where: 
	$t$ is the number of hashes
	$n$ is the number of bits in the output
	$\lambda$ is the probability with which at least one collision occurs between at least two values


# SHA-3