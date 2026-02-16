# Contributing to Limestone

We're excited you want to help build the future of reliable LLM evaluation! This guide will help you get started.

## Quick Start

1. **Fork and clone**
   ```bash
   gh repo fork basalt-ai/limestone --clone
   cd limestone
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run tests**
   ```bash
   npm test
   ```

4. **Make changes and verify**
   ```bash
   npm run build
   npm run lint
   npm test
   ```

## Development Setup

### Prerequisites

- **Node.js** 20+ and npm
- **TypeScript** 5.7+
- **Git** with GitHub CLI (`gh`) recommended

### Project Structure

```
limestone/
├── src/
│   ├── core/          # Core judge and criteria logic
│   ├── sessions/      # Expert feedback session management
│   ├── alignment/     # Dataset generation and alignment
│   ├── validation/    # Reliability testing and validation
│   ├── optimization/  # Judge tuning and improvement
│   └── cli/           # Command-line interface
├── examples/          # Example judges and sessions
├── docs/              # Documentation
└── tests/             # Test files
```

### Running Locally

```bash
# Build and watch for changes
npm run dev

# Run CLI locally  
./bin/limestone.js --help

# Run specific tests
npm test -- --grep "expert session"
```

## What We're Looking For

### High Priority
- **Expert session interfaces** for different domains (code, content, support, etc.)
- **Criteria extraction algorithms** that identify patterns in expert feedback
- **Judge reliability metrics** beyond basic accuracy
- **Integration with evaluation platforms** (Cobalt, LangSmith, Braintrust)

### Medium Priority  
- **Judge optimization algorithms** (prompt tuning, few-shot selection)
- **Stress testing frameworks** for adversarial examples
- **Expert management tools** (recruitment, tracking, analytics)
- **Performance optimizations** for large-scale evaluation

### Lower Priority
- **UI components** for expert review interfaces
- **Advanced analytics** and reporting
- **Compliance and audit features**
- **Documentation improvements**

## Contribution Guidelines

### Code Style

We use Biome for linting and formatting:

```bash
# Check formatting and lints
npm run lint

# Auto-fix issues
npm run lint:fix

# Format code
npm run format
```

**Key conventions:**
- Use TypeScript with strict settings
- Prefer composition over inheritance
- Write self-documenting code with clear names
- Add JSDoc comments for public APIs
- Keep functions focused and testable

### Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add expert session analytics for disagreement detection
fix: handle empty feedback gracefully in criteria extraction
docs: add quickstart guide for structured evaluators
test: add integration tests for judge validation
```

### Pull Request Process

1. **Create a feature branch** from `main`
   ```bash
   git checkout -b feat/your-feature-name
   ```

2. **Make focused changes** - one feature/fix per PR

3. **Add tests** for new functionality
   ```bash
   # Add tests in tests/
   npm test -- --coverage
   ```

4. **Update documentation** if you change APIs or add features

5. **Ensure CI passes**
   - All tests pass
   - Linting passes
   - Type checking passes  
   - Coverage meets threshold

6. **Write a clear PR description**
   - What problem does this solve?
   - What approach did you take?
   - How was it tested?
   - Any breaking changes?

### Testing

We use Jest for testing:

```bash
# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run specific test file
npm test -- tests/judge.test.ts

# Generate coverage report
npm test -- --coverage
```

**Test categories:**
- **Unit tests**: Test individual functions and classes
- **Integration tests**: Test expert sessions and judge workflows
- **End-to-end tests**: Test CLI and complete pipelines
- **Reliability tests**: Test judge consistency and agreement

### Documentation

Update docs when you:
- Add new features or change APIs
- Fix bugs that affect usage patterns
- Add new examples or use cases

```bash
# Build docs locally
npm run docs:build

# Serve docs for development
npm run docs:dev
```

## Expert Feedback & Domain Knowledge

Limestone depends on high-quality expert feedback. If you have domain expertise in:

- **Code quality evaluation**
- **Content and writing assessment**
- **Customer support evaluation**
- **Scientific/technical accuracy**
- **Creative evaluation**

Consider contributing by:
- Participating in expert sessions
- Reviewing judge criteria
- Providing domain-specific examples
- Validating judge performance in your area

## Getting Help

- **Questions?** Open a [GitHub Discussion](https://github.com/basalt-ai/limestone/discussions)
- **Found a bug?** [File an issue](https://github.com/basalt-ai/limestone/issues)
- **Need real-time help?** Join our [Discord](https://discord.gg/yW2RyZKY)
- **Expert sessions?** Contact us about domain expertise contributions

## Areas Needing Expertise

We especially welcome contributions in:

### Evaluation Science
- **Psychometrics** - Reliability and validity testing
- **Statistical methods** - Agreement metrics, significance testing
- **Experimental design** - A/B testing for judges, bias detection

### Machine Learning  
- **Fine-tuning** - Methods for aligning judges with expert feedback
- **Active learning** - Smart sampling for alignment datasets
- **Calibration** - Improving judge confidence estimates

### Domain Applications
- **Medical/healthcare** - Clinical accuracy evaluation
- **Legal** - Contract and document analysis
- **Financial** - Risk assessment and compliance
- **Education** - Automated grading and feedback

## Code of Conduct

Be respectful, inclusive, and constructive. We're building tools that help people evaluate AI systems fairly and accurately.

Key principles:
- **Be collaborative** - Different perspectives strengthen evaluation
- **Be rigorous** - Reliability requires careful methodology  
- **Be practical** - Focus on real-world evaluation needs
- **Be ethical** - Consider bias, fairness, and responsible use

## Recognition

Contributors are recognized in:
- **README.md** - Major contributors listed
- **Release notes** - Contributors credited for their changes
- **Expert contributor program** - Special recognition for domain experts
- **Conference talks** - Opportunities to present contributions

## Questions?

Don't hesitate to reach out! Open a discussion, join Discord, or tag @basalt-ai in your PR.

Thanks for helping make LLM evaluation more reliable! 🔬