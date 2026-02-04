# M&V Context Graph: Competent Counterfactual Framework

```mermaid
graph TD

%% === The Core Equation ===
Impact["Reported Impact (kWh, therms, $)"]
Actual["Actual Consumption<br/>(Reporting Period)"]
Counterfactual["Counterfactual Projection<br/>(What Would Have Happened)"]

%% === Dual Digital Twin ===
ActualModel["Actual Measurement Path"]
CFModel["Counterfactual Model<br/>(Statistical or Physical)"]

%% === Period Definitions ===
Baseline["Baseline Period Definition"]
Reporting["Reporting Period Definition"]
Boundary["Measurement Boundary"]

%% === Adjustments ===
RoutineAdj["Routine Adjustments<br/>(weather, production, occupancy)"]
NonRoutineAdj["Non-Routine Adjustments<br/>(equipment changes, use changes)"]

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
ParamProvenance["Parameter Provenance<br/>(every calibration choice documented)"]
Docs["Evidence Package<br/>(M&V Plan, As-builts, O&M logs)"]

%% === Calibration & Validation ===
StatTests["Statistical Tests<br/>(CVRMSE, NMBE, residuals)"]
CalibProcess["Calibration Process<br/>(transparent, repeatable)"]
PhysicalPlausibility["Physical Plausibility Check"]

%% === Uncertainty (Two Types) ===
EpistemicUnc["Epistemic Uncertainty<br/>(what we don't know but could)"]
AleatoricUnc["Aleatoric Uncertainty<br/>(inherent variability)"]
UncQuantification["Uncertainty Quantification<br/>(CI, Bayesian, bootstrap)"]

%% === Judgment Layer (The 'Competent' in Competent Counterfactual) ===
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

%% Dual paths
Actual --> ActualModel
Counterfactual --> CFModel

%% Actual measurement path
ActualModel --> Meters
ActualModel --> Reporting
ActualModel --> Boundary

%% Counterfactual model construction
CFModel --> Baseline
CFModel --> Vars
CFModel --> RoutineAdj
CFModel --> NonRoutineAdj
CFModel --> CalibProcess

%% Variables feed model
Vars --> Weather
Vars --> Production
Weather --> RoutineAdj
Production --> RoutineAdj

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
CalibProcess --> StatTests
CalibProcess --> PhysicalPlausibility
StatTests -.-> Competence
PhysicalPlausibility -.-> Competence

%% Uncertainty flows
CFModel --> EpistemicUnc
CFModel --> AleatoricUnc
EpistemicUnc --> UncQuantification
AleatoricUnc --> UncQuantification
UncQuantification --> Impact

%% Judgment layer (the key insight)
Competence --> Defensibility
Competence --> Sensitivity
Sensitivity --> EpistemicUnc
Defensibility --> Signoff

%% Governance
Protocol --> CFModel
Protocol --> RoutineAdj
Protocol --> NonRoutineAdj
Protocol --> UncQuantification
Stake --> Roles
Roles --> Signoff
Signoff --> Impact
Dispute --> NonRoutineAdj
Dispute --> CFModel
Docs --> Signoff
Docs --> Defensibility
```

## Key Concepts in This Graph

### The Fundamental Equation
**Impact = Actual − Counterfactual**

This makes explicit what traditional M&V often obscures: we're not just comparing two measurements. We're comparing what *happened* against what *would have happened* — a fundamentally different epistemic claim.

### Dual Digital Twin
The graph shows two parallel paths:
- **Actual Measurement Path**: What the meters recorded during the reporting period
- **Counterfactual Model**: Our best estimate of consumption *absent the intervention*

### Competent Counterfactual (The Judgment Layer)
Statistical tests (CVRMSE, NMBE) are *necessary but not sufficient*. A competent counterfactual also requires:
- **Physical plausibility**: Does the model behave like a real building?
- **Defensibility**: Would a qualified, skeptical reviewer find this credible?
- **Sensitivity analysis**: Which assumptions drive the result?

Passing thresholds is checkbox compliance. Building confidence is the real goal.

### Two Types of Uncertainty
- **Epistemic**: Uncertainty from incomplete knowledge (reducible with more data/analysis)
- **Aleatoric**: Inherent randomness in the system (irreducible)

Conflating these leads to false confidence or unnecessary conservatism.

### Parameter Provenance
Every calibration choice should be documented: what was changed, why, what alternatives were considered. This isn't just audit trail — it's how we build (and communicate) confidence.

### Governance as First-Class Concern
M&V results are social agreements as much as technical calculations. The graph acknowledges that stakeholder alignment, dispute resolution, and sign-off are integral to the meaning of "reported impact."

## How to Read This Graph

- **Solid arrows** (→): Direct dependency or data flow
- **Dashed arrows** (⇢): Inferential or judgment relationship
- Nodes are color-grouped conceptually (rendering depends on viewer)
- The "Competence" node is the bridge between technical validity and stakeholder acceptance
