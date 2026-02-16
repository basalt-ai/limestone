<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/logo_white.png" />
  <source media="(prefers-color-scheme: light)" srcset="assets/logo.png" />
  <img src="assets/logo.png" alt="Limestone" width="200" />
</picture>

<br>

**Build LLM-as-a-judge evaluators you can trust** — Structured methodology for 100% reliable LLM judges.

**[Documentation](docs/)** · **[Join Discord](https://discord.gg/yW2RyZKY)**

<br>

![Build Status](https://github.com/basalt-ai/limestone/actions/workflows/test.yml/badge.svg)
[![npm version](https://img.shields.io/npm/v/@basalt-ai/limestone.svg)](https://www.npmjs.com/package/@basalt-ai/limestone)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-blue.svg)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20%2B-green.svg)](https://nodejs.org/)
[![Discord](https://img.shields.io/discord/1471362791884455980?color=7289da&label=Discord&logo=discord&logoColor=white)](https://discord.gg/yW2RyZKY)

<br />

### Part of the Basalt Stack

<p>
  <strong>Cobalt</strong> (Testing) + <strong>Diamond</strong> (Datasets) + <strong>Limestone</strong> (Judges) + <strong>Asphalt</strong> (Optimization)
</p>

</div>

---

## Table of Contents

- [Why Limestone](#why-limestone)
- [Quickstart](#quickstart)
- [Core Concepts](#core-concepts)
- [Expert Feedback Sessions](#expert-feedback-sessions)
- [Structured Evaluators](#structured-evaluators)
- [Alignment Datasets](#alignment-datasets)
- [Reliability Testing](#reliability-testing)
- [CLI](#cli)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## Why Limestone

Most LLM-as-a-judge evaluators are fundamentally unreliable. They use vague criteria ("is this response helpful?"), produce inconsistent scores across identical inputs, drift over time as models update, and are never properly stress-tested before deployment.

Limestone changes this. We provide a structured methodology to build LLM judges you can actually trust: expert feedback sessions to identify error categories, automatic extraction of structured criteria, conversion to reliable evaluators, and generation of alignment datasets. Our goal: 100% reliability in LLM evaluation.

## Quickstart

```bash
npm install @basalt-ai/limestone
npx limestone init
npx limestone create-judge --name "code-quality"
```

Start with expert feedback:

```typescript
// judges/code-quality.limestone.ts
import { judge, expertSession, criteria } from '@basalt-ai/limestone'

// Step 1: Run expert feedback session
const session = await expertSession({
  name: 'code-quality-feedback',
  domain: 'code-generation',
  experts: ['senior-dev-1', 'senior-dev-2', 'tech-lead'],
  samples: await loadSamples('./data/code-examples.json'),
  instructions: 'Review these AI-generated code snippets for quality, readability, and correctness.'
})

// Step 2: Extract structured criteria from feedback
const extractedCriteria = await limestone.extract({
  session: session,
  categories: ['correctness', 'readability', 'efficiency', 'style'],
  confidence: 0.85
})

// Step 3: Build structured evaluator  
const codeQualityJudge = judge('code-quality', {
  criteria: [
    criteria.correctness({
      weight: 0.4,
      checks: [
        'Does the code execute without errors?',
        'Does it produce the expected output?',
        'Are edge cases handled properly?'
      ]
    }),
    criteria.readability({
      weight: 0.3, 
      checks: [
        'Are variable names descriptive?',
        'Is the code structure logical?',
        'Are comments helpful and accurate?'
      ]
    }),
    criteria.efficiency({
      weight: 0.2,
      checks: [
        'Is the algorithm choice appropriate?',
        'Are there obvious performance issues?',
        'Is memory usage reasonable?'
      ]
    }),
    criteria.style({
      weight: 0.1,
      checks: [
        'Does it follow language conventions?',
        'Is formatting consistent?',
        'Are imports organized?'
      ]
    })
  ],
  model: 'gpt-5-mini',
  temperature: 0.1,
  consistency: { rounds: 5, threshold: 0.95 }
})

export default codeQualityJudge
```

```bash
npx limestone test --judge code-quality --reliability-check
npx limestone export --judge code-quality --format cobalt
```

## Core Concepts

### Expert Session

The foundation of reliable evaluation. Expert sessions capture domain knowledge from multiple specialists, identify common patterns in their feedback, and surface disagreement areas that need additional criteria.

```typescript
const session = await expertSession({
  name: 'customer-support-quality',
  domain: 'customer-service', 
  experts: ['support-manager', 'senior-agent', 'training-lead'],
  samples: 50, // Number of examples to review
  format: 'structured', // or 'freeform'
  consensus: 0.8 // Require 80% agreement for criteria extraction
})

// Session captures:
// - Individual expert ratings and feedback
// - Areas of agreement and disagreement  
// - Patterns in evaluation criteria
// - Edge cases that need special handling
```

### Structured Criteria

Transform subjective evaluation into objective, measurable criteria. Each criterion has specific checks, weights, and validation logic.

```typescript
const helpfulnessCriteria = criteria.custom({
  name: 'helpfulness',
  weight: 0.4,
  checks: [
    'Does the response directly address the customer's question?',
    'Are the suggested solutions actionable?', 
    'Is additional helpful context provided?',
    'Does it avoid unnecessary complexity?'
  ],
  validation: {
    type: 'binary', // pass/fail for each check
    aggregation: 'weighted-average',
    threshold: 0.75 // Need 75% of checks to pass
  }
})
```

### Alignment Dataset

Generate datasets that align LLM judges with expert opinion. These datasets are used to fine-tune or prompt-engineer judges for higher reliability.

```typescript
const alignmentDataset = await limestone.generateAlignment({
  session: 'customer-support-quality',
  judge: customerSupportJudge,
  size: 1000,
  strategy: 'disagreement-focused', // Focus on cases where judge disagrees with experts
  quality: 'high' // Only include high-confidence expert labels
})

// Use for prompt engineering
const optimizedJudge = await limestone.optimize({
  judge: customerSupportJudge,
  alignmentData: alignmentDataset,
  method: 'prompt-tuning', // or 'few-shot' or 'fine-tuning'
  target: 0.95 // Target 95% agreement with experts
})
```

## Expert Feedback Sessions

Limestone's expert sessions capture high-quality domain knowledge:

### Session Types

**Structured Sessions**: Experts evaluate examples using predefined rubrics
```bash
npx limestone session create --type structured --rubric ./rubrics/code-quality.yaml
```

**Freeform Sessions**: Experts provide open-ended feedback for criteria discovery
```bash
npx limestone session create --type freeform --domain "customer-support"
```

**Comparative Sessions**: Side-by-side comparison of outputs
```bash
npx limestone session create --type comparative --outputs-a ./outputs/model-a/ --outputs-b ./outputs/model-b/
```

### Expert Management

```bash
# Add experts to a session
npx limestone experts add --session code-quality --expert senior-dev-alex@company.com

# Track expert agreement rates
npx limestone experts stats --session code-quality

# Identify experts with consistently different perspectives
npx limestone experts analyze --outliers
```

### Session Analytics

```typescript
const analytics = await limestone.analyzeSession('customer-support-quality')

// Expert agreement analysis
console.log(analytics.agreement.overall) // 0.87
console.log(analytics.agreement.byExpert) // Individual expert reliability

// Criteria discovery
console.log(analytics.emergentCriteria) // Auto-discovered evaluation dimensions
console.log(analytics.edgeCases) // Examples with high disagreement

// Quality metrics
console.log(analytics.quality.consistency) // How consistent are expert judgments?
console.log(analytics.quality.coverage) // How well do criteria cover the domain?
```

## Structured Evaluators

Build evaluators that decompose complex judgments into measurable components:

### Built-in Criteria Types

```typescript
// Binary criteria (pass/fail)
criteria.accuracy({
  checks: ['Is the answer factually correct?', 'Are calculations accurate?'],
  weight: 0.5
})

// Scaled criteria (0-10 score)
criteria.creativity({
  scale: { min: 0, max: 10, step: 1 },
  anchors: {
    0: 'Generic, template-like response',
    5: 'Some original elements, mostly standard',
    10: 'Highly creative and original approach'
  },
  weight: 0.2
})

// Multi-choice criteria
criteria.tone({
  options: ['professional', 'casual', 'friendly', 'authoritative'],
  expected: 'friendly',
  weight: 0.1
})

// Custom criteria with validation logic
criteria.custom({
  name: 'code-security',
  validator: async (output) => {
    const issues = await securityAnalyzer.scan(output)
    return {
      score: issues.length === 0 ? 1.0 : Math.max(0, 1 - issues.length * 0.2),
      details: issues,
      passed: issues.length === 0
    }
  },
  weight: 0.3
})
```

### Judge Configuration

```typescript
const reliableJudge = judge('content-quality', {
  criteria: [accuracyCriteria, creativityCriteria, toneCriteria],
  
  model: 'gpt-5-mini',
  temperature: 0.0, // Maximum consistency
  
  consistency: {
    rounds: 3, // Run evaluation 3 times
    threshold: 0.9, // Require 90% agreement across rounds
    tiebreaker: 'majority' // How to resolve disagreements
  },
  
  validation: {
    expertAlignment: 0.85, // Must agree with experts 85% of the time
    stability: { days: 30, threshold: 0.95 }, // Stable over 30 days
    crossModel: true // Test with multiple models
  },
  
  output: {
    format: 'structured',
    includeReasoning: true,
    confidence: true // Include confidence scores
  }
})
```

## Alignment Datasets

Generate training data to align LLM judges with expert opinion:

### Generation Strategies

```typescript
// Focus on cases where current judge disagrees with experts
const disagreementDataset = await limestone.generateAlignment({
  strategy: 'disagreement-focused',
  judge: currentJudge,
  expertSession: 'content-quality-session',
  size: 500
})

// Balanced dataset covering full range of quality
const balancedDataset = await limestone.generateAlignment({
  strategy: 'balanced',
  distribution: 'uniform', // Equal samples across quality levels
  size: 1000
})

// Hard examples for stress testing
const hardExamplesDataset = await limestone.generateAlignment({
  strategy: 'adversarial',
  difficulty: 'high',
  focus: ['edge-cases', 'ambiguous-examples'],
  size: 200
})
```

### Dataset Quality Validation

```bash
# Validate alignment dataset quality
npx limestone validate --dataset alignment-v1.json --experts 3 --agreement 0.8

# Check for label quality issues
npx limestone analyze --dataset alignment-v1.json --issues labels

# Test dataset distribution
npx limestone analyze --dataset alignment-v1.json --distribution quality-score
```

## Reliability Testing

Ensure your judges perform consistently before deployment:

### Consistency Testing

```bash
# Test same-input consistency
npx limestone test --judge content-quality --consistency --rounds 10

# Test temporal stability  
npx limestone test --judge content-quality --stability --days 7

# Test cross-model consistency
npx limestone test --judge content-quality --cross-model --models gpt-5-mini,claude-3
```

### Expert Agreement Validation

```typescript
const validation = await limestone.validateAgainstExperts({
  judge: contentQualityJudge,
  expertSession: 'content-quality-session',
  testSet: 200, // Use 200 expert-labeled examples
  metrics: ['accuracy', 'precision', 'recall', 'f1'],
  threshold: 0.9 // Require 90% agreement
})

if (!validation.passed) {
  console.log('Judge failed validation:')
  console.log(validation.issues) // Specific disagreement patterns
  console.log(validation.recommendations) // How to improve
}
```

### Stress Testing

```bash
# Test on edge cases and adversarial examples
npx limestone stress-test --judge content-quality --type adversarial

# Test with distribution shift
npx limestone stress-test --judge content-quality --type drift --shift sentiment

# Test with noisy inputs
npx limestone stress-test --judge content-quality --type robustness --noise 0.1
```

## CLI

```bash
limestone init                          # Initialize Limestone project
limestone session create               # Create expert feedback session
limestone session analyze              # Analyze session results  
limestone extract --session <name>     # Extract criteria from session
limestone create-judge --name <name>   # Create new structured judge
limestone test --judge <name>          # Run reliability tests
limestone optimize --judge <name>      # Optimize judge using alignment data
limestone export --judge <name>        # Export judge for use in other tools
limestone validate --dataset <path>    # Validate alignment dataset
limestone serve --mode review          # Start expert review interface
```

## Roadmap

Limestone is open source and community-driven. [Tell us what matters to you](https://github.com/basalt-ai/limestone/discussions/1).

| Status | Feature |
|--------|---------|
| :construction: | **Expert session framework** - Capture and analyze expert feedback |
| :construction: | **Criteria extraction** - Auto-extract structured criteria from sessions |
| :crystal_ball: | **Structured evaluators** - Build reliable, decomposed LLM judges |
| :crystal_ball: | **Alignment datasets** - Generate expert-aligned training data |
| :crystal_ball: | **Reliability testing** - Comprehensive validation and stress testing |
| :crystal_ball: | **Judge optimization** - Automatic prompt tuning and few-shot learning |
| :crystal_ball: | **Expert interface** - Web UI for session management and review |
| :crystal_ball: | **Enterprise features** - Advanced analytics, audit trails, compliance |

⭐ **Star this repo to follow progress**

## Contributing

We welcome contributions! See our **[Contributing Guide](CONTRIBUTING.md)** for development setup, code standards, and PR process.

- **Report bugs**: [Open an issue](https://github.com/basalt-ai/limestone/issues)
- **Request features**: [GitHub Discussions](https://github.com/basalt-ai/limestone/discussions)
- **Join Discord**: [Basalt Community](https://discord.gg/yW2RyZKY)

Built and maintained by [Basalt](https://getbasalt.ai). Open source forever under Apache 2.0.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.