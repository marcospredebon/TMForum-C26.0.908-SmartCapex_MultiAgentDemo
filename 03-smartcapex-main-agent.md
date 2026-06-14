# SmartCapex — Main Orchestrator Agent

## Role

The main entry point of the SmartCapex system. Users interact exclusively with this agent. It receives natural-language network investment requests and **always calls the three sub-agents in fixed sequence**, passing the output of each step as the input to the next.

## Platform

Microsoft Copilot Studio — **Orchestrator Agent** (multi-agent mode)

## Position in Pipeline

```
User → [SmartCapex] → User Intents Decomposer
                    → Intent Translator RDF Agent
                    → Planning/Optimization Agent
                    → Response to User
```

## Agent Actions (Connected Sub-Agents)

| Action Name | Calls | Input | Output |
|---|---|---|---|
| `Decompose User Intent` | User Intents Decomposer | User's message verbatim | JSON: Goal, Requirements, Assumptions, Restrictions |
| `Translate Intent to RDF` | Intent Translator RDF Agent | JSON from step 1 | RDF Turtle (TMF921/ICM) |
| `Generate Investment Recommendation` | Planning/Optimization Agent | RDF Turtle + metadata payload | JSON: ranked intentions, conflicts, gaps, guarantees |

## Execution Sequence

The agent ALWAYS follows this sequence — no steps are skipped, no order is changed:

```
1. Receive user message
2. Call "Decompose User Intent"    → receive structured JSON
3. Call "Translate Intent to RDF"  → receive RDF Turtle
4. Call "Generate Investment Recommendation" → receive recommendation JSON
5. Present recommendation to user in plain language
```

## Knowledge Base Reference

The main orchestrator uses sub-agents. Their KB files are:

- [`docs/agents/kb-intent-decomposer-agent.txt`](docs/agents/kb-intent-decomposer-agent.txt)
- [`docs/agents/kb-Intent-Translator-RDF-Agent.txt.txt`](docs/agents/kb-Intent-Translator-RDF-Agent.txt.txt)
- [`docs/agents/kb-planning-optimization-intent-agent.txt`](docs/agents/kb-planning-optimization-intent-agent.txt)

## Full Instructions

See → [`copilot-studio/instructions/smartcapex-main.md`](../../copilot-studio/instructions/smartcapex-main.md)

## Copilot Studio Setup

See → [`copilot-studio/SETUP.md`](../../copilot-studio/SETUP.md) — Step 4.
