#flashcards/zkps/Finite_Fields/Lidl/1
# Intro

What are the axioms of a group called?
?
Assosiativity
Identity
Inverse
<!--SR:2021-11-01,4,270-->

What is the associativity axiom?
?
It doesn't matter in which direction you associate the operations, i.e.;
$$
\forall a, b, c \in G, a \ast(b\ast c) = (a \ast b) \ast c
$$
<!--SR:2021-10-31,3,270-->

What is the identity axiom?
?
$$
\exists e \in G\ |\ \forall a \in G ae = ea = a
$$
<!--SR:2021-11-01,4,270-->

What is the inverse axiom?
?
$$
\forall a \in G\ \exists a^{-1}\ |\ a^{-1}a = aa^{-1} = e
$$
<!--SR:2021-10-31,3,270-->

What are the elementary consequences of the group axioms?
?
Uniqueness of the identity
Uniqueness of the inverse
Inversion of a product
<!--SR:2021-11-01,4,270-->

How do you prove the uniqueness of identity?
?
We must show that 
$$
ae_1 = ae_2 = a \implies e_1 = e_2
$$
We can do it like so:
$$
ae_1 = ae_2 \implies a^{-1}ae_1 = a^{-1}ae_2 \implies ee_1 = ee_2 \implies e_1 = e_2
$$
This implies that there is one unique identity per element, and since that must be the identity proper, there is one unique identity.
<!--SR:2021-11-06,7,270-->

How do you prove the uniqueness of the inverse?
?
$$
\begin{align}
e = e \\
\implies aa^{-1}_1 = aa^{-1}_2 \\
\implies a^{-1}aa^{-1}_1 = a^{-1}aa^{-1}_2 \\
\implies ea^{-1}_1 = ea^{-1}_2 \\
\implies a^{-1}_1 = a^{-1}_2 \\
\end{align}
$$
<!--SR:2021-11-02,5,270-->

What is the "inversion of a product" elementary group property, and how do you prove it?
?
Inversion of a product means that
$$
(ab)^{-1} = b^{-1}a^{-1}
$$
You prove it with:
$$
b^{-1}a^{-1} = b^{-1}a^{-1}ab(ab)^{-1} = b^{-1}b(ab)^{-1} = (ab)^{-1}
$$
<!--SR:2021-11-02,5,270-->

How do you represent the n-fold composite of a group element with itself?
?
In multiplicative notation we have n factors of a:
$$
a^n = aa...a
$$
In additive notation we have n summands of a:
$$
na = a + a + ... + a
$$
<!--SR:2021-10-31,1,230-->

How do we know that $a_1a_2...a_n$ is an unambiguous expression for a group?
?
The associative law implies that no matter how we insert parentheses, the expression will always represent the same element of G.
<!--SR:2021-11-04,5,270-->

What are the "n-fold" rules in each notation?
?
Multiplicitive:
$a^{-n} = (a^{-1})^n$
$a^na^m = a^{n+m}$
Additive:
$(-n)a = n(-a)$
$na + ma = (n + m)a$
<!--SR:2021-10-31,1,230-->

What is "0-fold" of $a$ in both notations?
?
$a^0 = e$
$0a = 0$
Where the last zero is the identity in G, and the others are the integer 0
<!--SR:2021-11-03,4,250-->

What are some trivial examples of groups?
?
Integers under addition.
The group with a single element e.
A modular arithmetic group.
<!--SR:2021-11-03,4,270-->

What are the identity and inverse of $a$ in the additive group over the integers?
?
$0$ and $a^{-1}$

What is a cyclic multiplicative group, and what is the generator?
?
A multiplicative group is called cyclic if there is some $a \in G$ such that for any $b \in G$ there is some integer $j$ with $b = a^j$.
$a$ is called the generator and we write $G = \langle a\rangle$.

What is the immediate property of cyclic groups and how do we know?
?
Cyclic groups are commutative because all elements can be represented as a power of $a$, and $aaaa = aaaa$ no matter how many times you move an $a$ around.

What are the generators of the additive group $\mathbb{z}$?
?
$1$ and $-1$.

