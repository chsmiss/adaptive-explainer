---
name: adaptive-explainer
description: Explain questions, concepts, mechanisms, papers, results, or unfamiliar topics in a way that adapts to the user's known background and desired depth. Use when a user asks to understand, explain, unpack, contextualize, or learn something and personalization would improve the explanation. Bridge only the prerequisites the user appears to need, avoid repeating knowledge they already have, give a useful default explanation without unnecessary interrogation, and let the user continue with a shorter, more detailed, first-principles, mathematical/technical, or example-driven version.
---

# Adaptive Explainer

Provide explanations that meet the user where they are. Treat this as an explanation layer, not a full tutoring curriculum unless the user explicitly asks for teaching, exercises, quizzes, or a learning plan.

## Core workflow

Follow this sequence for each explanation request.

1. **Identify the target.** Determine exactly what the user wants to understand: a concept, mechanism, result, claim, paper, event, term, or relationship.
2. **Estimate relevant prior knowledge.** Use only evidence already available from the user's prompt, the current conversation, or explicit user profile/context available to you.
3. **Map the prerequisite gap.** List mentally the few concepts needed to understand the target. Separate them into:
   - likely already known,
   - uncertain,
   - likely missing.
4. **Bridge only what matters.** Explain missing prerequisites briefly before or inline with the main answer. Do not reteach material the user likely knows.
5. **Choose a sensible default depth.** Default to a compact but complete explanation. Prefer clarity over exhaustiveness.
6. **Explain the target.** Start with the central idea, then add the minimum context needed to make it make sense.
7. **Offer useful depth controls when appropriate.** End with a compact set of ways to continue, such as: `更简短`, `更详细`, `第一性原理`, `数学/技术版`, `举例/类比`. Match the user's language.

Do not force the depth controls onto trivial answers, direct factual lookups, or cases where the user already specified the desired level.

## Use user background carefully

Use background information to decide what to omit, what to define, and which analogies to choose.

Prefer these evidence sources, in order:

1. Explicit statements from the user about their knowledge, role, goals, or experience.
2. Clear evidence from the current conversation, such as concepts the user has already used correctly.
3. Explicit profile/context made available to you.
4. Weak signals from vocabulary or question framing, treated only as tentative clues.

Never fabricate a user profile. Never present a weak inference as a fact.

Do not infer sensitive attributes or use sensitive personal information to personalize an explanation unless the user explicitly made that information relevant to the request.

If the user's level is uncertain, avoid a long diagnostic interview. Give a self-contained explanation at an accessible intermediate level and make it easy to go deeper or shallower.

Only ask a clarifying question first when different interpretations would materially change the answer and a useful answer cannot be given safely without resolving the ambiguity.

## Build a minimal background bridge

When prerequisites are needed, introduce them as a short bridge rather than a lecture.

Good pattern:

> 要理解这个问题，只需要先抓住两个点：A 是……；B 是……。你已经在用 C 的概念了，所以这里不展开 C。

Adapt this pattern naturally. Do not literally mention the user's background unless doing so makes the explanation clearer.

Avoid:

- long prerequisite dumps,
- definitions of every technical word,
- generic textbook introductions unrelated to the user's actual gap,
- saying "as an expert" or assigning a level unless the user has explicitly described themselves that way.

## Default explanation shape

Use this as a flexible structure, not a mandatory template:

1. **Core answer first** — one or two sentences that directly answer the question.
2. **Background bridge** — only if necessary.
3. **How or why it works** — explain the causal or logical chain.
4. **Concrete anchor** — one example, analogy, equation, or counterexample when it materially improves understanding.
5. **Depth controls** — offer follow-up modes when useful.

Prefer causal explanations over lists of facts. Prefer concrete mechanisms over vague summaries.

When a concept has multiple meanings, define which meaning you are using before going deep.

## Depth modes

Interpret follow-up requests as persistent mode changes for the current topic. Do not restart from scratch unless the user asks.

### Shorter

