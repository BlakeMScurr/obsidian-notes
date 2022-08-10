
#flashcards/software/eigenlayer

# Questions

How does "the value of Ethereum increases significantly due to the future fee opportunity from these manifold services"? How are fees on EigenLayer connected to Eth? I don't see it, if we're just talking capital at stake.

# Appendix

## A

What $CoC$ mean?
?
Cost of corruption.
<!--SR:2022-08-14,4,250-->

What is the $CoC$ of a DApp without restaking?
?
$CoC_i = \underset{j \in M_i}{\mathrm{min}} \{CoC_j\}$
<!--SR:2022-08-12,2,250-->

What is the $CoC$ of a DApp with restaking?
?
$$CoC_i = \sum_{j \in M_i} \{CoC_j\}$$
<!--SR:2022-08-14,4,250-->

What does $S$ denote?
?
The set of all stakers.
<!--SR:2022-08-13,3,250-->

What does $T$ denote?
?
The set of all tasks secured by eigenlayer.
<!--SR:2022-08-13,3,250-->

What does $s_i$ denote?
?
The amount of stake held by staker $i$
<!--SR:2022-08-11,1,230-->

What does $S_j$ denote?
?
The set of stakers who have staked for the task $j$.
<!--SR:2022-08-11,1,230-->

What does $\alpha_j$ denote?
?
The fraction of stake require to corrupt task $j$.
<!--SR:2022-08-14,4,250-->

What does $U$ denote?
?
A sumset of the validators/restakers $S$.
<!--SR:2022-08-12,2,250-->

What does $V$ denote?
?
A subset of the tasks $T$
<!--SR:2022-08-14,4,250-->

When do we define the condition when a set of validators is sufficient to corrupt a task?
?
$U \subseteq S$ is sufficient to corrupt task $j \in T$ if their combined share of stake surpasses the fraction $\alpha_j$.
<!--SR:2022-08-11,1,230-->

What is $S_j^c$?
?
The collection of staker sets sufficient to corrupt $j$.
<!--SR:2022-08-13,3,250-->

How do we define $S_j^c$?
?
$$
\{ U \subseteq S : \sum_{i \in S_j \cap U} s_i > \alpha_j \sum_{i \in S_j} s_i\}
$$
<!--SR:2022-08-12,2,250-->

What does $S^c(V)$ denote?
?
The collection of staker sets which are sufficient to corrupt all tasks in the subset $V$.

What is the definition of $S^c(V)$?
?
$\bigcap_{j \in V} S_j^c$

What does $c(V)$ denote?
?
The cost of corruption for a subset of tasks $V$.

How is $c(V)$ defined?
?
$$\underset{U \in S^c(V)}{\mathrm{min}} \sum_{i \in U}s_i$$

What does $p_j$ denote?
?
The profit from corruption of task $j$.

What does $p(V)$ denote?
?
The total profit from corrupting the set of tasks $V$.

How is $p(V)$ defined?
?
$$\sum_{j \in V} p_j$$

When is a task $j$ secure? Use natural language.
?
If for all sets of tasks containing $j$, the cost of corruption is higher than the profit from corruption.

When is a task $j$ secure? Use mathmatical symbols.
?
$j$ is secure $\iff \forall\ V \ni j,\ c(V) > p(V)$

For all tasks to be secure, $\forall\ V \subseteq T$ . . .?
?
$c(V) > p(V)$

What does $T^c(U)$ denote?
?
The set of tasks that the stakers $U$ are able to corrupt.

What is the definition of $T^c(U)$?
?
$$
\{j \in T : \sum_{i \in S_j \cap U} s_i > \alpha_j \sum_{i \in S_j}s_i\}
$$


All tasks are secure $\iff$ . . . ?
?
$$\forall\ U \in S, \sum $$







