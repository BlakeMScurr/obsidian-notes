#flashcards/Finite_Fields/Lidl/1
# Intro

What are the axioms of a group called?
?
Assosiativity
Identity
Inverse
<!--SR:2022-10-20,203,270-->

What is the group associativity axiom?
?
It doesn't matter in which direction you associate the operations, i.e.;
$$
\forall a, b, c \in G, a \ast(b\ast c) = (a \ast b) \ast c
$$
<!--SR:2022-10-19,202,270-->

What is the group identity axiom?
?
$$
\exists e \in G\ |\ \forall a \in G ae = ea = a
$$
<!--SR:2022-10-30,213,270-->

What is the group inverse axiom?
?
$$
\forall a \in G\ \exists a^{-1}\ |\ a^{-1}a = aa^{-1} = e
$$
<!--SR:2022-10-29,212,270-->

What are the elementary consequences of the group axioms?
?
Uniqueness of the identity
Uniqueness of the inverse
Inversion of a product
<!--SR:2022-06-23,58,250-->

How do you prove the uniqueness of group identity?
?
$e_1 = e_1e_2 = e_2$ by the indentity property of $e_1$ and $e_2$
<!--SR:2022-06-25,60,250-->

How do you prove the uniqueness of the group inverse?
?
$a^{-1}_1 = a^{-1}_2aa^{-1}_1 = a^{-1}_2$
<!--SR:2022-11-01,215,270-->

What is the "inversion of a product" elementary group property, and how do you prove it?
?
Inversion of a product means that
$$
(ab)^{-1} = b^{-1}a^{-1}
$$
You prove it by noting that both are the inverse of $ab$:
$$
b^{-1}a^{-1} = b^{-1}a^{-1}ab(ab)^{-1} = (ab)^{-1}
$$
<!--SR:2022-06-20,55,250-->

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
<!--SR:2022-06-12,47,210-->

How do we know that $a_1a_2...a_n$ is an unambiguous expression for a group?
?
The associative law implies that no matter how we insert parentheses, the expression will always represent the same element of G.
<!--SR:2022-06-24,59,250-->

What are the "n-fold" rules in each notation?
?
Multiplicitive:
$a^{-n} = (a^{-1})^n$
$a^na^m = a^{n+m}$
Additive:
$(-n)a = n(-a)$
$na + ma = (n + m)a$
<!--SR:2022-05-27,2,150-->

What is "0-fold" of $a$ in both notations?
?
$a^0 = e$
$0a = 0$
Where the last zero is the identity in G, and the others are the integer 0
<!--SR:2022-10-12,195,250-->

What are some trivial examples of groups?
?
Integers under addition.
The group with a single element e.
A modular arithmetic group.
<!--SR:2022-06-10,32,230-->

What are the identity and inverse of $a$ in the additive group over the integers?
?
$0$ and $-a$
<!--SR:2022-05-31,35,250-->

What is a cyclic multiplicative group, and what is the generator?
?
A multiplicative group is called cyclic if there is some $a \in G$ such that for any $b \in G$ there is some integer $j$ with $b = a^j$.
$a$ is called the generator and we write $G = \langle a\rangle$.
<!--SR:2022-06-28,42,190-->

What is the immediate property of cyclic groups and how do we know?
?
Cyclic groups are commutative because all elements can be represented as a power of $a$, and $aaaa = aaaa$ no matter how many times you move an $a$ around.
<!--SR:2022-05-30,29,210-->

What are the generators of the additive group $\mathbb{z}$?
?
$1$ and $-1$.
<!--SR:2022-06-21,48,250-->

What are the properties of an equivalence relation?
?
Reflexivity, symmetry, and transitivity.
<!--SR:2022-06-01,36,250-->

What is the reflexivity property of an equivalence relation?
?
$$(s, s) \in R\ \forall s \in S$$
<!--SR:2022-05-30,14,170-->

What is the symmetry property of an equivalence relation?
?
$$(t, s) \in R \implies (s, t) \in R$$
<!--SR:2022-06-08,43,270-->

What is the transitivity property of an equivalence relation?
?
$$(s, t),\ (t, u) \in R \implies (s, u) \in R$$
<!--SR:2022-06-15,43,230-->

How does an equivalence relation induce a partition of $S$?
?
A partition of $S$ is a representation of $S$ as a union of mutually disjoint subsets of $S$.
The union of equivalence classes is equivalent to $S$ because of reflexivity (all elements are in a class at least containing themselves), and the classes are mutually disjoint because of symmetry and transitivity (if any two elements are equivalent, they share the same equivalence class with all their other equivalents).
<!--SR:2022-06-14,43,230-->

What is the definition of an equivalence class?
?
$$[s] = \{ t \in S\ |\ (s, t) \in R\ \}$$
<!--SR:2022-06-06,27,170-->