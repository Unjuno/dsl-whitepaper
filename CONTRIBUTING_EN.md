# Contributing to DSL

Contributions to the DSL project are welcome!

## How to Participate

1. **Declare the feature you want to implement in Issues**
   - Check existing Issues
   - Use [Issue templates](.github/ISSUE_TEMPLATE/) for new issues
   - Recommended to start with Issues labeled "Help Wanted"

2. **Share design before implementation**
   - Share design proposals in Discussions (recommended)
   - Direct PR is acceptable for small changes

3. **When submitting PR, include:**
   - Implementation description
   - Test results
   - Protocol compliance verification
   - Documentation updates (as needed)

## Implementation Priorities

### Phase 1: MVP (Minimum Implementation)

**Goal**: Basic operation verification

- [ ] **MVP runner**
  - 1 specialist model + verifier
  - Basic winner selection logic
  - Log output in run_log.jsonl format

- [ ] **Basic Verifier Implementation**
  - JSON Schema validation (recommended: cheapest)
  - Or Unit Test validation

- [ ] **Model Manifest Validation**
  - YAML format loading
  - Required field validation

### Phase 2: Protocol Completion

**Goal**: Full protocol specification implementation

- [ ] **Metric Registry Implementation**
  - metric_v1 implementation
  - Reward function implementation
  - metric_version logging

- [ ] **Audit Set Execution**
  - Audit set loading
  - Automatic validation execution

- [ ] **Selector Implementation**
  - Basic routing
  - Training data collection (from winner logs)

### Phase 3: Distributed Participation

**Goal**: Enable distributed participation

- [ ] **Model Registry**
  - Model list management
  - Version management

- [ ] **Supply Chain Verification**
  - Hash verification
  - Manifest verification
  - Signature verification (future)

- [ ] **Selector Training**
  - Learning from winner logs
  - Inference-time routing optimization

## Coding Guidelines

### Protocol Compliance First

- Follow existing schema definitions ([schemas/](schemas/))
- Comply with Model Manifest format
- Comply with Run Log format

### Tests are Required

- Implement tests including Verifier
- Protocol compliance tests
- Operation verification with sample data

### Documentation

- Update documentation for implemented features
- Provide sample code (when possible)

## Questions & Discussions

- **Technical questions**: Use "Question" label in Issues
- **Design discussions**: Use Discussions
- **Bug reports**: Use "Bug" label in Issues

## Implementation Examples

Samples for implementation reference:

- [examples/basic_manifest.yaml](examples/basic_manifest.yaml) - Model Manifest example
- [examples/run_log_sample.jsonl](examples/run_log_sample.jsonl) - Run Log example
- [schemas/](schemas/) - JSON Schema definitions

## Commit Messages

Recommended format:

```
[IMP] Brief description of implementation

- Change 1
- Change 2
```

Example:
```
[IMP] MVP runner implementation

- Basic winner selection logic implementation
- Log output in run_log.jsonl format
- Model Manifest loading functionality
```

## Review Process

1. After PR submission, automatic checks (CI) run
2. Maintainers review
3. Fix based on feedback
4. Merge after approval

## Code of Conduct

- Provide constructive feedback
- Follow protocol specifications
- Respect the community

## License

Code contributions must comply with the project license (Apache-2.0).
