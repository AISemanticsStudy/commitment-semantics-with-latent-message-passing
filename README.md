# Commitment Semantics with Latent Message Passing

Commitment Semantics with Latent Message Passing, is a theory try to formalize computational semantics of artificial intelligence and unify the understanding of various AI paradigms and specific models.

## TLDR
You might post a question like to ChatGPT or any other LLM:

> if someone says
> "intelligence is idempotent discrete record, learning is message passing",
> what does it mean?

Or you might copy paste the full [README.md](README.md) content to ChatGPT and ask any question you find interesting.
The answer you get might be very surprising yet compelling.

Or you might copy paste the full [README.md](README.md) and append this question and hit enter:
> As a GPT, an artificial intelligence model, do you believe this is how you work? Yes or no.

## Why most of explanations of AI fall short?

### Forced metaphors
Most of the existing explanations of AI models, especially large language models (LLMs) like GPT, tend to focus on surface-level descriptions or analogies that do not capture the underlying computer science inner work of these models.
The problem with these explanations is not they are using metaphors, but using metaphors that are not well-aligned with the actual hardware and software.

### Rigid mathematical frameworks
Many explanations rely heavily on specific mathematical frameworks or formal systems, which can be difficult to understand for non-experts and may not fully capture the complexity of AI models.
The problem is that those explanations often fail to provide a unified understanding of different AI paradigms and models, leading to confusion and misinterpretation, although they might be mathematically rigorous in one domain. These kinds of explanations usually work very on one specific model or dataset, but fail to generalize to other model design or task.

### Most theories lack reflexivity
The theory of AI should be able to answer the question: "if building a new model A following the theory you derived from studying B, will A and B be identical or at least partially equivalent?". Spoil alert: our theory could answer "yes" to this question. GPT is already one perfect model design under our theory, although we can't prove it is the only one.

### But how we should explain AI then?
The ideal explanation should be able to define AI using well-formed semantics as its micro-foundation,
and derive the dynamics of as a macro landscape to overview how an AI model works and why it could work.

What is more important, the explanation should be compatible with **all** existing well-established findings in life sciences, cognitive sciences, neuroscience, and computer science.
If the explanation could not align with these well-established findings, there should be a very **falsifiable** prediction that could be tested to validate or invalidate the explanation rather than
using the explanation to cherry-pick some findings and discard others.

I have to borrow some trust from you here.
The most natural and universal angle to explain AI models is through the lens of **semantics**.
To be more specific, the computational semantics of a modern AI model like GPT/BERT.

Because semantics is at the unique position of the crossway of multiple disciplines including computer science, cognitive science, linguistics, and philosophy.
And that is exactly what we need to explain AI, as an interdisciplinary field that draws insights and methods from all these disciplines.

## Pre-requisites
To better understand the concepts and ideas presented, we encourage readers to have a minimal understanding of the following topics.
These topics are not strictly required or fully covered by the theory, but they will help readers build natural intuition.

- neural networks, GPT
- WAL (Write Ahead Log)
- Logical Clocks and Consensus algorithms (e.g., Paxos, Raft)
- CRDTs (Conflict-free Replicated Data Types)
- Actor model, SmallTalk, Erlang

To **fully** understand this theory, you **must** have a solid or a least none-intro level understanding of these topics:
- How GPT and BERT are trained and work during inference.
- What is KVCache in GPT and why only GPT has it but BERT doesn't.
- Why WAL is important in databases.
- What is message passing and implications of it.
- What is commitment semantics in databases and distributed systems.
- How to use logical clocks to reason about distributed systems.

Lacking **any** of these knowledge could make it hard to follow some of the arguments and explanations in the theory,
but it is also possible to learn them along the way by asking for help from ChatGPT-like AI assistants or a human expert on these topics.
In the words, this theory is not a theory serving as a pillar to learn these topics or AI from scratch,
but a theory that unifies and connect all these topics and make AI a coherent whole that is definable and with research objects.

We have confidence that once you understand these topics, you will be able to grasp the core concepts of the theory quickly
and find the theory resonate so well with all of them in a beautiful way.

## LOC
- the core concepts and definitions
- revisiting existing AI paradigms and models from the theory's perspective
- hypothesis and cross-discipline observations derived from the theory

## The core concepts and definitions

