# Limestone

**LLM-as-a-judge evaluators are fundamentally broken. We're building ones you can trust.**

---

## The LLM Judge Reliability Crisis

Every AI team using LLM-as-a-judge hits the same nightmare: **evaluators that can't be trusted.**

Your "helpful response" judge gives different scores to identical inputs. Your "accuracy" evaluator drifts over time as models update. Your criteria are so vague ("is this good?") that even humans disagree on what they mean.

**The brutal truth:** You're making critical AI decisions based on evaluators that are less consistent than a coin flip.

You've built evaluation pipelines on quicksand. Your judges work fine in demos, fail spectacularly in production, and nobody knows why. The worst part? You only discover this after shipping to users.

---

## Why LLM Judges Fail

**Vague criteria create chaos.** "Is this response helpful?" means something different to every reviewer and every model run.

**Zero consistency testing.** Your judge passes eval on Monday, fails the same examples on Tuesday. Did your AI get worse, or did your judge?

**No expert alignment.** Your LLM judge thinks it's great, your domain experts disagree. Who do you trust?

**Drift is invisible.** Model updates break your judges in subtle ways you won't catch until it's too late.

---

## The Basalt Stack

Limestone is part of a complete AI evaluation ecosystem:

- **[Cobalt](https://github.com/basalt-ai/cobalt)** — CI-native testing for AI agents
- **[Diamond](https://github.com/basalt-ai/diamond)** — Dataset engine for AI evals
- **[Limestone](https://github.com/basalt-ai/limestone)** — Build trustworthy LLM-as-a-judge evaluators ← *You are here*
- **[Asphalt](https://github.com/basalt-ai/asphalt)** — Self-improving engine for production AI agents

---

## ⭐ Star this repo to follow progress

We're building Limestone in the open. Star this repo to get notified about major updates and releases.

## 💬 Join the discussion

Struggling with unreliable LLM judges? [Join the conversation](https://github.com/basalt-ai/limestone/discussions) and help us build evaluation you can trust.

Built and maintained by Basalt. Open source forever under Apache 2.0.