#flashcards/funmaths/aleph0/galois
# Intro

What is Galois Theory about, roughly?
?
Algerbraic expressions including values like $\sqrt{2}$ and $-\sqrt{2}$, and the ways you can permute those values while keeping the expression true.
<!--SR:!2023-02-27,35,230-->

What is the popularly known consequence of the Fundamental Theorem of Galois Theory?
?
That there is no general formula to solve a polynomial of degree 5 or higher.
<!--SR:2023-05-14,229,250-->


# What is the Square root of 2?

What is the square root of 2 as a truncated decimal?
?
1.41... and -1.41...
<!--SR:2023-04-30,207,230-->

Explain the "algebraic difference" between $\sqrt(2)$ and $-\sqrt{2}$.
?
There is none. Consider any true expression containing $\sqrt{2}$, it will still be true if you replace $\sqrt{2}$ with  $-\sqrt{2}$.
<!--SR:2023-03-07,211,270-->

What are basic examples of algebraic expressions that both $\sqrt{2}$ and $-\sqrt{2}$ satisfy?
?
$\sqrt{2}^2 = 2$
$(\sqrt{2})^3 = 2\sqrt{2}$
<!--SR:!2024-03-28,430,250-->

What does it mean to say that $\sqrt{2}$ and $-\sqrt{2}$ are conjugate over $\mathbb{Q}$?
?
Whenever you have an equation with rational coefficients, replacing $\sqrt{2}$ with $-\sqrt{2}$ will leave the equation holding true.
<!--SR:!2023-07-18,242,210-->

??? Does this mean that we can construct expressions with non rational coefficients for which $\sqrt{2}$ and $-\sqrt{2}$ are not conjugate?

What is the "basic question" of Galois Theory?
?
Given a bunch of numbers that are conjugate over $\mathbb{Q}$, how many ways are there to swap them that preserve algebraic relations?
<!--SR:!2023-08-11,248,210-->

What is an example of an equation where you can swap $\sqrt{2}$ and $-\sqrt{2}$?
%%%%?
$\frac{1}{3 + 2\sqrt{2}} = [1 + (-\sqrt(2)]^2$
<!--SR:2022-07-08,35,190-->

Can we always swap $\sqrt{2}$ and $-\sqrt{2}$ in algebraic expressions with rational coefficients?
?
Yes.
<!--SR:!2024-05-24,487,270-->

What is $\zeta$
?
$e^{\frac{2i\pi}{5}}$, a 5th root of unity.
<!--SR:2023-03-02,162,210-->

What are the conjugates of $\zeta$ over $\mathbb{Q}$?
?
$\zeta,\zeta^2,\zeta^3,\zeta^4$
<!--SR:!2024-01-14,356,250-->

How many ways are there to permutate the conjugates of $\zeta$ over $\mathbb{Q}$, and how many of those permute algebraic relations?
?
$4! = 24$ permutations
$4$ preserve algebraic relations
<!--SR:2023-03-15,190,250-->

What are the permutations of conjugates of $\zeta$ that preserve algebraic relations?
?
$(\zeta,\zeta^2,\zeta^3,\zeta^4)$
$(\zeta^2,\zeta^4,\zeta,\zeta^3)$
$(\zeta^3,\zeta,\zeta^4,\zeta^2)$
$(\zeta^4,\zeta^3,\zeta^2,\zeta)$
<!--SR:2023-05-15,230,250-->

Why do we want to study the algebra preserving permutations of conjugates?
?
It helps to understand how numbers (like $\sqrt{2}$ and $e^{\frac{2i\pi}{5}}$) are related to each other.
<!--SR:!2023-08-21,270,230-->

# Fields and Automorphisms

What is a field, roughly speaking?
?
Any set where you can add, subtract, multiply, and divide elements.
<!--SR:!2023-09-18,304,250-->

Name a field (basic, but highly relevant to Galois theory)
?
The rational numbers
<!--SR:2023-03-31,225,270-->

What can't you do in a field?
?
Take square roots.
<!--SR:2023-04-13,213,250-->

What is $\mathbb{Q}(\sqrt(2)$? What does it contain?
?
The smallest field containing the rationals and $\sqrt{2}$.
Being closed under +, -, \*, and /, it contains $1+\sqrt{2}$ etc.
<!--SR:2023-04-16,239,270-->

Describe the automorphisms analogous to our non-rigorous motivating example with $\sqrt{2}$
?
Some automorphism fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$.
<!--SR:2023-04-27,191,210-->

What is an automorphism, formally?
?
An automorphism of $F$ is:
A bijection $\sigma$ from $F$ to $F$ where
$\sigma(x + y) = \sigma(x) + \sigma(y)$
$\sigma(x\cdot y) = \sigma(x)\cdot\sigma(y)$
for all x and y in the field
<!--SR:!2023-02-15,23,150-->

What is the intuition behind the definition of an automorphism?
?
An automorphism is a function that shuffles around the field elements while respecting the field operations.
<!--SR:2023-05-28,222,230-->

What is $Aut\ F$?
?
The set of all automorphisms of $F$.
<!--SR:2023-07-04,259,250-->

What is the additional property of an automorphism fixing $\mathbb{Q}$? (As compared to an ordinary automorphism not fixing $\mathbb{Q}$).
?
$\sigma(x) = x,\ \forall x \in \mathbb{Q}$
<!--SR:!2023-09-04,224,230-->

What is $Aut\ F/\mathbb{Q}$?
?
The set of all automorphisms over $F$ fixing $\mathbb{Q}$.
<!--SR:2023-02-16,174,250-->

What are the formalisations for "numbers" and permutations from the $\sqrt{2}$  example?
?
Numbers become fields, i.e., $\sqrt{2}$ and $-\sqrt{2}$ becomes $\mathbb{Q}(\sqrt{2})$.
Permutations become automorphism, i.e., the permutations of $\sqrt{2}$ and $-\sqrt{2}$ become the automorphisms of $\mathbb{Q}(\sqrt{2})$.
<!--SR:2023-06-21,246,250-->


# Examples

What is the formal definition of $\mathbb{Q}(\sqrt{2})$?
?
$\{a + b\sqrt{2} : a, b \in \mathbb{Q}\}$
<!--SR:2023-03-21,221,270-->

How do we calculate the number of automorphisms fixing $\mathbb{Q}$ in $\mathbb{Q}(\sqrt{2})$?
?
$\sigma(a + b \sqrt{2})$ arbitrary automorphism of arbitrary element
$= \sigma(a) + \sigma(b)\sigma(\sqrt{2})$ by the additive and multiplicative properties of automorphisms
$= a + b\sigma(\sqrt{2})$ since $\sigma$ fixes $\mathbb{Q}$
$= a + b \cdot(\pm\sqrt{2})$ since automorphisms send numbers to one of their conjugates
So there are just 2 such automorphisms.
<!--SR:!2023-03-29,113,230-->

How do we visualise an automorphism fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$?
?
Just draw how it acts on the conjugates of $\sqrt{2}$, since that determines how it acts on the whole field.
<!--SR:2023-06-06,231,250-->

What do the each of the automorphisms fixing $\mathbb{Q}$ over $\mathbb{Q}(\sqrt{2})$ do to the conjugates of $\sqrt{2}$?
?
The first leaves all conjugates in the same place.
The second swaps $\sqrt{2}$ and $-\sqrt{2}$
<!--SR:2023-05-25,219,250-->

# Group Theory

# The Fundamental Theorem