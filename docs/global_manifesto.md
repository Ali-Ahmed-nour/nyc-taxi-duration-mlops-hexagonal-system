# 🏛️ Global Manifesto: The Sovereign Tech Stack (2026)

## 1. Governance & Authority

This manifesto dictates the official engineering protocols for the NYC Taxi Predictive Platform. Adherence is non-negotiable to ensure industrial-grade reliability. All modifications must be ratified by the **Principal Architect (Ali)**.

## 2. Execution Environment & Tooling (SOTA)

- **Runtime:** Python 3.12.3+ (Mandatory type safety and performance features).
- **Environment Manager:** **uv project** (Mandatory).
  - *Rationale:* Sub-second dependency resolution and deterministic builds via `uv.lock`.
- **Project Configuration:** `pyproject.toml` is the **Single Source of Truth** for all metadata and tool orchestrations (Ruff, Pyright).

## 3. Data & ML Architecture

- **Data Engine:** **Polars (Lazy API)**.
  - *Mandate:* All ingestion must utilize the Lazy API for query optimization. Eager execution is forbidden in production to preserve memory sovereignty.
- **The Registry Pattern:** All ML inferences must be stored in the `predictions: dict[str, float]` registry within Domain Entities.
  - *Rationale:* Decouples core logic from model proliferation, allowing horizontal scaling of AI tasks.
- **Refinery Workflow:** Data is treated as "Raw Ore" that must be refined by the Domain Core's validation before reaching the ML Inference engine.

## 4. Engineering DNA (Sovereign Standards)

- **Memory Efficiency:** All domain objects mandate `slots=True` and `frozen=True`.
- **The Sanctuary Rule:** The `Domain Core` is a dependency-free zone (Standard Python only).
- **Atomic Defense:** Self-guarding entities via `__post_init__` validation. Legacy `validate()` methods are deprecated.
- **SDDL Documentation:** Mandatory **Action/Logic/Rationale** headers in all docstrings. Language: Strictly English.

## 5. Error & Telemetry Protocol

- **Sovereign Codes:** Errors are **Data Signals** with structured codes (e.g., `ERR_DOM_VAL_001`).
  - `DOM`: Domain Sanctuary failures.
  - `INF`: Infrastructure/Adapter failures.
  - `APP`: Orchestration failures.
- **Traceability:** Every signal is paired with a `source_id` for industrial auditing.

## 6. Quality & Reliability Guardrails

- **Linter/Formatter:** **Ruff** (The industrial standard for speed and precision).
- **Static Analysis:** **Pyright** (Ensuring type-safe data pipelines).
- **Stress Testing:** **Hypothesis** for Property-Based Testing (PBT) to simulate urban edge cases.
- **Mocking:** **Factory-Boy** for high-fidelity synthetic data generation.

## 7. The Agnostic Clause

The platform is designed to outlast the tools. Libraries, databases, and ML frameworks are **Disposable Gears**. The `Domain Core` remains the only permanent, protected, and immutable asset.

______________________________________________________________________

*"Architected for the Future of Urban Transit. Designed to Outlast the Tools."*
