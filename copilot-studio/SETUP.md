# SmartCapex — Copilot Studio Setup Guide

This guide walks you through creating the four SmartCapex agents in Microsoft Copilot Studio. The three sub-agents must be **created and published first**, then the main SmartCapex agent connects them as sequential actions.

---

## Demo Instructions — Ready to Use

The three files below are the **exact agent instructions deployed in this demo**. Paste each one directly into the corresponding agent's **Instructions** field in Copilot Studio:

| File | Agent | Where to paste |
|---|---|---|
| [`instructions/demo-intent-decomposer.txt`](instructions/demo-intent-decomposer.txt) | User Intents Decomposer | Step 1.2 below |
| [`instructions/demo-bi-translator-rdf.txt`](instructions/demo-bi-translator-rdf.txt) | Intent Translator RDF Agent | Step 2 below |
| [`instructions/demo-planning-optimization.txt`](instructions/demo-planning-optimization.txt) | Planning/Optimization Agent | Step 3 below |

The `.md` files in this folder are extended reference versions with additional context and annotations.

---

## Prerequisites

- Access to [Microsoft Copilot Studio](https://copilotstudio.microsoft.com)
- Permission to create and publish agents in your environment
- (Optional) An Azure OpenAI connection configured in your Copilot Studio environment for custom model selection

---

## Overview — Creation Order

```
Step 1 → Create & publish:  User Intents Decomposer     (Sub-Agent 1)
Step 2 → Create & publish:  Intent Translator RDF Agent               (Sub-Agent 2)
Step 3 → Create & publish:  Planning/Optimization Agent (Sub-Agent 3)
Step 4 → Create & connect:  SmartCapex                  (Main Agent)
```

> Sub-agents **must be published** before the main agent can connect to them.

---

## Step 1 — Create Sub-Agent 1: User Intents Decomposer

### 1.1 Create the agent

1. Go to [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. Click **Create** → **New agent**
3. Fill in:
   - **Name:** `User Intents Decomposer`
   - **Description:** `Converts a natural-language network investment request into a structured JSON with Goal, Requirements, Assumptions, and Restrictions.`
4. Click **Create**

### 1.2 Configure Instructions

1. In the agent editor, click **Instructions** (or **Overview → Edit** in some versions)
2. Replace the default text with the full content of:
   **[`copilot-studio/instructions/demo-intent-decomposer.txt`](instructions/demo-intent-decomposer.txt)** ← actual demo instructions
3. Click **Save**

### 1.3 Configure the AI model

1. Go to **Settings** → **AI capabilities**
2. Under **Generative AI**, ensure it is **Enabled**
3. (Optional) Connect to Azure OpenAI if you want to use a specific model

### 1.4 Disable topics (optional but recommended)

Since this agent is called programmatically by the main agent, you may disable the default conversation topics:
1. Go to **Topics** → For each system topic, toggle **Enabled** off
2. Keep only the fallback or escalation topics if needed

### 1.5 Publish

1. Click **Publish** (top right)
2. Confirm the publication
3. Note the agent's **Connection ID** — you will need it when connecting it to the main agent

---

## Step 2 — Create Sub-Agent 2: Intent Translator RDF Agent

Repeat the same steps as Step 1 with:
- **Name:** `Intent Translator RDF Agent`
- **Description:** `Translates a structured business intent JSON into RDF Turtle format aligned with TM Forum TMF921 and the Intent Common Model (ICM / TIO v3.6.0).`
- **Instructions:** paste the full content of **[`copilot-studio/instructions/demo-bi-translator-rdf.txt`](instructions/demo-bi-translator-rdf.txt)** ← actual demo instructions

Publish when done.

---

## Step 3 — Create Sub-Agent 3: Planning/Optimization Agent

Repeat with:
- **Name:** `Planning Optimization Agent`
- **Description:** `Processes TM Forum RDF intent documents and returns a structured investment recommendation with ranked intentions, conflicts, gaps, and optimization focus areas.`
- **Instructions:** paste the full content of **[`copilot-studio/instructions/demo-planning-optimization.txt`](instructions/demo-planning-optimization.txt)** ← actual demo instructions

Publish when done.

---

## Step 4 — Create the Main Agent: SmartCapex

### 4.1 Create the agent

1. Click **Create** → **New agent**
2. Fill in:
   - **Name:** `SmartCapex`
   - **Description:** `AI-powered network CapEx planning assistant. Orchestrates three specialized agents to convert natural-language investment goals into ranked, standards-based network investment recommendations aligned with TM Forum TMF921.`
3. Click **Create**

### 4.2 Configure Instructions

1. Go to **Instructions**
2. Paste the full content of **`copilot-studio/instructions/smartcapex-main.md`**
3. Click **Save**

### 4.3 Add Agent Actions — Connect the three sub-agents

This is the key step. You will add each sub-agent as an **action** that SmartCapex can call.

#### Add Sub-Agent 1 as an action

1. In the SmartCapex agent editor, go to **Actions** → **Add an action**
2. Select the **Agents** tab (or search for agent actions)
3. Find and select **User Intents Decomposer**
4. Configure:
   - **Action name:** `Decompose User Intent`
   - **Action description:** `Receives the user's natural-language investment request and returns a structured JSON with Goal, Requirements, Assumptions, and Restrictions.`
   - **Input:** Map the user's message as the input to this agent
   - **Output:** The structured JSON (Goal, Requirements, Assumptions, Restrictions)
5. Click **Save action**

#### Add Sub-Agent 2 as an action

1. **Actions** → **Add an action** → **Agents** tab
2. Select **Intent Translator RDF Agent**
3. Configure:
   - **Action name:** `Translate Intent to RDF`
   - **Action description:** `Receives the structured intent JSON and returns RDF Turtle aligned with TM Forum TMF921 and the Intent Common Model.`
   - **Input:** The JSON output from the Decompose User Intent action
   - **Output:** RDF Turtle string
4. Click **Save action**

#### Add Sub-Agent 3 as an action

1. **Actions** → **Add an action** → **Agents** tab
2. Select **Planning Optimization Agent**
3. Configure:
   - **Action name:** `Generate Investment Recommendation`
   - **Action description:** `Receives the RDF intent document and returns a structured investment recommendation with ranked intentions, conflicts, gaps, and guarantees.`
   - **Input:** The RDF Turtle from the previous step, plus requestId and timestamp
   - **Output:** Structured JSON recommendation
4. Click **Save action**

### 4.4 Verify the action sequence in Instructions

In the SmartCapex agent's **Instructions**, confirm that the orchestration sequence references the three action names exactly as you named them in 4.3:
- `Decompose User Intent`
- `Translate Intent to RDF`
- `Generate Investment Recommendation`

If you used different names, update the instructions accordingly.

### 4.5 Publish SmartCapex

1. Click **Publish**
2. Choose the publication channel:
   - **Microsoft Teams** — for internal use
   - **Copilot Studio Demo Website** — for quick testing
   - **Custom website / embed code** — for integration into portals
3. Confirm publication

---

## Step 5 — Test the End-to-End Pipeline

1. Open the agent's **Test** panel (or the published channel)
2. Paste the content of `examples/sample-intent-request.txt` as your first message
3. Verify the agent:
   - Calls Sub-Agent 1 and receives a JSON
   - Passes the JSON to Sub-Agent 2 and receives RDF Turtle
   - Passes the RDF to Sub-Agent 3 and receives an investment recommendation
   - Presents the final recommendation in plain language

### Expected behavior

```
You:        "Based on a $2M budget and 3-year demand forecast, generate a
             transport deployment plan for the metropolitan region..."

SmartCapex: [internally calls 3 sub-agents in sequence]

SmartCapex: "Here is your SmartCapex investment recommendation:

             Priority 1 (High): Optimize transport investments...
             ...
             Conflicts detected: None
             Gaps identified: None
             Optimization focus: Minimize capital investment while...
             Guarantees required: Availability ≥ 99.95%..."
```

---

## Troubleshooting

| Issue | Cause | Fix |
|---|---|---|
| Sub-agent not appearing in Actions | Agent not yet published | Publish the sub-agent first |
| Main agent does not call sub-agents | Action names mismatch in Instructions | Ensure action names in instructions match exactly the action names you configured |
| Sub-agent returns empty output | Input not mapped correctly | Check the input mapping in the action configuration — ensure the previous step's output is passed |
| RDF Turtle is malformed | Intent Translator RDF Agent instructions truncated | Verify the full instructions were pasted, including all prefix declarations |
| Planning agent returns error status | Missing fields in input payload | Check that `sourceAgent`, `receivedAt`, `requestId`, and `intentDocuments` are all included in the action input |

---

## Environment Variables & Secrets

Copilot Studio manages credentials through **environment variables** and **connections** within your Power Platform environment — not through `.env` files.

To configure an Azure OpenAI connection:
1. Go to **Settings** → **AI capabilities** → **Azure OpenAI Service**
2. Add your Azure OpenAI endpoint and key as a **connection** (stored securely in Power Platform)
3. Reference the connection in each agent's AI model settings

Never hard-code API keys or connection strings in agent instructions or action configurations.
