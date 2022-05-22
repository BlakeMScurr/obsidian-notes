#flashcards/funmaths/aleph0/galois
# Intro

What is the Fundamental Theorem of Galois Theory about, roughly?
?
Algerbraic expressions including values like $\sqrt{2}$ and $-\sqrt{2}$, and the ways you can permute those values while keeping the expression true.
<!--SR:2022-05-25,16,270-->

What is the popularly known consequence of the Fundamental Theorem of Galois Theory?
?
That there is no general formula to solve a polynomial of degree 5 or higher.
<!--SR:2022-06-26,35,250-->


# What is the Square root of 2?

What is the square root of 2 as a truncated decimal?
?
1.41... and -1.41...
<!--SR:2022-05-27,16,230-->

Explain the "algebraic difference" between $\sqrt(2)$ and $-\sqrt{2}$.
?
There is none. Consider any true expression containing $\sqrt{2}$, it will still be true if you replace $\sqrt{2}$ with  $-\sqrt{2}$.
<!--SR:2022-06-09,24,250-->

What are basic examples of algebraic expressions that both $\sqrt{2}$ and $-\sqrt{2}$ satisfy?
?
$\sqrt{2}^2 = 2$
$(\sqrt{2})^3 = 2\sqrt{2}$
<!--SR:2022-06-08,23,230-->

What does it mean to say that $\sqrt{2}$ and $-\sqrt{2}$ are conjugate over $\mathbb{Q}$?
?
Whenever you have an equation with rational coefficients, replacing $\sqrt{2}$ with $-\sqrt{2}$ will leave the equation holding true.
<!--SR:2022-06-12,20,190-->

??? Does this mean that we can construct expressions with non rational coefficients for which $\sqrt{2}$ and $-\sqrt{2}$ are not conjugate?

What is the "basic question" of Galois Theory?
?
Given a bunch of numbers that are conjugate over $\mathbb{Q}$, how many ways are there to swap them that preserve algebraic relations?
<!--SR:2022-05-30,9,170-->

What is an example of an equation where you can swap $\sqrt{2}$ and $-\sqrt{2}$?
?
$\frac{1}{3 + 2\sqrt{2}} = [1 + (-\sqrt(2)]^2$
<!--SR:2022-06-03,17,190-->

Can we always swap $\sqrt{2}$ and $-\sqrt{2}$ in algebraic expressions with rational coefficients?
?
Yes.
<!--SR:2022-06-02,20,250-->

What is $\zeta$
?
$e^{\frac{2i\pi}{5}}$, a 5th root of unity.
<!--SR:2022-06-01,16,210-->

What are the conjugates of $\zeta$ over $\mathbb{Q}$?
?
$\zeta,\zeta^2,\zeta^3,\zeta^4$
<!--SR:2022-06-17,30,250-->

How many ways are there to permutate the conjugates of $\zeta$ over $\mathbb{Q}$, and how many of those permute algebraic relations?
?
$4! = 24$ permutations
$4$ preserve algebraic relations
<!--SR:2022-06-20,31,250-->

What are the permutations of conjugates of $\zeta$ that preserve algebraic relations?
?
$(\zeta,\zeta^2,\zeta^3,\zeta^4)$
$(\zeta^2,\zeta^4,\zeta,\zeta^3)$
$(\zeta^3,\zeta,\zeta^4,\zeta^2)$
$(\zeta^4,\zeta^3,\zeta^2,\zeta)$
<!--SR:2022-05-25,15,250-->

Why do we want to study the algebra preserving permutations of conjugates?
?
It helps to understand how numbers (like $\sqrt{2}$ and $e^{\frac{2i\pi}{5}}$) are related to each other.
<!--SR:2022-06-07,22,230-->

# Fields and Automorphisms

What is a field, roughly speaking?
?
Any set where you can add, subtract, multiply, and divide elements.
<!--SR:2022-05-30,18,250-->

Name a field (basic, but highly relevant to Galois theory)
?
The rational numbers
<!--SR:2022-06-12,27,250-->

What can't you do in a field?
?
Take square roots.
<!--SR:2022-06-20,33,250-->

What is $\mathbb{Q}(\sqrt(2)$? What does it contain?
?
The smallest field containing the rationals and $\sqrt{2}$.
Being closed under +, -, \*, and /, it contains $1+\sqrt{2}$ etc.
<!--SR:2022-06-13,27,250-->

Describe the automorphisms analogous to our non-rigorous motivating example with $\sqrt{2}$
?
Some automorphism fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$.
<!--SR:2022-06-06,19,210-->

What is an automorphism, formally?
?
An automorphism of $F$ is:
A bijection $\sigma$ from $F$ to $F$ where
$\sigma(x + y) = \sigma(x) + \sigma(y)$
$\sigma(x\cdot y) = \sigma(x)\cdot\sigma(y)$
for all x and y in the field
<!--SR:2022-05-31,15,210-->

What is the intuition behind the definition of an automorphism?
?
An automorphism is a function that shuffles around the field elements while respecting the field operations.
<!--SR:2022-05-31,18,230-->

What is $Aut\ F$?
?
The set of all automorphisms of $F$.
<!--SR:2022-05-26,15,250-->

What is the additional property of an automorphism fixing $\mathbb{Q}$?
?
$\sigma(x) = x,\ \forall x \in \mathbb{Q}$
<!--SR:2022-06-11,26,250-->

What is $Aut\ F/\mathbb{Q}$?
?
The set of all automorphisms over $F$ fixing $\mathbb{Q}$.
<!--SR:2022-06-14,28,250-->

What are the formalisations for "numbers" and permutations from the $\sqrt{2}$  example?
?
Numbers become fields, i.e., $\sqrt{2}$ and $-\sqrt{2}$ becomes $\mathbb{Q}(\sqrt{2})$.
Permutations become automorphism, i.e., the permutations of $\sqrt{2}$ and $-\sqrt{2}$ become the automorphisms of $\mathbb{Q}(\sqrt{2})$.
<!--SR:2022-05-26,16,250-->


# Examples

What is the formal definition of $\mathbb{Q}(\sqrt{2})$?
?
$\{a + b\sqrt{2} : a, b \in \mathbb{Q}\}$
<!--SR:2022-06-10,25,250-->

How do we calculate the number of automorphisms fixing $\mathbb{Q}$ in $\mathbb{Q}(\sqrt{2})$?
?
$\sigma(a + b \sqrt{2})$ arbitrary automorphism of arbitrary element
$= \sigma(a) + \sigma(b)\sigma(\sqrt{2})$ by the additive and multiplicative properties of automorphisms
$= a + b + \sigma(\sqrt{2})$ since $\sigma$ fixes $\mathbb{Q}$
$= a + b \pm\sqrt{2}$ since automorphisms send numbers to one of their conjugates
So there are just 2 such automorphisms.
<!--SR:2022-05-25,4,250-->

How do we visualise an automorphism fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$?
?
Just draw how it acts on the conjugates of $\sqrt{2}$, since that determines how it acts on the whole field.
<!--SR:2022-05-25,4,250-->

What do the each of the automorphisms fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$ do to the conjugates of $\sqrt{2}$?
?
The first leaves all conjugates in the same place.
The second swaps $\sqrt{2}$ and $-\sqrt{2}$
<!--SR:2022-05-25,4,250-->

# Group Theory

# The Fundamental Theorem