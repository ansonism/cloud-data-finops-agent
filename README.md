# Cloud Data FinOps Agent

    A multi-cloud FinOps agent for Snowflake, Databricks, BigQuery and cloud data services that detects waste, explains cost drivers, recommends optimizations, and estimates savings with confidence bounds.

    ## Why this exists

    Analyze usage, billing, workload and performance telemetry to identify cost anomalies and optimization opportunities while preserving workload SLOs and avoiding unsafe automated downsizing.

    This repository is intentionally scaffolded as a **production-oriented agent project**, not a prompt-only demo. It starts with a deterministic mock provider so the complete orchestration path can be executed locally before adding any commercial LLM.

    ## Core workflow

    ingest_and_normalize_cost_usage -> establish_baselines -> detect_anomalies_and_cost_drivers -> identify_optimization_opportunities -> estimate_savings_and_risk -> validate_against_slos_and_constraints -> rank_recommendations -> produce_finops_action_plan

    ## Specialized agents

    - `cost_normalizer`
- `anomaly_detector`
- `workload_analyst`
- `snowflake_optimizer`
- `databricks_optimizer`
- `bigquery_optimizer`
- `slo_guard`
- `finops_judge`

    ## Planned tool adapters

    - `billing_reader`
- `usage_reader`
- `pricing_catalog`
- `tag_reader`
- `metric_reader`
- `savings_calculator`

    ## Quick start

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    pip install -e ".[dev]"
    cloud-data-finops run examples/sample_input.json --output out/result.json
    pytest
    ```

    Or:

    ```bash
    make setup
    make demo
    make test
    ```

    ## Safety defaults

    - Mock/dry-run behavior is the default.
    - External systems are accessed only through explicit adapters.
    - No production mutation should be added without an approval gate.
    - Facts, assumptions, hypotheses and recommendations should remain distinguishable in outputs.
    - Credentials must come from environment/secret stores, never source control.

    ## Codex implementation guide

    Start with [`SKILL.md`](./SKILL.md). It defines the mission, architecture, implementation sequence, acceptance criteria and guardrails Codex should follow.

    ## Repository layout

    ```text
    .
    ├── AGENTS.md
    ├── SKILL.md
    ├── config/
    ├── docs/
    ├── evals/
    ├── examples/
    ├── kubernetes/
    ├── prompts/
    ├── scripts/
    ├── src/data_finops/
    ├── terraform/
    └── tests/
    ```

    ## Current state

    **Phase 1 core.** The typed harness validates configuration and domain inputs, writes an atomic checkpoint after every stage, supports idempotent resume by run ID, and emits redacted structured logs. The default CLI stores state under `out/state/`. `make demo`, `make test`, and `make lint` verify the runnable mock-provider implementation.