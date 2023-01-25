
#flashcards/software/eigenlayer

# Questions

How does "the value of Ethereum increases significantly due to the future fee opportunity from these manifold services"? How are fees on EigenLayer connected to Eth? I don't see it, if we're just talking capital at stake.

# Appendix

## A

What $CoC$ mean?
?
Cost of corruption.
<!--SR:!2023-05-02,159,250-->

What is the $CoC$ of a DApp without restaking?
?
$CoC_i = \underset{j \in M_i}{\mathrm{min}} \{CoC_j\}$
<!--SR:2023-03-05,132,270-->

What is the $CoC$ of a DApp with restaking?
?
$$CoC_i = \sum_{j \in M_i} \{CoC_j\}$$
<!--SR:!2023-03-17,52,250-->

## B

### B.0

What does $S$ denote?
?
The set of all stakers.
<!--SR:!2023-08-25,213,230-->

What does $T$ denote?
?
The set of all tasks secured by eigenlayer.
<!--SR:!2023-05-03,160,250-->

What does $s_i$ denote?
?
The amount of stake held by staker $i$
<!--SR:2023-01-07,78,230-->

What does $S_j$ denote?
?
The set of stakers who have staked for the task $j$.
<!--SR:!2023-05-29,186,270-->

What does $\alpha_j$ denote?
?
The fraction of stake require to corrupt task $j$.
<!--SR:2023-02-28,130,270-->

What does $U$ denote?
?
A subset of the validators/restakers $S$.
<!--SR:!2023-05-27,184,270-->

What does $V$ denote?
?
A subset of the tasks $T$
<!--SR:2023-01-20,88,250-->

When do we define the condition when a set of validators is sufficient to corrupt a task?
?
$U \subseteq S$ is sufficient to corrupt task $j \in T$ if their combined share of stake surpasses the fraction $\alpha_j$.
<!--SR:2023-01-29,94,210-->

What is $S_j^c$?
?
The collection of staker sets sufficient to corrupt $j$.
<!--SR:!2023-05-25,120,250-->

How do we define $S_j^c$?
?
$$
\{ U \subseteq S : \sum_{i \in S_j \cap U} s_i > \alpha_j \sum_{i \in S_j} s_i\}
$$
<!--SR:!2023-01-31,68,250-->

What does $S^c(V)$ denote?
?
The collection of staker sets which are sufficient to corrupt all tasks in the subset $V$.
<!--SR:!2023-06-01,189,270-->

What is the definition of $S^c(V)$?
?
$\bigcap_{j \in V} S_j^c$
<!--SR:!2023-03-23,142,270-->

What does $c(V)$ denote?
?
The cost of corruption for a subset of tasks $V$.
<!--SR:2023-02-22,124,270-->

How is $c(V)$ defined?
?
$$\underset{U \in S^c(V)}{\mathrm{min}} \sum_{i \in U}s_i$$
<!--SR:!2023-01-27,64,230-->

What does $p_j$ denote?
?
The profit from corruption of task $j$.
<!--SR:!2023-07-30,236,290-->

What does $p(V)$ denote?
?
The total profit from corrupting the set of tasks $V$.
<!--SR:!2023-06-09,197,270-->

How is $p(V)$ defined?
?
$$\sum_{j \in V} p_j$$
<!--SR:!2023-07-12,227,290-->

When is a task $j$ secure? Use natural language.
?
If for all sets of tasks containing $j$, the cost of corruption is higher than the profit from corruption.
<!--SR:2023-02-17,118,250-->

When is a task $j$ secure? Use mathmatical symbols.
?
$j$ is secure $\iff \forall\ V \ni j,\ c(V) > p(V)$
<!--SR:!2023-05-28,185,270-->

For all tasks to be secure, $\forall\ V \subseteq T$ . . .?
?
$c(V) > p(V)$
<!--SR:!2023-03-19,53,270-->

What does $T^c(U)$ denote?
?
The set of tasks that the stakers $U$ are able to corrupt.
<!--SR:!2023-03-18,52,250-->

What is the definition of $T^c(U)$?
?
$$
\{j \in T : \sum_{i \in S_j \cap U} s_i > \alpha_j \sum_{i \in S_j}s_i\}
$$
<!--SR:!2023-05-09,104,190-->


All tasks are secure $\iff \forall\ U \in S$ . . . ?
?
$$\sum_{i \in U}s_i > \sum_{j \in T^c(U)} p_j $$
<!--SR:!2023-02-24,31,190-->

What does $\gamma_{ij}$ denote?
?
The fraction of task $j$s securing stake which is held by staker $i$.
<!--SR:!2023-06-18,206,290-->

How is $\gamma_{ij}$ defined?
?
$s_i/\sum_{k \in S_j} s_k$
<!--SR:!2023-03-07,126,250-->

What does $T_i$ denote?
?
The set of tasks for which $i$ is a staker.
<!--SR:!2023-02-14,21,250-->

### B.1

What is the simple sufficient enforcable condition for cryptoeconomic security of all tasks?
?
$$
s_i \geq \sum_{j \in T_i} \gamma_{ij}\frac{p_j}{\alpha_j}
$$
<!--SR:!2023-02-01,8,130-->

What does $T_i$ denote?
?
The set of tasks for which $i$ is a staker.
<!--SR:!2023-02-14,21,250-->

### B.1

What is the simple sufficient enforcable condition for cryptoeconomic security of all tasks?
?
$$
s_i \geq \sum_{j \in T_i} \gamma_{ij}\frac{p_j}{\alpha_j}
$$
<!--SR:!2023-02-01,8,130-->


??? How do the steps in line (10) work?
1/  just applies (9) and sums both sides
2/ Just inverts the sum looking from a different perspective, i.e., for every staker in the subset, for each of their tasks, is equivalent to, for every task, for every staker of that task in the subset.
3/ idk!
4/ Just takes the fact that U is able to corrupt the subset, and so its proportion is at least as large as alpha_j
5/ just a simple x/x = 1 reduction
...
So, let's keep looking at step 3. So TcU is a subset of T, can it be equal? Yes, since U is defined as such. So there is no tradeoff of the rest of the equation there.