### The inspiration: KVCache in GPT as a strange being
The original author(Shenghang) has been working on build AI training-inference systems for years, since the ResNet era.
In 2023, his team went through a major reorganization and pivoted to focus on building efficient GPT inference systems.
And after a while some of the team's engineering efforts shifted to optimize GPT inference with KVCache,
since that point, he has been constantly boggled by the strange being of GPT's KVCache mechanism.
In the all the AI models he has worked on before, the inductive bias introduced by the model designers always align with
how the model learn and how the model run.
While GPT is the only model he has seen so far that breaks this convention.
The KVCache stands out as a flashy outlier.
The GPT was designed to has a "next token prediction" core capability,
while what it comes with "KVCache" capability it has during inference
feels more like a cliched word "emerging".

## What is it exactly about KVCache that makes it so special?

GPT is not just predicting tokens — it is committing to them, and once committed, they become part of an irreversible symbolic timeline. KVCache is not an optimization; it is the mechanism that turns probability into memory.

And here comes the big question:
How could we formally define this "committing to tokens" and "irreversible symbolic timeline" in a rigorous way that aligns with well-established computer science concepts?

We need a new concept to capture this unique property of GPT's KVCache, and that concept is what we call **IDR: Idempotent Discrete Record**.
## Let's define IDR: Idempotent Discrete Record
1. Idempotent

- In computer science, an operation is idempotent if performing it multiple times has the same effect as performing it once (e.g., setting a light switch to "ON" is idempotent; toggling it is not).
Applied to an IDR, this means the record is stable and consistent. Once formed, applying the same learning operation (message) to it doesn't change its fundamental state. It represents a reliable, committed piece of knowledge or state.

2. Discrete

- The record is a separate, distinct unit. It's not a continuous gradient but a defined entity that can be stored, referenced, and passed around.

3. Record

- This is the data structure that holds the intelligence. In the context of AI models, the theory strongly suggests that the Key-Value (KV) Cache in a model like GPT is the physical manifestation of an IDR.
- The KV Cache stores computed representations of previous tokens in a sequence. According to the theory, this cache isn't just an optimization trick; it's the model's intelligent state—the idempotent, discrete record of what it has "understood" so far.

### Quick validation, human text and DNA as IDR
To quickly validate the definition of IDR, we could look at two well-known examples of information
storage and transmission in nature: human text and DNA.
Both human text and DNA exhibit the properties of being idempotent, discrete, and record-like.
- Human text: Once written, a piece of text remains unchanged unless explicitly edited. Copying or transmitting the text does not alter its content, making it idempotent. Each character or word is a discrete unit of information, and the entire text serves as a record of knowledge or communication.
- DNA: The genetic code in DNA is stable and can be replicated without change, demonstrating idempotency. The sequence of nucleotides (A, T, C, G) is discrete, and the entire DNA strand serves as a record of an organism's genetic information.
These examples support the idea that IDR is a fundamental concept in both artificial and natural systems of intelligence.

| Property             | Text | DNA | KVCache |
| -------------------- | ---- | --- | ------- |
| Discrete             | ✔    | ✔   | ✔       |
| Idempotent           | ✔    | ✔   | ✔       |
| Replicable           | ✔    | ✔   | ✔       |
| Survives transport   | ✔    | ✔   | ✔       |
| Enables coordination | ✔    | ✔   | ✔       |

A trilling revelation:
The most unique emerging property of GPT is that it has or support a mechanism recognizable and definable works identically to
two things we take for granted to form intelligence in human world:
- human text
- DNA

### IDR vs. CRDT
IDR is a broader concept: all CRDTs are IDRs, but not all IDRs are CRDTs. Please refer to [this file](ird-formalization/crdt.md) for the full comparison.
### Logical clocks view of IDR
please refer to [this file](ird-formalization/logical-clocks.md) for the full formalization.
### IDR as WAL and its implications
please refer to [this file](ird-formalization/wal.md) for how to identify IDR as WAL.
### Mathematical Formalization of IDR Properties
please refer to [this file](ird-formalization/math.md) for the full formalization.

### Commitment semantic is disguised as sampling
One confusing aspect of modern AI models like GPT is the presence of both randomness and determinism in their behavior.
On one hand, these models are often described as probabilistic systems that generate outputs based on learned probability distributions.
On the other hand, they can also exhibit deterministic behavior when given the same input and random seed.
The strange mixture of behaviors hold people from studying it purely as a probabilistic system like random number generator or a deterministic system like database.
But once the concept of IDR is formalized, you would find GPT is actually a commitment semantic system disguised as a probabilistic sampling system.
It perfectly mirror the collapse of wave function in quantum mechanics although there is no proof to support AI is quantum(for now).

