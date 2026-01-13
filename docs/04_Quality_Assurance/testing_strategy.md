# 🏛️ Testing Strategy: Property-Based Reliability (SOTA 2026)

## 1. The Sovereign Testing Hierarchy

Our goal is not "Coverage %" but **"Invariant Certainty"**. We ensure that the Domain Sanctuary remains impenetrable.

- **Unit Tests:** Verification of individual properties (e.g., `route_key` logic).
- **Property-Based Testing (PBT):** Utilizing **Hypothesis** to stress-test domain invariants against millions of random permutations.
- **Integration Tests:** End-to-end flow from Polars LazyFrames to ML Inference outputs.

## 2. High-Fidelity Data Factories (Factory-Boy)

We utilize **Factory-Boy** as our "Industrial Synthetic Engine" to generate high-fidelity domain objects.

- **Role:** Centralized creation of `TaxiTrip` objects, bypassing manual dictionary instantiation.
- **ML Ready:** The factory is pre-configured to populate the `predictions` registry with default baseline values.
- **Hypothesis Integration:** We use `strategies.builds(TaxiTripFactory)` to create a "Fuzzer" that explores every corner of our logic.

## 3. The 3-Zone Defensive Coverage

Using the **Hypothesis** engine, we systematically explore three data territories:

1. **The Sovereign Zone:** Valid, standard trips (Default behaviors).
1. **The Boundary Zone:** Extreme but legal values (e.g., exactly 124.9 mph or 1 cent fares).
1. **The Nullified Zone:** Illegal values (e.g., 125.1 mph) intended to trigger `ERR_DOM_VAL_XXX` and verify the **Atomic Defense**.

## 4. Static Guardrails & Quality CI

- **Linter (Ruff):** Mandatory sub-second code cleaning and PEP 8 enforcement.
- **Type Safety (Pyright):** Strict type checking to prevent "Type Pollution" in the multi-model pipeline.
- **SDDL Compliance:** Automated checks to ensure every method contains **Action/Logic/Rationale** in its docstring.

## 5. Industrial Rationale

- **Why PBT?** In NYC Taxi data, edge cases (like trips crossing midnight during a DST change) are common. Manual tests miss these; Hypothesis finds them.
- **Why 100% Core Coverage?** The `02_Domain_Core` is the brain. If the brain is flawed, the entire infrastructure is compromised.

______________________________________________________________________

*"We do not test to find bugs; we test to prove the sovereignty of our logic."*
