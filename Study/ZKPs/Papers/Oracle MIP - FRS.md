MIPs may be more powerful than IPs because you have another unrelated person corroborating your story.

IPs have been generally very useful. IPs have shown that if graph isomorphism is NP-complete then the polynomial time hierarchy collapses.

Key results
	- MIPs can be characterised in terms of probabilistic oracle Turing machines.
	- MIP <= NEXP
	
Babai et al show that MIP = NEXP

The third result hoping to bound MIP and NEXP that I don't yet understand
	- "We then show results like the one proved by Babi et al. cannot relativize by exhibiting an oracle relative to which there exist co-NP problems that do not have multiple prover interactive proof systems."
	- "MIP = NEXP cannot relativize by exhibiting an oracle relative to which there exist co-NP problems that do not have multiple prover interactive proof systems."
	- "Finally we exhibit a relativized world where a co-NP language does not have MIPs"
	
"We show, however, that the existence of an oracle relative to which there exist languages with multiple prover interactive proof systems but cannot be computer in polynomial space would imply an unrelativized separation of NP and poly-log space.'' What does that mean? "We show, however, that the existence of an oracle relative to which there exist languages with multiple prover interactive proof systems, but cannot be computed in polynomial in polynomial space would imply an unrelativized separation of NP and poly-log space"

Finally, we show a simple example that illustrates that multiple prover interactive proof systems do not behave independently in parallel as previously believed.

Let P_1, ... P-k be infinitely powerful machines and V be a probabilistic polynomial-time machine, all of which share the same read-only input tape. The verifier V shares communication tapes with each P_i, but different provers Pi and Pj have no tapes they can both access besides the input tape. We allow k to be as large as a polynomial in the size of the input; any larger and V could not acess all the provers.

Formally, each P_i is a function from the input and the conversation it has seen so far to a message. We put no restrictions on the complexity of this function other than that the lengths of the messages produced by this function must be bounded by a polynomial in the size of the input. We will assume throughout this paper that the inputs are drawn from the set of strings over the alphabet {0,1}.


Ps and V form a MIP for L if:
	- x in L then Pr(Ps and V on x accept) > 1 - 2^-n
	- if x not in L then for all bad Ps, Pr(bad Ps and V on x accept) < 2^-n
	
Note that this is the same condition essentially as the IP set out in GMR.

MIP is the class of all languages which have multi-prover interactive protocols. If k is one gets geth class IP of languages accepted by one-prover interactive proof systems.

Note that we require an exponentially small probability of error. We could reduce a constant error to a probability of error less than 2^-p(n) for any polynomial p(n) by running the protocols several times serially.

Unlike the result of Babi and Moran for the one-prover model, it is unknown whether we can decrease the probability of error in multi-prover proof systems by running the protocols in parallel.

A round of a multi prover interactive protocol consists of messages from the verifier to some of all of the provers followed by messages from these provers to the verifier. In general, interactive protocols can have a polynomial number of rounds. We let alpha_ij designatea message from prover i to the verifier in round j and beta_ij designate a message from the verifier to the prover i in round j.

Ben-Or et al originally developed multi-prover interactive proof systems primarily for cryptographic purposes. They show every language accepted by two prover interactive prof system has a perfect zero-knowledge two prover proof system, where even NP does not have perfect zero-nkowledge single prover proof systems unless the polynomial time hierarchy collapses.

That's fucking interesting. I guess they were trying to find powerful models in which to perform zero knowledge proofs, and they showed that IPs only prove NP if the polynomial time hierarchy collapses, whereas MIPs can definitely do it. However, how does this circle square with the notion that one way functions imply that NP has IPs? Since GMW supposedly showed that?? What's the complexity theory angle on this? Well, it's that you can determine what languages have IPs, and so you can determine whether the polynomial hierarchy collapses. It's just another avenue for interrelation.

They also show two prover systems can simulate any multi-prover system. Along the lines of Furer et al, the show any two prover system has an equivalent system that accepts with probability one for strings in the language. That's incredible!!! We can reduce MIPs from probabilstic to total! What an amazing result.

Subsequent to the results described in this paper, the complexity of interactive proof systems have been shown to be much more powerful than previously believed. Lund et al have showen the existen of an IP for every language in the polynomial time hierarchy. Using the techniques of Lund, has shown that every language computable in polynomial space has an IP.

Can I characterise what I've learned here? Well, it's that broadly, the work in proofs is a combination of complexity theory and cryptography. That we have new proof models which define language classes, and we try to define the interrelations between the classes. It's useful to know the languages that proofs can prove from a cryptographic perspective, obviously, and generating new models which have additional power are useful. Moreover, recharacterising existing models can usefully define the classes. So IP was constructed for cryptograph, then we had MIP, which lived on the border of complexity theory, since the goal was to provide a cryptgraphic system that had additional power and fewer assumptions. This is cryptographic, but increasing the complexity of cryptographic protocols. Well actually, I think the stated goals in GMW were more to remove computational assumptions from the system. This is another complex way in which complexity and cryptography mix - modern cryptographic systems rely on hard problems, which are categorised and made sense of with complexity theory. Simultaneously, the actual computations done in cryptography (namely accepting a language, in the QRP or GMR) also fall into complexity classes. So actually BGKW wanted to improve the robustness of IPs by removing a computational asssumption and replacing it with a structural assumption. Was this their whole goal?


The very interesting fact is that it seems that complexity theory seems to have been the increasing interest of people using IPs etc.

I still can't quite capture the thrust and purpose of FRS. First they characterise MIP in a new way, then prove MIP = NEXP, then they prove that 
