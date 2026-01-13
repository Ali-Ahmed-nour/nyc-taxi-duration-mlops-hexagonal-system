# 🏛️ Unified Domain Entity: TaxiTrip (SOTA 2026)

## 1. The Sovereign Source of Truth

The `TaxiTrip` entity is a **Sovereign Aggregate Root** representing a single journey. It is engineered to be the single point of coordination between raw data, physical laws, and multiple AI model outputs.

## 2. Technical Blueprint (Industrial Standards)

To ensure the system can handle massive throughput (Millions of rows via Polars) with zero corruption, the entity mandates:

- **`__slots__ = True`**: Optimized memory layout by preventing the creation of `__dict__`.
- **`frozen = True`**: Strict immutability to ensure the entity remains a constant throughout the pipeline.
- **SDDL Documentation**: Every logic block follows the **Action/Logic/Rationale** protocol.

## 3. The Sovereign Composition (Schema)

The entity is composed of specialized Value Objects that handle their own internal integrity:

| Component | Type | Responsibility |
| :--- | :--- | :--- |
| `location` | `TripLocation` | Spatial identifiers and TLC Rate Codes. |
| `temporal` | `TripTemporal` | Timestamps, Duration, and Seasonality. |
| `financials` | `TripFinancials` | Fare components and arithmetic audit. |
| `occupancy` | `TripOccupancy` | Physical distance and passenger count. |
| **`predictions`** | **`Dict[str, float]`** | **The Registry:** Storage for swappable ML model outputs. |

## 4. The Registry Pattern (The AI Hub)

Instead of anemic models with fixed fields, we use a **Dynamic Registry**. This allows the entity to scale horizontally across different ML tasks:

- **Logic:** `predictions` maps a model's signature to its result.
- **Example:** - `predictions["trip_duration_v1"] = 1240.5`
  - `predictions["fare_estimate_xgboost"] = 18.75`

## 5. Domain Logic: Atomic Defense

The entity is "Self-Guarding." It utilizes `__post_init__` to trigger immediate validation, making it physically impossible for an invalid `TaxiTrip` to exist in memory.

### Cross-Object Invariants:

1. **Velocity Guard (`_check_physical_velocity`):** - **Action:** Detects impossible transit speeds.
   - **Rationale:** NYC physical limits (125 mph) filter out GPS anomalies or fraudulent data.
1. **Financial Guard (`_check_financial_integrity`):** - **Action:** Audits the sum of all charges.
   - **Rationale:** Ensures accounting consistency within a 0.01 tolerance threshold.

______________________________________________________________________

*"One Entity. Total Integrity. Built for the Future of NYC Transit."*
