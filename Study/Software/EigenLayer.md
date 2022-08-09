# Questions

How does "the value of Ethereum increases significantly due to the future fee opportunity from these manifold services"? How are fees on EigenLayer connected to Eth? I don't see it, if we're just talking capital at stake.

# Appendix

## A

What $CoC$ mean?
?
Cost of corruption.

What is the $CoC$ of a DApp without restaking?
?
$CoC_i = \underset{j \in M_i}{\mathrm{min}} \{CoC_j\}$

What is the $CoC$ of a DApp with restaking?
?
$$CoC_i = \sum_{j \in M_i} \{CoC_j\}$$
What does $S$ denote?
?
The set of all stakers.

What does $T$ denote?
?
The set of all tasks secured by eigenlayer.

What does $s_i$ denote?
?
The amount of stake held by staker $i$

What does $S_j$ denote?
?
The set of stakers who have staked for the task $j$.

What does $\alpha_j$ denote?
?
The fraction of stake require to corrupt task $j$.

What does $U$ denote?
?
A sumset of the validators/restakers $S$.

What does $V$ denote?
?
A subset of the tasks $T$

When do we define a set of validators as sufficient to corrupt a task?
?
$U \subseteq S$ is sufficient to corrupt task $j \in T$ if their combined share of stake surpasses the fraction $\alpha_j$.

What is $S_j^c$?
?
The collection of staker sets sufficient to corrupt $j$.

How do we define $S_j^c$?
?
$$
\{ U \subseteq S : \sum_{i \in S_j \cap U} s_i > \alpha_j \sum_{i \in S_j} s_i\}
$$