### How about learning?
After defining IDR as the core concept of intelligence representation, the next natural question is: How does learning happen? If IDRs are stable records, how are they formed and updated?

There are so many ways to answer this question if you don't have a well-defined concept of minimal committable semantic unit.
But once we have IDR defined, the answer becomes clear and straightforward:
**Learning is message passing that leads to the formation of new IDRs.**

<!-- the original author(Shenghang) is just assigned with critical task by CTO, and will be absent for a while to finish the message passing part -->
<!-- but at this point the theory should be competed enough at its first published form -->

### Back-propagated Message Passing
BP, as the dominant learning mechanism in modern AI models, can be reinterpreted through the lens of message passing.
In this view, BP is a specialized form of message passing that propagates error signals backward through the network to update weights.
However, BP alone does not directly form IDRs; instead, it facilitates the conditions under which IDRs can be formed during forward passes.

### Message passing has duality to neural network's dataflow
To further clarifying why message passing is the right way to think about learning in AI systems like GPT, we need to examine the relationship between message passing and dataflow in
neural network training.
We can think of attention mechanisms as a specific implementation of message passing within neural networks.
For instance
- in GPT, the object(token) is broadcasting its latent representation to other objects(tokens) in a communication pattern define by the causal mask.
- in BERT, the object(token) is broadcasting its latent representation to all other objects(tokens) in a fully-connected pattern.
- in MLP/CNN, the object(one sample(image)'s feature map) is broadcasting its latent representation to all other objects(labels) in a fully-connected pattern.

also, it is worth to point out that the fully-connected pattern of MLP/CNN is not the same as the fully-connected pattern of BERT(1-N vs. N-N).

### Latent objects and actor model
In the theory, we introduce the concept of "latent objects" to represent the pair of sender and receiver in latent message passing.
A latent object is an abstraction that encapsulates both the data and the behavior associated with a particular entity in the system.
We admit that the concept of latent objects is still very preliminary and needs more formalization and validation.
At this point, we could only draw a rough analogy between latent objects and actors in the actor model and hope readers
could form their own understanding and intuition about latent objects after they get familiar with the actor model.

### Latent message passing is not the only way to form IDR
Although the theory choose latent message passing as the primary mechanism to explain to form IDR in AI systems like GPT.
The theory does not exclude other possible mechanisms to form IDR and doesn't claim latent message passing is the only perspective to express the dynamics.
Latent message passing is defined as a fusion of convention and practice of distributed systems and deep learning model training/inference.
Unlike IDR, latent message passing is not a semantic that can be formalized purely from mathematical perspective of computation.
It is more of an engineering-level design pattern that could be implemented in various ways.
You can think of it as a software design pattern like MVC, repository, or observer etc.
For IDR, it is very natural to reuse very well-defined mathematical formalization of other data types or theoretical frameworks to examine and analyze its
properties
(CRDT, WAL, logical clocks).
But for latent message passing, we don't have such luxury(yet).
And that is why we have to invent a new terminology to describe it as a design pattern fusing hardcoded human source code and probabilistic states.
By intuition, the mathematical tools to formalize latent message passing should be fields like information theory, category theory, and algebraic topology.
And these fields are often co-related or even co-inviting concepts and methods with programming language theory and compiler.
So the original author(Shenghang) chose to leave the formalization of latent message passing as future work and
accept the software design pattern level description and calling it a paradigm is sufficient for now
(if you are an expert in studying "monoid" or "functors", please reach out to the original author(Shenghang) for collaboration.)

This is also an empirical signal to suggest it is possible to define what is intelligence in a math-solid way,
but the learning can be of various forms as long as it could produce IDR.

### Object-transfer duality of latent message passing

## revisiting existing AI paradigms and models from the theory's perspective

### Residual

### Bottleneck and level of features
If neural networks is of message passing paradigm. We can safely use information bottleneck theory to analyze the level of features being learned at different layers of the network.


### Feature map reusing and transfer learning
The usefulness of reusing features maps support the durability of network being latent objects and forming connections between latent objects.

### Checkpoint technique
The message passing paradigm ensures the recomputation of the forward passing will always yield the same result as long as the IDR representation is not changed.
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
1. BERT with mask sampling fully cover causal mask.
2. Mask only last token.

many informative discussions with the definition of IDR can actually be inspired by BERT.
- We do not include the alignment between the IDR representation and causality to be a requirement in our definition.
- We do not require IDR to be linear.

By studying BERT's unique design, we could further clarify these two points.
If the IDR is not generated following the causality of the physical world, the IDR could not be used to represent the physical world accurately.
Under our theory, it is not a bug but a feature.
This opens up the possibility of forming IDR that is not linear but aligned with other forms of causality, e.g., hierarchical causality or graph-based causality or even non-causal relationships.
So in the definition of IDR, we don't require the IDR to be generated from causality but only define it being idempotent and discrete.
In the theory, causality is purely a problem of alignment not a problem of dynamics.
It is worth to point out that these are still an open questions and our theory is not yet mature enough to provide a definitive answer on:
- if idempotent and discrete are the minimal requirements for forming IDR as a representation of atomic unit if we and building models in non-causal domains.
- if intelligence as a concept itself is strictly coupled with causality.
The original author(Shenghang) doesn't have a strong conviction on this yet due to the lack of more concrete evidences and tools to validate.
We believe the falsifiability of these questions is crucial for the theory to be a scientific theory rather than a philosophical one and could foreseen this to be an important direction for future research.

Verdict: BERT form lossless IDR representation but the message passing it creates during train drifts away too much from the one form from causal masking.
Here we are not arguing BERT is worse than GPT, but just pointing out the difference of the two models from the theory's perspective.
On the contrary, revisiting BERT's unique design from the les of the theory could lead to the conclusion that BERT would be perfect for tasks:
- can perfectly encode its message passing as a mask distribution.
- latent objects require exact same connections to each other.

To summarize, BERT can produce IDR, but its IDR is not compatible with the physical world tightly because BERT's message passing is fully-connected rather than causal broadcasting.
We are not drawing a conclusion casual masking or an autoregressive model is always better but pointing out under the theory, different masking strategies can be explainable purely from distribution alignment.
rather than empirical performance or philosophical take.
Also we can further supplement the above interpretation that forming of IDR is not coupled with
- how many tokens to offset, BERT none, GPT 1, or more than 1
but coupled with
- the pattern of message passing, BERT fully-connected, GPT causal broadcasting

### GPT inference optimization techniques
After the debut of GPT models, a variety of optimization techniques have been proposed to improve the efficiency and performance of GPT inference.
If we look closely at these techniques from the theory's perspective, they can be generally categorized into two groups:
1. Techniques that optimize the message passing mechanism.
2. Techniques that modify the IDR representation(KVCache) to a lossy form or drop some of them in exchange for improved efficiency.
Note that these two groups of techniques are not mutually exclusive, and some techniques may involve both aspects.
Also we are not making any judgment on the effectiveness of these techniques, but just providing a new perspective to understand or further improve them based on the theory.

### CoT
If we view one IDR as a unit of intelligence.
CoT could be regarded as injecting a set of meaningful IDRs as intermediate steps could significantly improve the quality of the further IDR being generated.

### Symbolic AI
(This section is very opinionated, rather than serious deduction, please feel free to disagree and discuss.
The comments here are purely technical and philosophical,
the original author(Shenghang) has nothing but huge admiration and respect for the pioneers and contributors of symbolic AI
including John McCarthy, Alan Kay, Joe Armstrong and many others.
)
It is interesting to revisit symbolic AI from the theory's perspective.
We can further confirm that BERT or GPT is both connectionism AI and symbolic AI under the theory.
Whether having symbols is not the classifier.
Whether the symbols in the system is generated or learned is the difference between traditional symbolic AI and modern AI models like GPT.
Because symbols are learned, it is possible to form IDR representation with symbols as the latent objects.
Traditional symbolic AI can be seen as as an "mounter" designed to hold human hard-coded knowledge and perform reasoning by massage passing.
Actor-model based symbolic AI system (Smalltalk, Erlang) also has the object-transfer durability because reference of an actor itself can be send as messages as well.
With the theory, we could further confirm that the ideas kept being emphasized by Alan Kay, Joe Armstrong
- message passing is the most universal semantic to model the physical world
- objects are the units of intelligence
- time must be a first-class citizen to be studied in a first principle theory of intelligence

Also we can conclude that a GPT is essentially a massive, probabilistic actor system.
So here we find GPT to be such an exceptional yet inclusive rare being, is all at once:
- a commitment semantic system, aka, database/distributed system
- a probabilistic sampling system, aka, random number generator
- a actor system, aka, message passing system
- a symbolic reasoning system

GPT is so special that it defies all odds yet doesn't contract any.
And GPT is so simple with both minimum design in training and inference.

## hypothesis and cross-discipline observations derived from the theory
Please note that the role of the theory in other disciplines is still very preliminary and speculative.
We would advise you to use it as a guideline to prune and examine your research goal (separate of the concerns)
rather than using it to predict or explain until more concrete evidences and validations are found.
The core takeaway you can derive from the theory is the separation of intelligence into two orthogonal dimensions:
- IDR representation: the minimal committable semantic unit's representation and how it is being stored
- message passing mechanism: how the minimal committable semantic units communicate and coordinate with each other
With this separation in mind, we could confidently explore various hypothesis and observations in a much focus and precise manner.
For instance, one researcher could presumably focus on studying to locate IDR representation in human brain rather than being distracted by the complexity of neural linkages.
If this decomposition is valid, we could expect significant progress in multiple disciplines by applying the theory as a guiding principle and further validate the theory itself.
And that is the key contribution of the theory to non-CS disciplines.

### origin of animal brain
The theory support the hypothesis animals with a brain could evolve from a fusion of two or multiple primitive lives.
With one life providing the IDR representation and the other life providing the message passing mechanism, the fused life form could gain significant advantages in adapting to complex environments, leading to the evolution of more sophisticated brains.
From probability perspective much easier for natural selection to evolve one single mechanism, either IDR representation or message passing, but not both at the same time due to the complexity of co-evolution. Further study might facilitate this timothies of how animal brain evolved, by creating quantitative methods to measure to the complexity of DNA as an IDR to represent IDR and message passing mechanism separately or jointly.

### There is no back-propagation in human brain
The theory suggests that the human brain or any being definitely does not need back-propagation as a learning mechanism.
Using only prune and connect operations on neural linkages (synapses) to adjust the message passing pathways is sufficient for the brain to learn and adapt to new information.
As long as the linkages maintain a set of IDRs.

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

---

## Taking a step back
We the listing parallel of phenomenons and more potential applications on-going research might discover of the theory, we can make a strong call back to the theory
that the semantics of intelligence and learning.
- intelligence: IDR, strict, reliable, consistent
- learning: general, flexible, adaptable, evolving. human brain, GPT and nature selection each uses dramatically different mechanisms to achieve this.

---

## About this repository
This repository contains the code and resources for the research project

## Why project(repo) not paper?
The unique view of the theory being developed here follows and uses the concepts and wording wildly used in programming languages, distributed systems, and databases, which makes the theory more accessible to researchers from these fields, and also opens up more engineering-focused practitioners to understand the concepts.
Also we don't want to write a paper for the sake of writing a paper, that forcing the core subject of this theory, **semantics**, into the rigid format of one specific mathematical framework or formal system.
So we decided to use a tone between system design documents and semi-philosophical essays to present the ideas and concepts of the theory.

We would like everyone to be a part of the open research process, and we believe that sharing the ideas in an informal manner first will help us gather feedback and improve the theory before formalizing it into academic papers.
Why this is important? We would like to make the theory as theoretical and as structural as possible, so that it can be easily applied to various AI paradigms and models. That's why it is crucial to have a wide range of feedback from different perspectives, especially from those who are working on developing AI inference systems and training new models. We appreciate any feedback if you apply the theory and find interesting results or new methodologies derived from it.

Once the theory is more established and widely accepted, we plan to write formal papers to present the findings in a traditional academic format and submit them to well-suited tracks of conferences and journals of different fields and disciplines.

## Repository Structure
- `models/`: Implementations of various experimental AI models designed by applying the theory.
  - [torus-10](models/torus-10/README.md) exploits torus topology of pixels and  using database as KVCache to build GPT model for video generation.
- `research-log/`: A collection of research notes, experiments, and findings related to the project.
- `blogs/`: Informal blog posts discussing various aspects of commitment semantics and latent message passing.

## Contact
For questions, discussions, or collaborations, please open an issue or reach out to the original author
(Shenghang) directly via email: jackalcooper@gmail.com

## Citation
If you find this theory useful in your research or work, please consider citing it as follows:
```
@misc{shenghang2025commitment,
  author = {Shenghang},
  title = {Commitment Semantics with Latent Message Passing},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/AISemanticsStudy/commitment-semantics-with-latent-message-passing}},
  note = {A theory formalizing computational semantics of artificial intelligence}
}
```
