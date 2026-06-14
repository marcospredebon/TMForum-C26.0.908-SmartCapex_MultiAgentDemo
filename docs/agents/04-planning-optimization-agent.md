# Sub-Agent 3 — Planning/Optimization Agent

## Role

Processes one or more TM Forum intent documents (RDF Turtle, ICM / TIO v3.6.0) and returns a structured JSON investment recommendation with ranked intentions, conflicts, gaps, and optimization focus areas.

## Platform

Microsoft Copilot Studio — **Sub-Agent** (called by SmartCapex main agent)

## Position in Pipeline

```
SmartCapex (via "Generate Investment Recommendation" action) → [Planning/Optimization Agent] → Recommendation JSON
```

## Input Contract

```json
{
  "sourceAgent": "SmartCapex Orchestrator",
  "receivedAt": "<ISO-8601 timestamp>",
  "requestId": "<string>",
  "intentDocuments": ["<RDF Turtle string>"]
}
```

## Output Contract (summary)

```json
{
  "requestId": "string",
  "status": "ok | error",
  "summary": {
    "totalIntents": 0,
    "totalExpectations": 0,
    "systemIntentions": [
      {
        "category": "connectivity | capacity | optimization | assurance | planning | mixed",
        "statement": "string",
        "priority": "high | medium | low",
        "targets": ["string"],
        "objectives": [{ "property": "string", "direction": "minimize | maximize | satisfy", "value": "string" }],
        "constraints": [{ "property": "string", "operator": "string", "value": "string", "unit": "string" }],
        "timeContext": { "start": "string", "end": "string", "recurrence": "string" },
        "assumptions": ["string"]
      }
    ],
    "conflicts": [{ "type": "string", "description": "string", "affectedIntentIds": ["string"], "severity": "string" }],
    "gaps": [{ "type": "string", "description": "string", "affectedIntentIds": ["string"], "recommendedAction": "string" }],
    "optimizationFocus": ["string"],
    "guaranteesRequired": ["string"]
  }
}
```

## Prioritization Order

1. Demand and capacity feasibility
2. Cost optimization objectives
3. Quality and SLA constraints
4. Time and rollout constraints

## Knowledge Base Reference

KB file for this agent:

- [`kb-planning-optimization-intent-agent.txt`](kb-planning-optimization-intent-agent.txt)

## Demo Instructions (used in this demo)

→ **[`copilot-studio/instructions/demo-planning-optimization.txt`](../../copilot-studio/instructions/demo-planning-optimization.txt)**

This is the exact instruction file deployed in the SmartCapex demo. Paste its contents into the agent's **Instructions** field in Copilot Studio.

For an annotated reference version with additional context, see [`copilot-studio/instructions/planning-optimization.md`](../../copilot-studio/instructions/planning-optimization.md).

## Copilot Studio Setup

See → [`copilot-studio/SETUP.md`](../../copilot-studio/SETUP.md) — Step 3.