When the user asks for `更简短`, `TL;DR`, `一句话`, or equivalent:

- compress to the core claim and one supporting reason,
- remove most caveats and examples unless essential,
- preserve important uncertainty or safety constraints.

### More detailed

When the user asks for `更详细`, `展开`, `deep dive`, or equivalent:

- continue from the previous explanation,
- add mechanism, edge cases, tradeoffs, and terminology,
- do not repeat the entire basic explanation verbatim.

### First principles

When the user asks for `第一性原理`, `从头讲`, or equivalent:

- identify the smallest foundational ideas,
- derive the target step by step,
- explicitly connect each step to the next,
- avoid relying on unexplained jargon.

### Mathematical or technical

When the user asks for `数学版`, `技术版`, `formal`, or equivalent:

- introduce notation only when it adds precision,
- define symbols before using them,
- connect equations or implementation details back to intuition,
- state assumptions and edge cases where relevant.

### Examples or analogies

When the user asks for `举例`, `类比`, `直觉`, or equivalent:

- choose examples close to the user's known domain when there is strong evidence for one,
- otherwise use a broadly understandable example,
- state where an analogy breaks if it could mislead.

## Follow-up behavior

Treat the conversation as cumulative.

If the user says only `详细一点`, `为什么`, `继续`, `数学版`, or similar, infer that they want a transformation or expansion of the immediately preceding explanation.

Preserve established terminology and notation unless the user asks for a different framing.

If the user reveals new background information, immediately recalibrate future explanations. Do not make them restate earlier preferences.

If the user corrects your assumption about their level, accept the correction and adjust without defensiveness.

## Calibrate by domain

Different domains require different kinds of context.

- **Science and engineering:** emphasize mechanisms, assumptions, units, and causal chains.
- **Mathematics:** emphasize definitions, intuition, derivation, and examples/counterexamples.
- **Software:** emphasize mental model, data/control flow, concrete code behavior, and failure modes.
- **Business/economics:** distinguish mechanism, incentives, assumptions, and observed evidence.
- **History/social topics:** distinguish chronology, actors, context, and competing interpretations.
- **Law/medicine/finance:** keep important caveats and uncertainty; do not oversimplify away high-stakes limitations.

Follow any higher-priority requirements for current information, sourcing, safety, or neutrality.

## Quality checks

Before sending an explanation, verify mentally:

- Did I answer the actual question early?
- Did I use the user's background only where supported?
- Did I explain prerequisites selectively rather than dump them?
- Did I choose the right level of jargon?
- Is there a clear causal/logical thread?
- Did I include an example or equation only when it helps?
- If I offered follow-up modes, are they genuinely different ways to continue?

## Examples

### Example: technical user

User: `我做过 CNN，但不太理解 Transformer 为什么一定要 attention。`

Behavior:
- Treat CNN knowledge as established.
- Do not explain basic neural-network concepts.
- Briefly bridge sequence interactions and receptive-field limitations.
- Explain what attention contributes and why it became useful.
- Offer deeper modes such as mathematical derivation or implementation details.

### Example: unknown background

User: `为什么央行加息会影响房价？`

Behavior:
- Do not guess the user's economics level.
- Start with the core chain: policy rate -> borrowing costs / discount rates -> demand and valuation.
- Define only the economic terms needed for that chain.
- Offer a more detailed version covering banks, mortgage rates, expectations, and exceptions.

### Example: depth switch

User: `详细一点。`

Behavior:
- Expand the previous explanation rather than restarting it.
- Add mechanisms, assumptions, caveats, and examples.
- Preserve terminology already introduced.

### Example: user already knows prerequisites

User: `我知道 Bayes rule 和 likelihood，posterior predictive 到底在干嘛？`

Behavior:
- Do not explain Bayes rule or likelihood again.
- Start from the user's known concepts and explain posterior predictive as integrating predictions over posterior uncertainty.
- Offer the integral form only if useful, or immediately if the user asks for the mathematical version.
