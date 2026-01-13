# 🏛️ Platform Vision: The Multi-Model Sovereign Engine

## 1. Executive Summary

This platform is engineered as a **Unified Inference Hub**. It transcends traditional ML scripts by treating models as "Swappable Industrial Gears" attached to a high-performance, validated data stream (The Sovereign Core).

## 2. Core Objective: Vertical & Horizontal Scaling

- **Phase I (Foundational):** Deployment of the `Duration` prediction engine utilizing the `TaxiTrip` Aggregate Root.
- **Phase II (Structural):** Integration of `Tip Amount` and `Demand Forecasting` models without modifying the Domain Sanctuary.
- **Phase III (Industrial):** Real-time streaming inference using the same unified validation logic, powered by the Polars Lazy API.

## 3. Design Principles (The DNA)

- **Entity Sovereignty:** The `TaxiTrip` entity is the **Single Source of Truth**. All models ingest from its validated state and write back to its internal `predictions` registry.
- **Logic Agnosticism:** The core remains indifferent to the ML library (XGBoost, CatBoost, etc.). If a tool respects the `InferencePort`, it is compatible.
- **SDDL Mandate:** All platform operations are documented via **Action/Logic/Rationale** to ensure zero technical debt and total transparency.

## 4. The "Predictions Registry" Architecture

Every prediction task is registered within the `TaxiTrip` entity. The platform orchestrates the following sequence:

1. **Sovereign Ingestion:** Data fetching via Polars (Zero-Copy/Lazy).
1. **Atomic Defense:** Instant validation through `__post_init__` (No corrupted data enters the engine).
1. **Registry Injection:** Models execute and store their results in the `predictions: dict[str, float]` field.
1. **Unified Aggregation:** A single, enriched entity returns all inferences, ensuring total data consistency.

## 5. Industrial Rationale

- **Why Polars?** To handle millions of rows with sub-second latency while maintaining zero-dependency in the core.
- **Why the Registry?** To allow multiple AI models to "collaborate" on a single trip object without creating messy, disparate data structures.

______________________________________________________________________

*"One Entity. Multiple Intelligences. Absolute Sovereignty."*
