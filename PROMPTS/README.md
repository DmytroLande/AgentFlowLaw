# AgentFlowLaw Prompts

This directory contains an example demonstrating how **AgentFlowLaw transforms a simple legal-analysis request into a structured multi-agent procedure**.

## Primary Prompt

The initial task is formulated by a human expert in natural language:

> **Implement automated detection of risks, contradictions, and corruption threats in the text of a draft law.**

The complete primary prompt is available here:

**[PrimaryPrompt](PrimaryPrompt)**

The Primary Prompt describes **what has to be analyzed**, but does not specify the internal analytical procedure, agent roles, verification mechanisms, or interaction logic.

---

## From Primary Prompt to Agentic Prompt

AgentFlowLaw acts as a **meta-prompt**.

It interprets the Primary Prompt, identifies the required legal-analysis operations, decomposes the task, creates specialized agents, defines their interactions, introduces verification procedures, and specifies the structure of the final output.

The transformation can be represented as:

```text
┌──────────────────────┐
│    PRIMARY PROMPT    │
│                      │
│  Legal analysis task │
│  formulated by a     │
│  human expert        │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     AgentFlowLaw     │
│                      │
│     Meta-Prompt      │
│                      │
│  Task decomposition │
│  Agent generation   │
│  Workflow design    │
│  Verification       │
│  Human control      │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    AGENTIC PROMPT    │
│                      │
│ Structured no-code  │
│ multi-agent legal   │
│ analysis procedure  │
└──────────────────────┘
In compact form:

Primary Prompt → AgentFlowLaw → Agentic Prompt

AgentFlowLaw therefore does not merely expand the original prompt. It programs the analytical procedure required to solve the legal task.

Agentic Prompt

The generated Agentic Prompt defines a structured multi-agent procedure for performing the requested legal analysis.

It specifies:

specialized legal agents;
their roles and goals;
input and output for each agent;
sequential and parallel analytical operations;
information transfer between agents;
legal-source verification;
detection of risks, contradictions, ambiguities, gaps, and corruption-risk indicators;
verification and traceability procedures;
synthesis of results;
human-control points.

The complete generated prompt is available here:

**[AgenticPrompt](AgenticPrompt)**

Transformation Principle

The example illustrates the central principle of AgentFlowLaw:
Legal Task
    ↓
Primary Prompt
    ↓
AgentFlowLaw
    ↓
Generated Agentic Prompt
    ↓
Multi-Agent Analysis
    ↓
Verification
    ↓
Structured Result
    ↓
Human Expert

AgentFlowLaw does not primarily program an answer to a legal question; it programs the procedure for obtaining, checking, tracing, and presenting that answer.
---------------------------------------------------------------------------------------------------------
| File                                  | Description                                                   |
| ------------------------------------- | ------------------------------------------------------------- |
| **[PrimaryPrompt](PrimaryPrompt)**    | Initial legal-analysis task formulated in natural language    |
| **[AgenticPrompt](AgenticPrompt)**    | Multi-agent analytical procedure generated using AgentFlowLaw |
---------------------------------------------------------------------------------------------------------
