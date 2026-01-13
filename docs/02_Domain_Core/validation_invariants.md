# 🏛️ Validation Invariants: The Guardrails of Truth (SOTA 2026)

## 1. Individual Invariants (Atomic Value Object Laws)

These rules are enforced at the moment of creation for each sub-component. If these fail, the component cannot exist.

- **Spatial Boundary:** `pickup_id` and `dropoff_id` must follow the `ZONE_` prefix protocol.
- **Occupancy Boundary:** `passenger_count` must be between 0 and 9.
- **Financial Boundary:** All monetary components (fare, taxes, tolls) must be non-negative.
- **Rationale:** To block data corruption at the most granular level before it reaches the orchestrator.

## 2. Relational Invariants (Global Entity Laws)

These rules are enforced by the `TaxiTrip` Aggregate Root. They govern the relationship between multiple Value Objects.

### A. Physics Engine (Velocity Guard)

- **Rule:** Velocity must not exceed 125 mph.
- **Logic:** `distance_miles / (duration_minutes / 60)`.
- **Rationale:** NYC urban traffic physics and legal limits. Anything above is flagged as `PhysicalImpossibilityError`.

### B. Temporal Integrity (Time Sequence)

- **Rule:** `duration_minutes` must be a positive non-zero value.
- **Logic:** `dropoff_at - pickup_at`.
- **Rationale:** Blocks "Time Travel" anomalies where the trip ends before it starts.

### C. Financial Audit (Arithmetic Integrity)

- **Rule:** Calculated sum of sub-charges must match the `total_amount`.
- **Logic:** `abs(actual - calculated) <= 0.01`.
- **Rationale:** Protects against floating-point errors and ghost charges.

## 3. Enforcement Strategy (Atomic Defense)

- **Layer:** All validation is strictly contained within the **Domain Core**.
- **Action:** No generic `validate()` calls. Validation is automatic during instantiation (`__post_init__`).
- **Outcome:** If an invariant fails, a `DomainValidationError` is raised immediately, halting the pipeline.

## 4. Sovereign Error Mapping

| Violation Type | Sovereign Code | Exception Class | Severity |
| :--- | :--- | :--- | :--- |
| Velocity Violation | `ERR_DOM_VAL_001` | `PhysicalImpossibilityError` | CRITICAL |
| Financial Mismatch | `ERR_DOM_VAL_002` | `FinancialMismatchError` | CRITICAL |
| Spatial Protocol | `ERR_DOM_VAL_007` | `SpatialIntegrityError` | HIGH |
| Temporal Anomaly | `ERR_DOM_VAL_013` | `TemporalAnomalyError` | HIGH |

______________________________________________________________________

*"Invariants are not suggestions; they are the physical laws of our digital sanctuary."*
