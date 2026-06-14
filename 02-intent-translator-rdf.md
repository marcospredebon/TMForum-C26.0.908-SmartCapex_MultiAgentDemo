# Sub-Agent 2 — Intent Translator RDF Agent

## Role

Converts the structured business intent JSON (from the User Intents Decomposer) into one or more **RDF Turtle** business intents aligned with **TMF921** and the **TM Forum Intent Common Model (ICM / TIO v3.6.0)**.

## Platform

Microsoft Copilot Studio — **Sub-Agent** (called by SmartCapex main agent)

## Position in Pipeline

```
SmartCapex (via "Translate Intent to RDF" action) → [Intent Translator RDF Agent] → Planning/Optimization Agent
```

## Output Contract

Returns **RDF Turtle only** — no JSON, no markdown, no prose. Uses these prefixes:

```turtle
@prefix ex:   <http://example.com/ns#> .
@prefix icm:  <https://www.tmforum.org/2020/07/intent-model#> .
@prefix insp: <https://www.tmforum.org/2020/07/intent-model/intent-specific-properties#> .
@prefix dct:  <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
```

## Expectation Types

| Type | When used |
|---|---|
| `ex:DeliveryExpectation` | Deploy, establish, connect, provide |
| `ex:PropertyExpectation` | Constrain cost, quality, capacity, latency |
| `ex:ConstraintExpectation` | Hard guardrails, budget caps, business rules |
| `ex:ContextExpectation` | Planning premises, time horizons, growth assumptions |

> **Format note:** Serialization is **RDF** (Resource Description Framework) Turtle. All references use "RDF" — correct and intentional throughout SmartCapex.

## Knowledge Base Reference

KB file for this agent:

- [`docs/agents/kb-Intent-Translator-RDF-Agent.txt.txt`](docs/agents/kb-Intent-Translator-RDF-Agent.txt.txt)

## Demo Instructions (used in this demo)

→ **[`copilot-studio/instructions/demo-bi-translator-rdf.txt`](../../copilot-studio/instructions/demo-bi-translator-rdf.txt)**

This is the exact instruction file deployed in the SmartCapex demo. Paste its contents into the agent's **Instructions** field in Copilot Studio.

For an annotated reference version with additional context, see [`copilot-studio/instructions/intent-translator-rdf.md`](../../copilot-studio/instructions/intent-translator-rdf.md).

## Copilot Studio Setup

See → [`copilot-studio/SETUP.md`](../../copilot-studio/SETUP.md) — Step 2.
