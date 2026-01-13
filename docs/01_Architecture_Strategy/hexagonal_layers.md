# 🏛️ Hexagonal Layers: The Sovereign Isolation Mandate

## 1. Architecture Philosophy (The Dependency Rule)

To build a world-class scalable platform, we enforce a strict **Inward Dependency Rule**. The Core is a "Sovereign Sanctuary"—it must never possess knowledge of databases, ML frameworks, or APIs. Logic flows inward; dependencies never point out.

## 2. The Three Sovereign Layers

### A. The Domain Core (The Sanctuary)

- **Role:** Host of business logic, Aggregate Roots (`TaxiTrip`), and Value Objects.
- **Rules:** - **Zero External Dependencies:** Strictly Standard Python only.
  - **Immutability:** Forced via `@dataclass(frozen=True, slots=True)`.
  - **Stability:** The most stable and protected layer of the ecosystem.

### B. The Application Layer (The Orchestrator)

- **Role:** Definition of **Ports** (Interfaces) and orchestration.
- **Components:** - `TripRepositoryPort`: Interface for data ingestion.
  - `InferencePort`: Interface for ML model execution.
- **Responsibility:** Directing the flow of data between adapters and the domain sanctuary.

### C. The Infrastructure Layer (The Laborers)

- **Role:** Implementation of **Adapters**.
- **Components:**
  - **Data Engine:** Polars-based Parquet scanners (Lazy API).
  - **ML Adapters:** Implementations for XGBoost/CatBoost.
  - **API Servicing:** Disposable layers for model serving.
- **Mandate:** This layer is "Disposable." Tools are swapped without compromising the Domain.

## 3. Communication Flow (The Atomic Protocol)

Data and signals traverse hexagonal boundaries via a strict sequence:

1. **Request Entry:** Raw data is ingested via an **Infrastructure Adapter** (e.g., Polars scanner).
1. **Domain Construction:** The Adapter attempts to instantiate a `TaxiTrip` entity using Sovereign Value Objects.
1. **The Atomic Guardrail:** Instantiation triggers the `__post_init__` sequence. No intermediaries like `validate()` are allowed.
1. **Signal Propagation:** - If logic is violated (e.g., Velocity > 125 mph), the Domain raises a `DomainValidationError`.
   - The **Application Layer** intercepts this signal to log "Dirty Data" or abort the pipeline.
1. **Registry Injection:** Valid entities are enriched via the `predictions` registry for ML traceability.

## 4. Execution & Error Standards

- **Sovereign Codes:** Any violation triggers a specific code (e.g., `ERR_DOM_VAL_001`).
- **Isolation:** Domain exceptions inherit from a base `DomainValidationError` in `exceptions.py`, ensuring complete decoupling from infrastructure runtime errors.
- **Documentation (SDDL):** Every method follows the **Action/Logic/Rationale** protocol to maintain institutional memory within the code.

______________________________________________________________________

*"Architected for the Future of Urban Transit. Designed to Outlast the Tools."*
