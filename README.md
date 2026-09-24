# Adaptive Explainer

A lightweight Agent Skill for explanations that adapt to the user's known background and desired depth.

Instead of turning every question into a full tutoring session, Adaptive Explainer focuses on one thing: **bridge only the missing prerequisites, explain the target clearly, and let the user choose how deep to go next.**

## What it does

- Uses only supported evidence about the user's background; it does not invent a learner profile.
- Skips prerequisites the user already appears to know.
- Adds a minimal background bridge when needed.
- Gives a compact but complete default explanation.
- Supports follow-up depth modes such as:
  - shorter / TL;DR
  - more detailed / deep dive
  - first principles
  - mathematical / technical
  - examples / analogies
- Treats the conversation as cumulative, so "more detail" expands the previous answer instead of restarting it.

## Example

User:

```
I know Bayes' rule and likelihood. What is posterior predictive actually doing?
```

The skill should skip re-explaining Bayes' rule and likelihood, explain posterior predictive from those concepts, and offer deeper mathematical or example-driven follow-ups.

## Files

```
adaptive-explainer/
├── SKILL.md
└── agents/
    └── openai.yaml
```

## Install

### Agent Skills compatible agents

Copy the `adaptive-explainer` directory into the agent's skills directory.

### Codex

Project-local:

```text
.codex/skills/adaptive-explainer/
```

Or user-level:

```text
~/.codex/skills/adaptive-explainer/
```

### Other agents

If the agent supports the Agent Skills / `SKILL.md` convention, install the whole directory. If it does not, the body of `SKILL.md` can still be adapted into system or developer instructions.

## Download

A packaged `skill.zip` is included at the repository root for direct installation where ZIP upload is supported.
