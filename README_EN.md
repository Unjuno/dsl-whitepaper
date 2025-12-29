# Distributed Specialist Learning (DSL)

**English**: This document | **日本語**: [README.md](README.md)

**DSL is not a "single powerful model" but a "distributed system that provides powerful responses".**

The goal is to enable participants to use "powerful responses" locally (PC/browser) without requiring massive GPUs through distributed learning.

## Why speed-only optimization fails

Optimizing only for speed leads to "fast garbage" (short templates, refusals, meaningless outputs) winning.
DSL prevents this with **Verifier (quality gate) + composite reward function**.

## Architecture

DSL adopts a three-layer structure:

- **Exploration Layer (distributed)**: Creates winner logs through multi-model competition and cultivates specialists
- **Execution Layer (local)**: Selector invokes only a few models for fast response
- **Governance Layer (institution)**: Proxy replacement, specialist model proliferation/pruning, supply chain security

For detailed architecture diagrams and data flows, see [WHITEPAPER.md](WHITEPAPER.md).

## MVP: JSON Transformation Task

Initial success condition: A model specialized for JSON transformation passes the verifier (schema validation) and wins based on the balance of quality and speed.

**Recommended**: Start with domains where verifiers are cheapest (JSON transformation, code generation, etc.)

## About This Project

**This proposal intentionally provides no reference implementation.**
**The goal is to enable independent verification and falsification.**

Implementation is delegated to the community, and we promote distributed verification by clearly defining specifications and protocols.

For details, see [WHITEPAPER.md](WHITEPAPER.md) or [WHITEPAPER_JP.md](WHITEPAPER_JP.md) (Japanese).

## Quick Start (For Implementers)

**Get started in 5 minutes**: See [QUICK_START_EN.md](QUICK_START_EN.md).

1. Read [DSL_PROTOCOL_V0_1_EN.md](DSL_PROTOCOL_V0_1_EN.md) (5 minutes)
2. Check [examples/](examples/) samples
3. Declare the feature you want to implement in [Issues](https://github.com/Unjuno/dsl-whitepaper/issues)

## Help Wanted

Major components that need implementation:

- [ ] **MVP runner** - Basic execution environment (1 specialist model + verifier)
- [ ] **q1 metrics** - Quality proxy implementation
- [ ] **audit set** - Audit set creation and execution

For details, see [CONTRIBUTING_EN.md](CONTRIBUTING_EN.md).

## Documentation

### For Implementers (Read First)

- [QUICK_START_EN.md](QUICK_START_EN.md) - 5-minute quick start guide
- [DSL_PROTOCOL_V0_1_EN.md](DSL_PROTOCOL_V0_1_EN.md) - Protocol summary (for implementers)
- [CONTRIBUTING_EN.md](CONTRIBUTING_EN.md) - Contribution guidelines

### Theory & Specifications

- [WHITEPAPER.md](WHITEPAPER.md) - Full theory & specifications (v1.3) - English **← Main document**
- [WHITEPAPER_JP.md](WHITEPAPER_JP.md) - Full theory & specifications (v1.3) - Japanese **← Main document**
- [SPECIALIST_MODEL_DEFINITION.md](SPECIALIST_MODEL_DEFINITION.md) - Specialist model definition (supplementary)
- [METRICS_AND_AUDIT.md](METRICS_AND_AUDIT.md) - Metrics and audit specifications (supplementary)
- [MODEL_RESPONSE_SPEED.md](MODEL_RESPONSE_SPEED.md) - Technical explanation of model response speed (supplementary)

### Project Information

- [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) - Project structure guide
- [LICENSE_INFO.md](LICENSE_INFO.md) - License information

### Samples & Schemas

- [examples/](examples/) - Sample files
- [schemas/](schemas/) - JSON Schema definitions

## Project Goals

**"Enable everyone to use powerful models locally"**

- ✅ Inference works locally (runs on general PCs/browsers)
- ✅ Learning runs in a distributed manner (participants can create and submit specialized diffs in their areas of expertise)
- ✅ Institutionally robust (prevents fast garbage, single dominance, supply chain pollution, model proliferation)

## License

Apache-2.0

For details, see [LICENSE_INFO.md](LICENSE_INFO.md).
