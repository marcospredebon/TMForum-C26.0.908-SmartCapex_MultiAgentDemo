# Sub-Agent 1 — User Intents Decomposer

## Role

Receives a free-text network investment request and extracts a structured JSON with four mandatory fields.

## Platform

Microsoft Copilot Studio — **Sub-Agent** (called by SmartCapex main agent)

## Position in Pipeline

```
SmartCapex (via "Decompose User Intent" action) → [User Intents Decomposer] → Intent Translator RDF Agent
```

## Output Contract

Returns exactly one JSON object:

```json
{
  "Goal":         ["string"],
  "Requirements": ["string"],
  "Assumptions":  ["string"],
  "Restrictions": ["string"]
}
```

| Field | Semantic |
|---|---|
| `Goal` | Primary business objectives |
| `Requirements` | Requested outcomes and operational priorities |
| `Assumptions` | Planning premises and forecast horizons |
| `Restrictions` | Hard limits, budget caps, exclusions |

## Demo Instructions (used in this demo)

→ **[`copilot-studio/instructions/demo-intent-decomposer.txt`](../../copilot-studio/instructions/demo-intent-decomposer.txt)**

This is the exact instruction file deployed in the SmartCapex demo. Paste its contents into the agent's **Instructions** field in Copilot Studio.

For an annotated reference version with additional context, see [`copilot-studio/instructions/user-intents-decomposer.md`](../../copilot-studio/instructions/user-intents-decomposer.md).

## Copilot Studio Setup

See → [`copilot-studio/SETUP.md`](../../copilot-studio/SETUP.md) — Step 1.
