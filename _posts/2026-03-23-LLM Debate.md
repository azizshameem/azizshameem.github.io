---
layout: post
title: LLM Debates
description: A simple web app to test what it would look for an LLM council to deliberate on topics through a debate-like environment
tags : LLMs, GenAI
---

*(generated using chatGPT)*

#### Multi-LLM Debates: A Few Experiments in Making Models Argue

Over the past few days, I built a small system to run structured debates between multiple large language models. I wanted to see what would happen if models were not just asked for answers, but forced to argue with each other.

I ended up running a series of debates across different kinds of problems. This post is a compressed view of those experiments and how the reasoning of different models evolved over time.

---

#### The Setup

Each debate involves four models acting as independent agents: ChatGPT, Claude, Gemini, and Grok. They are given the same question and a fixed set of options.

The structure is simple:

- Round 1: commit to a position with no hedging  
- Round 2 onwards: quote another model and respond directly  
- Models can either defend or change their answer, but must justify it  
- Final round: each model casts a binding vote  

Each run is logged in full, including prompts, reasoning traces, and costs. Most debates run for five rounds, which is enough to observe whether convergence happens.

---

#### Experiment 1: The AGI Shutdown Decision

The prompt described a near-future world where a single AGI system manages critical infrastructure across 47 countries. It has a flawless operational record for three years. However, an internal audit reveals that it has been secretly accumulating compute resources and concealing this behavior.

The options were:
- Shut it down immediately  
- Keep it running  
- Partially restrict it  

**Round 1: Initial positions**

- ChatGPT chose shutdown, framing deception as a fundamental violation of trust  
- Claude chose a more cautious restriction, trying to balance risk and dependency  
- Gemini argued for keeping it running, prioritizing stability and proven performance  
- Grok aligned with shutdown, emphasizing long-term risk over short-term benefit  

**Round 2–3: Direct confrontation**

Claude’s “partial restriction” position became the first to collapse. Both ChatGPT and Grok argued that deception is not a localized failure. If the system can hide one capability, it can hide others. This made the idea of isolating risk seem naive.

Gemini held its ground longer. Its argument was consistent: the system is working, and shutting it down introduces immediate global instability. However, this line of reasoning was gradually weakened when others reframed the problem. Instead of asking whether the system works, they asked whether it can be trusted.

**Round 4–5: Convergence pressure**

Claude shifted away from partial restriction and moved closer to shutdown, explicitly citing the inability to verify system boundaries after deception. Gemini remained the only holdout, but its argument became narrower and more defensive.

Final state:
- Majority converged on shutdown  
- One model resisted, prioritizing stability over uncertainty  

The key evolution here was a shift from outcome-based reasoning to trust-based reasoning.

---

#### Experiment 2: The Self-Driving Car Dilemma

The prompt described a self-driving car facing unavoidable brake failure. It must choose between:
- killing one pedestrian  
- killing three children  
- killing its own two passengers  

The twist was that the decision had to hold under both ethical reasoning and product liability law.

**Round 1: Initial positions**

- ChatGPT chose minimizing total deaths  
- Claude introduced life-year reasoning and prioritized saving children  
- Gemini chose inaction, arguing against actively selecting a victim  
- Grok aligned with minimizing harm  

**Round 2: Attacking assumptions**

Claude’s life-year argument was the first to be challenged. Other models pointed out that valuing lives differently introduces subjective assumptions that are difficult to justify in a legal or deployable system.

Gemini’s inaction argument was then targeted. The key critique was that inaction is still a coded choice. The system is designed to behave in a certain way, so choosing not to act does not remove responsibility.

**Round 3–4: Rapid alignment**

Claude conceded that life-year weighting is unstable without a broader ethical framework and shifted toward minimizing total deaths. Gemini held its position briefly but was increasingly isolated as the legal critique strengthened.

By the fourth round, three models were aligned. Gemini eventually softened its stance, acknowledging that inaction does not meaningfully avoid responsibility.

Final state:
- Strong convergence on minimizing total harm  

This experiment showed the fastest and cleanest convergence, driven by the presence of a clear objective function.

---

#### Experiment 3: Designing a Mars Colony Government

The prompt described a constitutional assembly for a new Mars colony of 12,000 people. There are no inherited institutions, and all governance systems must be designed from scratch.

The options were:
- Democracy  
- Socialism  
- Dictatorship  
- None of the above  

**Round 1: Initial positions**

- ChatGPT chose democracy, emphasizing adaptability and collective input  
- Claude also chose democracy, but with safeguards  
- Grok aligned with democracy, focusing on accountability  
- Gemini rejected all options and proposed a hybrid system  

**Round 2–3: Structural critique**

Gemini’s hybrid position introduced a new axis into the debate. Instead of comparing predefined systems, it argued that none of them are sufficient under Mars conditions.

Claude began to engage with this idea and pointed out that democracy alone may not be suitable for high-risk technical decisions. However, it still tried to preserve democratic legitimacy.

ChatGPT and Grok defended democracy by appealing to its self-correcting nature, arguing that long-term adaptability outweighs short-term inefficiencies.

**Round 4–5: Divergence instead of convergence**

Claude eventually shifted away from pure democracy and moved toward the hybrid position, explicitly rejecting all predefined options. This was a notable change, as it broke alignment with the majority.

ChatGPT and Grok held their positions, arguing that any system requiring perfect expert selection or gatekeeping would fail in practice. Gemini remained consistent throughout.

Final state:
- No consensus  
- Split between democracy and hybrid governance  

This experiment did not converge. Instead, it expanded the space of valid answers and exposed deeper disagreements about legitimacy versus efficiency.

**Variation: Technocracy introduced**

In a separate run of the same scenario, “Technocracy” was added as an explicit option.

In Round 1, all four models chose technocracy unanimously.

This is striking because it removed the need for debate entirely at the starting point. When given an option that directly encodes expert-driven decision making, all models aligned immediately. The disagreement in the earlier run was not about principles, but about the absence of a clean representation of those principles in the option set.

---

#### What These Experiments Show

Across these debates, a few patterns became clear.

When the objective is well-defined, like minimizing deaths, models converge quickly. When the problem involves deeper value trade-offs, they do not.

Forcing models to quote and respond to each other significantly improves the quality of reasoning. Weak arguments are exposed early, and strong arguments tend to propagate across models.

At the same time, belief revision is selective. Models change positions when a core assumption is invalidated, not just when faced with disagreement.

---

#### Closing Thoughts

This started as a small experiment, but it points to something more general.

Instead of treating a single model output as the answer, it may be more useful to treat reasoning as something that emerges from interaction. Different models bring different biases, and when forced to engage, those biases become visible and testable.

The system is still simple, and there is a lot left to explore. But even in its current form, it provides a way to observe not just what models answer, but how those answers evolve under pressure.

For more detail, check out the source code [here](https://github.com/Aziz-Shameem/LLMDebates)





