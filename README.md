# MnV_context_graph

Test of concept

```mermaid
graph TD

%% === Outcome ===
Impact["Reported Impact (kWh, therms, $)"]

%% === Counterfactual core ===
Baseline["Baseline Period Definition"]
Reporting["Reporting Period Definition"]
Boundary["Measurement Boundary"]
Model["Reporting Model Spec (statistical/physical)"]
Adj["Adjustments (routine / non-routine)"]
Vars["Independent Variables (weather, production, occupancy)"]

%% === Data & evidence ===
Meters["Meter Data"]
BAS["BAS/EMS Trends"]
Invoices["Utility Bills"]
Weather["Weather Data (station + method)"]
QAQC["Data QA/QC Rules"]
Provenance["Data Provenance + Lineage"]
Docs["Evidence: M&V Plan, As-builts, O&M logs"]

%% === Uncertainty & validation ===
Unc["Uncertainty Method (CI, Bayesian, etc.)"]
Valid["Model Validation (CVRMSE, NMBE, residual tests)"]
Sens["Sensitivity / Scenario Checks"]

%% === Governance ===
Stake["Stakeholders (Owner, ESCO, Evaluator, Utility, Regulator)"]
Protocol["Protocol / Ruleset (IPMVP option + local requirements)"]
Roles["Roles & Responsibilities"]
Signoff["Review + Sign-off"]
Dispute["Dispute / Change Control"]

%% === Relationships ===
Impact --> Model
Impact --> Adj
Impact --> Boundary
Model --> Baseline
Model --> Reporting
Model --> Vars
Model --> Valid
Model --> Unc
Valid --> Sens

Baseline --> Meters
Reporting --> Meters
Vars --> Weather
Vars --> BAS

Meters --> QAQC
BAS --> QAQC
Invoices --> QAQC
Weather --> QAQC

QAQC --> Provenance
Provenance --> Docs

Protocol --> Model
Protocol --> Adj
Protocol --> Unc
Stake --> Roles
Roles --> Signoff
Signoff --> Impact
Dispute --> Adj
Dispute --> Model
Docs --> Signoff
```

## How to read this graph

- Boxes represent entities that contribute to the meaning of reported impact.
- Arrows represent dependency or constraint relationships.
- Changing a node or relationship implies a change in interpretation, not just a recalculation.
- Governance nodes indicate where agreement, review, or dispute resolution applies.
