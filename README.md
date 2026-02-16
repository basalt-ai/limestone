<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/logo_white.png" />
  <source media="(prefers-color-scheme: light)" srcset="assets/logo.png" />
  <img src="assets/logo.png" alt="Limestone" width="200" />
</picture>

<br>

**Build LLM-as-a-judge evaluators you can trust** — Structured methodology for 100% reliable LLM judges.

**[Join Discord](https://discord.gg/yW2RyZKY)** · **[Share Your Pain Points](https://github.com/basalt-ai/limestone/discussions/1)**

<br>

![Build Status](https://github.com/basalt-ai/limestone/actions/workflows/test.yml/badge.svg)
[![npm version](https://img.shields.io/npm/v/@basalt-ai/limestone.svg)](https://www.npmjs.com/package/@basalt-ai/limestone)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Discord](https://img.shields.io/discord/1471362791884455980?color=7289da&label=Discord&logo=discord&logoColor=white)](https://discord.gg/yW2RyZKY)

<br />

### Part of the Basalt Stack

<p>
  <strong>Cobalt</strong> (Testing) + <strong>Diamond</strong> (Datasets) + <strong>Limestone</strong> (Judges) + <strong>Asphalt</strong> (Optimization)
</p>

</div>

---

## The Problem: LLM-as-a-Judge Is Fundamentally Unreliable

**Vague criteria that produce inconsistent scores.** You ask an LLM judge "Is this response helpful?" and get different answers for identical inputs. Your criteria are too subjective, your prompts are ambiguous, and your results are meaningless noise.

**Inconsistent scoring across identical inputs.** Run the same evaluation twice and get different scores. Your LLM judge is non-deterministic, temperature-sensitive, and completely unreliable for any serious evaluation work.

**Drift over time as models update.** Your LLM judge scores were calibrated on GPT-4, but now you're using a new model and all your baselines are broken. Every model update invalidates months of evaluation work.

**Never stress-tested before deployment.** You build an evaluator, run it on a few examples, and assume it works. No adversarial testing, no edge case validation, no reliability analysis. Then it fails spectacularly on real-world complexity.

**Poor agreement with human experts.** Your LLM judge disagrees with domain experts 40% of the time, but you have no systematic way to identify where it's wrong or how to fix the disagreements.

## Why This Kills AI Evaluation

**False confidence in model performance.** Your unreliable judge gives you meaningless scores that don't correlate with actual quality. You optimize for metrics that don't matter and deploy models that perform poorly.

**Wasted optimization cycles.** You spend weeks "improving" your model based on judge feedback that's inconsistent and untrustworthy. Every optimization is built on quicksand.

**No systematic quality assurance.** Without reliable evaluation, you can't confidently deploy AI systems or measure their real-world impact. You're shipping blindfolded.

**Expensive manual review.** When your automated judges fail, you fall back to slow, expensive human evaluation. Every production decision requires manual verification because you can't trust your tools.

**Inconsistent team decisions.** Different team members get different evaluation results, leading to conflicting priorities and wasted effort. Nobody knows what "good" actually means.

## What Should Exist Instead

**Expert feedback sessions** that systematically capture domain knowledge from multiple specialists and identify areas of agreement and disagreement.

**Structured criteria extraction** that transforms subjective evaluation into objective, measurable components with specific checks and validation logic.

**Reliability testing** that validates judge consistency across identical inputs, temporal stability, and agreement with expert consensus before deployment.

**Alignment datasets** that train judges to match expert opinion with high accuracy, focusing on disagreement cases and edge scenarios.

**100% reliability standards** with 95%+ expert agreement, <5% score drift over time, and consistent scoring across identical inputs.

## Join the Movement

We're building Limestone to make LLM judges actually reliable. But we need to understand your specific evaluation challenges first.

**[Tell us about your LLM judge struggles →](https://github.com/basalt-ai/limestone/discussions/1)**

What challenges do you face?
- Vague criteria that produce inconsistent scores?
- Drift over time as models update?
- Poor agreement with human experts?
- No way to validate judge reliability?
- Difficulty building structured evaluation criteria?

Your experiences directly shape what we build. Every reliability challenge shared helps us create better evaluation tools for the entire AI development community.

⭐ **Star this repo to follow our progress** — we'll be sharing our methodology for building trustworthy LLM evaluators as we validate the core problems.

---

**Built and maintained by [Basalt](https://getbasalt.ai). Open source forever under Apache 2.0.**