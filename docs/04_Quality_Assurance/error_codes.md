# 🏛️ Standardized Error Taxonomy: The Sovereign Alert System

## 1. Error Governance (The Data Signal Protocol)

In the Sovereign Sanctuary, exceptions are not mere failures; they are **Structured Data Signals**. Generic Python exceptions are strictly forbidden. Every failure must emit a **Sovereign Error Code** to enable automated telemetry, precise data filtering, and self-healing pipelines.

## 2. Code Anatomy: `ERR_[LAYER]_[TYPE]_[SEQ]`

- **LAYER:** `DOM` (Domain Sanctuary), `INF` (Infrastructure), `APP` (Application).
- **TYPE:** `VAL` (Validation), `SYS` (System/IO), `ML` (Machine Learning).
- **SEQ:** A three-digit unique identifier.

## 3. The Central Error Registry (The Guard)

### A. Domain Sanctuary (Refinery Gates)

These errors are raised within the `Domain Core` to prevent "Dirty Data" from polluting the ML engine. All inherit from `DomainValidationError`.

| Code | Class | Category | Rationale |
| :--- | :--- | :--- | :--- |
| `ERR_DOM_VAL_001` | `PhysicalImpossibilityError` | Physics | Velocity exceeds the 125 mph NYC safety ceiling. |
| `ERR_DOM_VAL_002` | `FinancialMismatchError` | Integrity | Total amount mismatches the sum of charges (Audit failure). |
| `ERR_DOM_VAL_007` | `SpatialIntegrityError` | Protocol | Identifiers fail the `ZONE_` prefix or TLC Rate Code standard. |
| `ERR_DOM_VAL_011` | `PhysicalImpossibilityError` | Occupancy | Passenger count or distance exceeds physical vehicle limits. |
| `ERR_DOM_VAL_013` | `TemporalAnomalyError` | Temporal | Trip duration is non-positive (Logical time reversal). |

### B. Infrastructure & Data Engine (The Laborers)

*To be implemented within the Adapters.*

| Code | Category | Description |
| :--- | :--- | :--- |
| `ERR_INF_POL_001` | Data Ingestion | **Polars Engine:** Failure to scan Parquet due to schema mismatch. |
| `ERR_INF_ML_001` | Inference | **Model Registry:** Failure to load weights or invalid input tensor. |

## 4. Handling & Resilience Policy

1. **Atomic Propagation:** Domain errors must be raised immediately upon instantiation (`__post_init__`).
1. **Refinery Logic:** During batch processing, records triggering `ERR_DOM_VAL_XXX` must be diverted to a "Dirty Data" sink (Log/DB) while valid entities proceed to the ML Inference engine.
1. **Traceability:** Every error signal must be paired with the `source_id` and `route_key` for industrial auditability.
1. **Authoritative Tone:** Error messages must be objective, technical, and avoid personal pronouns (SDDL Standard).

______________________________________________________________________

*"In the Sovereign Sanctuary, an error is an informative signal designed to protect the model's intelligence."*
