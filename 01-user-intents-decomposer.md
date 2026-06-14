# Agent 1 — User Intents Decomposer

## Role

Receives a free-text network investment request and produces a structured JSON object that captures the user's main intent plus all explicit requirements, assumptions, and restrictions.

## Position in Pipeline

```
User (natural language) → [User Intents Decomposer] → BI Translator
```

## Output Contract

Returns exactly one JSON object with four mandatory arrays:

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
| `Requirements` | Requested outcomes, operational priorities, mandatory business needs |
| `Assumptions` | Planning premises, forecast horizons, contextual starting points |
| `Restrictions` | Hard limits, budget caps, exclusions, hard constraints |

## Knowledge Base Reference

KB file for this agent:

- [`docs/agents/kb-intent-decomposer-agent.txt`](docs/agents/kb-intent-decomposer-agent.txt)

## Behavioral Rules

- Interpret paraphrases and semantically equivalent wording as the same intent
- Do **not** invent facts not present in the request
- Preserve important numeric values, time horizons, budget caps, and prioritization logic
- Merge duplicate ideas into a single concise item
- Use empty arrays when a category is not present in the request
- If a request asks for **assessment** rather than plan generation, reflect that in `Goal`

## Output Requirements

- Valid JSON only
- No markdown, no prose before or after the JSON
- All four fields must always be arrays of strings

## Example

### Input
```
Based on $500k budget and 2 years of projected future demand, generate a network
deployment plan that ensures optimal service levels, prioritizing both the most
saturated existing sites and areas where demand has been detected but no site
currently exists.
```

### Output
```json
{
  "Goal": [
    "Generate a network deployment plan",
    "Ensure optimal service levels"
  ],
  "Requirements": [
    "Prioritize the most saturated existing sites",
    "Prioritize areas with detected demand and no existing site"
  ],
  "Assumptions": [
    "Use a 2-year projected demand horizon"
  ],
  "Restrictions": [
    "Budget limited to $500k"
  ]
}
```
