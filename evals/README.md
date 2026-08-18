# Evaluation plan

    Start with deterministic evals against the mock/fake adapters, then add provider-backed eval runs.

    Domain acceptance targets from `SKILL.md`:

    - Recommendations separate measured cost from estimated savings.
- Savings estimates include assumptions and confidence.
- No destructive resize/termination action runs by default.
- Recommendations are filtered against workload SLOs.
- Sample scenarios cover idle compute, overprovisioning, inefficient queries and retention/storage waste.

    Do not use an LLM judge as the sole source of truth for safety-critical or mechanically verifiable assertions.

Phase 1 eval cases are validated against the strict `EvalCase` contract. They declare required stages and findings, forbidden findings/actions, an expected risk range, and minimum evidence coverage. The suite runs deterministically with `MockProvider` and requires no network access or model judge.
