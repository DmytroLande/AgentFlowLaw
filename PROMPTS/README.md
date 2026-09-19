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
