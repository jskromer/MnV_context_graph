# M&V Context Graph: Competent Counterfactual Framework

```mermaid
graph TD

%% === The Core Equation ===
Impact["Reported Impact<br/>(kWh, therms, $)"]
Actual["Actual Consumption<br/>(Reporting Period)"]
Counterfactual["Counterfactual<br/>(Adjusted Baseline)"]

%% === Counterfactual Construction ===
BaselineEvidence["Baseline Evidence<br/>(observed conditions + consumption)"]
Inference["Inference from Evidence"]
Model["Model / Ruleset<br/>(statistical or physical)"]

%% === Period Definitions ===
Baseline["Baseline Period Definition"]
Reporting["Reporting Period Definition"]
Boundary["Measurement Boundary"]

%% === Adjustments ===
RoutineAdj["Routine Adjustments<br/>(weather, production, occupancy)"]
NonRoutineAdj["Non-Routine Adjustments<br/>(conditions with no baseline analog)"]

%% === Independent Variables ===
Vars["Independent Variables"]
Weather["Weather Data<br/>(station + normalization method)"]
Production["Production / Occupancy"]

%% === Data Layer ===
Meters["Meter Data"]
BAS["BAS/EMS Trends"]
Invoices["Utility Bills"]
QAQC["Data QA/QC Rules"]

%% === Provenance Layer ===
DataProvenance["Data Provenance + Lineage"]
ParamProvenance["Parameter Provenance<br/>(calibration choices documented)"]
Docs["Evidence Package<br/>(M&V Plan, As-builts, O&M logs)"]

%% === Calibration & Validation ===
StatTests["Statistical Tests<br/>(CVRMSE, NMBE, residuals)"]
CalibProcess["Calibration Process<br/>(transparent, repeatable)"]
PhysicalPlausibility["Physical Plausibility Check"]

%% === Three Types of Uncertainty ===
EpistemicUnc["Epistemic Uncertainty<br/>(reducible with more data/analysis)"]
AleatoricUnc["Aleatoric Uncertainty<br/>(inherent variability, quantifiable)"]
OntologicalUnc["Ontological Uncertainty<br/>(no evidence exists — judgment required)"]

%% === Judgment Layer ===
Competence["Competent Counterfactual Assessment"]
Defensibility["Defensibility<br/>(Would a qualified reviewer agree?)"]
Sensitivity["Sensitivity Analysis<br/>(What assumptions matter most?)"]

%% === Governance ===
Stake["Stakeholders<br/>(Owner, ESCO, Evaluator, Utility, Regulator)"]
Protocol["Protocol / Ruleset<br/>(IPMVP option + local requirements)"]
Roles["Roles & Responsibilities"]
Signoff["Review + Sign-off"]
Dispute["Dispute / Change Control"]

%% ========== RELATIONSHIPS ==========

%% The fundamental equation
Impact --> Actual
Impact --> Counterfactual
Actual -. "minus" .-> Counterfactual

%% Actual measurement path
Actual --> Meters
Actual --> Reporting
Actual --> Boundary

%% Counterfactual construction (inference from evidence)
Counterfactual --> Inference
Inference --> BaselineEvidence
Inference --> Model
Counterfactual --> RoutineAdj
Counterfactual --> NonRoutineAdj

%% Baseline evidence
BaselineEvidence --> Baseline
BaselineEvidence --> Meters
BaselineEvidence --> Vars

%% Routine adjustments (within evidentiary basis)
RoutineAdj --> Model
RoutineAdj --> Vars
Vars --> Weather
Vars --> Production
RoutineAdj --> EpistemicUnc
RoutineAdj --> AleatoricUnc

%% Non-routine adjustments (beyond evidentiary basis)
NonRoutineAdj --> OntologicalUnc
OntologicalUnc --> Defensibility
OntologicalUnc --> Stake

%% Data sources
Meters --> QAQC
BAS --> QAQC
Invoices --> QAQC
Weather --> QAQC

%% Provenance chains
QAQC --> DataProvenance
CalibProcess --> ParamProvenance
DataProvenance --> Docs
ParamProvenance --> Docs

%% Calibration & validation
Model --> CalibProcess
CalibProcess --> StatTests
CalibProcess --> PhysicalPlausibility
StatTests -.-> Competence
PhysicalPlausibility -.-> Competence

%% Uncertainty quantification
EpistemicUnc --> Impact
AleatoricUnc --> Impact
OntologicalUnc -.-> Impact

%% Judgment layer
Competence --> Defensibility
Competence --> Sensitivity
Sensitivity --> EpistemicUnc

%% Governance
Protocol --> Model
Protocol --> RoutineAdj
Protocol --> NonRoutineAdj
Stake --> Roles
Roles --> Signoff
Signoff --> Impact
Dispute --> NonRoutineAdj
Docs --> Signoff
Docs --> Defensibility
```

## Key Concepts

### The Fundamental Equation
**Impact = Actual − Counterfactual**

The counterfactual (adjusted baseline) is *constructed through inference*, not measured.

### Inference from Evidence
The counterfactual is built from:
- **Baseline evidence**: Observed conditions and consumption during a defined period
- **Model/ruleset**: Systematic method for projecting that evidence into reporting period conditions

This is legitimate inference — we have evidence, we apply rules.

### Three Types of Uncertainty

| Type | Source | Character |
|------|--------|-----------|
| **Epistemic** | Incomplete analysis of available evidence | Reducible with effort |
| **Aleatoric** | Inherent system variability | Quantifiable, not reducible |
| **Ontological** | Conditions in reporting period have no baseline analog | No evidence exists — requires judgment |

### Where Ontological Uncertainty Lives
**Non-routine adjustments** are the boundary where inference from evidence ends.

When something occurs in the reporting period that was *not part of the baseline evidence* — new equipment, changed use, different occupancy patterns, a pandemic — we have no evidentiary basis for the counterfactual under those conditions.

This is not "harder to estimate." It is a fundamentally different epistemic status: we are making claims about a world-state for which *no direct evidence exists*.

### Why This Matters
- **Routine adjustments**: Governed by models and rules. Defensible through statistical tests and physical plausibility.
- **Non-routine adjustments**: Governed by *stakeholder agreement*. Defensibility requires transparency about the judgment being made.

This is where M&V disputes actually live — not in the statistics, but in the non-routines.

### Competent Counterfactual
A counterfactual is "competent" when:
1. Inference from evidence is sound (statistical + physical plausibility)
2. Ontological uncertainty is acknowledged and bounded
3. Stakeholders agree on the judgment calls
4. The whole chain is documented and defensible

## How to Read This Graph

- **Solid arrows** (→): Data flow or direct dependency
- **Dashed arrows** (⇢): Judgment, inference, or propagation of uncertainty
- **Ontological uncertainty** connects directly to stakeholders — because that's where agreement must be reached
