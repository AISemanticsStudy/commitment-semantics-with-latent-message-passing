# Commitment Semantics with Latent Message Passing
This repository contains the code and resources for the research project on "Commitment Semantics with Latent Message Passing", a theory try to formalize computational semantics of artificial intelligence and unify the understanding of various AI paradigms and specific models.

## Why project not paper?
The unique view of the theory being developed here follows and uses the concepts and wording wildly used in programming languages, distributed systems, and databases, which makes the theory more accessible to researchers from these fields, and also opens up more engineering-focused practitioners to understand the concepts.
Also we don't want to write a paper for the sake of writing a paper, that forcing the core subject of this theory semantics into the rigid format of one specific mathematical framework or formal system.
So we decided to use a tone between system design documents and semi-philosophical essays to present the ideas and concepts of the theory.

We would like everyone to be a part of the open research process, and we believe that sharing the ideas in an informal manner first will help us gather feedback and improve the theory before formalizing it into academic papers.
Why this is important? We would like to make the theory as theoretical and as structural as possible, so that it can be easily applied to various AI paradigms and models. That's why it is crucial to have a wide range of feedback from different perspectives, especially from those who are working on developing AI inference systems and training new models. We appreciate any feedback if you apply the theory and find interesting results or new methodologies derived from it.

Once the theory is more established and widely accepted, we plan to write formal papers to present the findings in a traditional academic format and submit them to well-suited tracks of conferences and journals of different fields and disciplines.

## Pre-requisites
To fully understand the concepts and ideas presented, we encourage readers to have a minimal understanding of the following topics.
These topics are not strictly required or fully covered by the theory, but they will help readers build natural intuition.

- WAL (Write Ahead Log)
- Logical Clocks and Consensus algorithms (e.g., Paxos, Raft)
- CRDTs (Conflict-free Replicated Data Types)
- SmallTalk and Erlang programming languages

## LOC
- the core concepts and definitions
- revisiting existing AI paradigms and models from the theory's perspective
- hypothesis and cross-discipline observations derived from the theory


## revisiting existing AI paradigms and models from the theory's perspective


## Residual

## Checkpoint technique
The message passing semantic ensures the recomputation of the forward passing will always yield the same result as long as the IDR representation is not changed.
Although it is obvious and trivial to prove this property from mathematical perspective, it has significant practical implications in engineering that here is great room to
explore by introducing compression techniques or other practices widely used in distributed systems and databases.

### RNN
Form lossy IDR.

### MLP and CNN
Doesn't form IDR. Purely message passing.
So under the theory, MLP or CNN is not a complete model for intelligence.
Please note that this is not mean to discount their researchers/inventors's contributions to the great success of CNN in computer vision tasks and MLP as a foundational building blocks of AI in general.
This is also a reminder for us the word choice of "intelligence" to describe IDR could be transitional and context-dependent.
Once IDR is a well-established concept in AI research, we could inter-communicate more precisely without using general terms like "intelligence".

### BERT
We should take caution when interpreting BERT's role in the theory because BERT is the an special case where it contracts GPT both IDR representation and message passing into one single model.
To demonstrate how BERT fits into the theory, we could conduct the following thought experiment:
1. BERT with mask sampling equivalent or even better than causal mask.
2. Mask only last token.

Verdict: BERT form lossless IDR representation but the message passing it create during train drifts away too much from the one form from causal masking.
Here we are not arguing BERT is worse than GPT, but just pointing out the difference of the two models from the theory's perspective.
On the contrary, revisiting BERT's unique design from the les of the theory could lead to the conclusion that BERT would be perfect for tasks:
- can perfectly encode its message passing as a mask distribution.
- hidden objects require exact same connections to each other.

To summarize, BERT can produce IDR, but its IDR is not compatible with the physical world tightly.
We are not drawing a conclusion casual masking or an autoregressive model is always better but pointing out under the theory, different masking strategies can be explainable purely from distribution alignment
rather than empirical performance or philosophical take.
Also we can further supplement the above interpretation that forming of IDR is not coupled with
- how many tokens to offset, BERT none, GPT 1, or more than 1
- the direction of message passing, BERT fully-connected, GPT causal broadcasting

## hypothesis and cross-discipline observations derived from the theory
### origin of animal brain
The theory support the hypothesis animal with brain could evolve from a fusion of two multiple primitive lives.
With one life providing the IDR representation and the other life providing the message passing mechanism, the fused life form could gain significant advantages in adapting to complex environments, leading to the evolution of more sophisticated brains.
By contrast, it is much easier for natural selection to evolve one single mechanism, either IDR representation or message passing, but not both.

### There is no back-propagation in human brain
The theory suggests that the human brain or any being definitely does not need back-propagation as a learning mechanism.
Using only prune and connect operations on neural linkages (synapses) to adjust the message passing pathways is sufficient for the brain to learn and adapt to new information.
As long as the linkages maintain a set of IDRs

### Neural linkage's robustness

One long standing question in neuroscience is how the brain maintains stable memory and intelligent behavior over sparse neural linkages (synapses) over long periods of time, despite the fact that individual synapses are constantly being formed and pruned. The message passing part of the theory provides a solid explanation for this phenomenon. Because the neural linkage purely serves as a communication channel for passing latent messages, the exact structure and strength of individual synapses are not critical for maintaining the overall functionality of the brain. As long as there are enough synapses to facilitate the necessary message passing, the brain can continue to function effectively, even if individual synapses are lost or weakened over time.

### Human brain's IDR
If you are a neuroscientist, you may find it interesting to think about what the IDR representation in human brain could be. And please feel free to share your thoughts and findings with us!

### Alzheimer's disease and other amnesia behaviors
With the theory, we could understand amnesia as a progressive degradation of the IDR representation.

### Sleep and dreaming
Under the theory, sleep could be understood as a process equivalent to a GPT conducting offline training to update its IDR representation.
And dreaming could be seen as an occasional inference process with a transient state of the message passing pathways being reconfigured.

### DNA is evolutionary's IDR
Like KVCache, DNA strictly complies with the properties of IDR representation defined in the theory.

### Two level of IDR
With the theory, we could understand animal intelligence at two levels by recognizing two levels of IDR representation:
- DNA
- Brain

We could also further create new categories classifying lives by having how many levels of intelligence they have and to confirm if plants only have one.

### Nature selection and mutation
With this theory, we could well understand the nature selection and mutation process in evolution at both a very atomic and macro level.
Mutation should not just be emergent useful behavior for the life form, but also should be able to maintain or improve the IDR representation and message passing mechanism of the life form.

### Difference between stimulant and psychedelic drugs
With this theory, we could understand how stimulant and psychedelic drugs affect human brain differently by studying how do they effect IDR representation and message passing mechanisms.

## Taking a step back
We the listing parallel of phenomenons and more potential applications on-going research might discover of the theory, we can make a strong call back to the theory
that the semantics of intelligence and learning.
- intelligence: IDR, strict, reliable, consistent
- learning: general, flexible, adaptable, evolving. human brain, GPT and nature selection each uses dramatically different mechanisms to achieve this.

## Repository Structure
- `research-log/`: A collection of research notes, experiments, and findings related to the project.
- `blogs/`: Informal blog posts discussing various aspects of commitment semantics and latent message passing.
