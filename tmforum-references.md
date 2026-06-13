# TM Forum Standards Reference

SmartCapex is aligned with the following TM Forum standards. All assets are referenced from the official TM Forum Open API and IG/GB document library.

## Intent Management

| Document | Title | Version | Role |
|---|---|---|---|
| TMF921 | Intent Management API Specification | v5.0.0 | Core intent lifecycle management |
| TR292A | Intent Management Elements | v3.6.0 | Intent element definitions and relationships |
| TR292B | Intent Management State Machines | v3.7.0 | Intent lifecycle state transitions |
| TR292C | Function Definition Ontology | v3.6.0 | Functional ontology for intent modeling |
| TR292D | Quantity Ontology | v3.6.0 | Measurement and unit definitions |
| TR290V | Intent Common Model Vocabulary Reference | v3.6.0 | Shared vocabulary across intent specs |

## Intent Common Model (ICM / TIO)

The **Intent Common Model** (TIO v3.6.0) is the RDF ontology used throughout SmartCapex to represent business intents in a machine-readable, standards-compliant format.

**RDF prefixes:**
```turtle
@prefix icm:  <https://www.tmforum.org/2020/07/intent-model#> .
@prefix insp: <https://www.tmforum.org/2020/07/intent-model/intent-specific-properties#> .
```

> **Format note:** SmartCapex uses **RDF** (Resource Description Framework) serialized as Turtle (`.ttl`). All references in code and documentation to the intent serialization format use "RDF" — this is correct and intentional.

## Information Framework

| Document | Title | Version | Role |
|---|---|---|---|
| GB922 | Information Framework (SID) — Resource domain | v25.5 | Network resource data model alignment |
| GB922 | Information Framework (SID) — Business Partner domain | v25.5 | Partner and stakeholder model |
| GB922F | Information Framework Excel | v25.5 | Full SID entity reference |

## Functional Framework (eTOM)

| Document | Title | Version | Role |
|---|---|---|---|
| GB1033 | Functional Framework (eTOM) | v25.5 | Business process model alignment |
| GB1033F | Functional Framework Excel | v25.5 | Full eTOM process reference |

## Autonomous Networks & ODA

| Document | Title | Role |
|---|---|---|
| ODA | Open Digital Architecture | Component mapping — 20 ODA components applied |
| AN Principles | Autonomous Network Principles | ANL framework and maturity model |

## Where to Obtain These Documents

All TM Forum specifications are available to TM Forum members via the [TM Forum Confluence](https://www.tmforum.org/resources/) and the TM Forum Open API Table. Non-members can access selected public documents at the TM Forum website.
