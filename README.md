# SmartCapex Multi-Agent Demo (TM Forum C26.0.908)

SmartCapex is a multi-agent AI pipeline for intelligent network CapEx planning aligned to TM Forum standards, including TMF921 Intent Management and the Intent Common Model (ICM/TIO v3.6.0).

## Architecture

The solution is orchestrated in **n8n** and uses four agents in sequence:

1. **User Intents Decomposer**
   - Input: natural-language CapEx request.
   - Output: structured JSON with `goal`, `requirements`, `assumptions`, and `restrictions`.

2. **BI Translator**
   - Input: decomposed JSON intent.
   - Output: RDF Turtle document aligned with TM Forum Intent Common Model (ICM/TIO v3.6.0) for TMF921-compatible processing.

3. **BI Orchestrator**
   - Input: RDF intent document.
   - Action: routes the intent to relevant specialist planning and optimization capabilities.

4. **Planning/Optimization Agent**
   - Input: TM Forum intent documents.
   - Output: ranked investment recommendations (e.g., expected impact, cost, and priority rationale).

## Repository Contents

- `workflows/smartcapex-n8n-template.json` — n8n workflow template with placeholder credentials and LLM model names.
- `intents/sample-intent.ttl` — sample TMF921-aligned RDF intent document (Turtle).
- `.env.example` — environment variable template for LLM/API credentials.
- `docs/agent-prompts/` — prompt description files for each SmartCapex agent.

## Quick Start

1. Copy `.env.example` to `.env` and fill in your credentials.
2. Import `workflows/smartcapex-n8n-template.json` into n8n.
3. Use `intents/sample-intent.ttl` as a starting intent payload for integration tests.
4. Tailor the prompts in `docs/agent-prompts/` to your deployment constraints.
