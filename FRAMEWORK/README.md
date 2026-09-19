# AgentFlowLaw

## A No-Code Framework for Programming Agentic Procedures for Legal Act Analysis

**Dmytro Lande, Leonard Strashnoy**  
**Version 1.0 · 2026**

> **AgentFlowLaw does not primarily program an answer to a legal question.  
> It programs the procedure for obtaining, checking, tracing, and presenting that answer.**

---

## 1. Purpose and Scope

**AgentFlowLaw (AFL)** is a domain-specific extension of the **AgentFlow** framework designed for no-code programming of agentic procedures for the analysis of legal acts and other legal and regulatory documents using Large Language Models (LLMs).

The framework is intended to be used primarily as a **meta-prompt**. It does not merely instruct an LLM to solve a legal task directly. Instead, it transforms a description of a legal analysis task into a structured no-code agentic procedure that can subsequently be executed by an LLM or an LLM-based system.

### General Processing Model

```text
Legal Task → AgentFlowLaw → Agentic Procedure → LLM → Analysis Result
```

AgentFlowLaw defines the structure and legal context of the task, specialized agents and their functions, sequential and parallel execution paths, inter-agent communication, legal-source verification, uncertainty handling, final output, and human-control points.

---

## 2. General Concept

AgentFlowLaw is **not a programming language in the traditional sense**. The program is represented as a structured natural-language description of an analytical procedure, while the LLM performs the functions of both execution environment and interpreter.

$$
P_{\mathrm{Law}} = F_{\mathrm{AFL}}(T,C,S,R,O)
$$

where $T$ is the legal analysis task, $C$ the legal context, $S$ the available sources, $R$ the requirements and constraints, and $O$ the required output.

```text
Prompt → Meta-Prompt → Agentic Procedure
```

---

## 3. Relationship to AgentFlow

AgentFlowLaw inherits the fundamental AgentFlow primitives:

```text
Condition
Loop
Function
Label
Goto
```

and the basic agent structure:

```text
ROLE
STATE
LOGIC
COMMUNICATION
```

It introduces:

```text
LEGAL_CONTEXT
LEGAL_SOURCE
JURISDICTION
VALIDITY
AUTHORITY
EVIDENCE
TRACEABILITY
UNCERTAINTY
VERIFICATION
HUMAN_CONTROL
```

Conceptually:

$$
\mathrm{AgentFlowLaw}
=
\mathrm{AgentFlow}
+
\mathrm{Legal\ Context}
+
\mathrm{Legal\ Sources}
+
\mathrm{Legal\ Verification}
+
\mathrm{Traceability}
+
\mathrm{Human\ Control}
$$

---

## 4. Input to AgentFlowLaw

### Minimal Input

```text
TASK:
    {{description_of_legal_task}}

INPUT:
    {{legal_document_or_documents}}
```

### Extended Input

```text
TASK:
    {{description_of_legal_task}}
INPUT:
    {{legal_document_or_documents}}
JURISDICTION:
    {{jurisdiction}}
ANALYSIS_DATE:
    {{date}}
AVAILABLE_SOURCES:
    {{sources}}
REQUIREMENTS:
    {{special_requirements}}
OUTPUT_REQUIREMENTS:
    {{required_output}}
```

If a parameter cannot be reliably derived, it must be represented as `UNKNOWN`. Missing information must not be silently replaced by assumptions.

---

## 5. Legal Context

```text
LEGAL_CONTEXT:
    JURISDICTION:
        {{country / legal system / institution}}
    ANALYSIS_DATE:
        {{date}}
    DOCUMENT_TYPE:
        {{law / draft_law / regulation / decision / contract / other}}
    LEGAL_DOMAIN:
        {{constitutional / administrative / criminal / civil / tax / other}}
    LEGAL_HIERARCHY:
        {{applicable hierarchy}}
    SOURCE_SCOPE:
        {{sources allowed for analysis}}
    TEMPORAL_SCOPE:
        {{relevant time interval}}
    HUMAN_DECISION_REQUIRED:
        TRUE
```

ContextLaw=Data+Jurisdiction+Time+Authority+Sources 

---

## 6. Legal Agent Model

The basic AgentFlow agent is:

$$
a=\langle R,S,L,C\rangle
$$

AgentFlowLaw extends it to:

$$
a_{\mathrm{Law}}=\langle R,S,L,C,J,A,E,V,T\rangle
$$

where $J$ is jurisdiction, $A$ normative authority, $E$ evidence, $V$ temporal validity, and $T$ traceability.

```text
TYPE:
    LEGAL_AGENT
ID:
    {{agent_ID}}
ROLE:
    {{legal_role}}
GOAL:
    {{goal}}
INPUT:
    {{required_input}}
LEGAL_CONTEXT:
    {{required_context}}
LOGIC:
    {{Condition / Loop / Function / Label / Goto}}
STATE:
    {{current_state}}
EVIDENCE_POLICY:
    {{rules_for_evidence}}
VERIFICATION:
    {{verification_rules}}
COMMUNICATION:
    RECEIVE_FROM: {{agents}}
    SEND_TO: {{agents}}
OUTPUT:
    {{structured_output}}
```

---

## 7. Basic Legal Operations

### Extraction

```text
EXTRACT_NORM()
EXTRACT_LEGAL_ENTITY()
EXTRACT_RIGHT()
EXTRACT_OBLIGATION()
EXTRACT_PROHIBITION()
EXTRACT_PERMISSION()
EXTRACT_EXCEPTION()
```

### Sources and Validity

```text
IDENTIFY_LEGAL_SOURCE()
RETRIEVE_NORM()
CHECK_SOURCE()
CHECK_VALIDITY()
CHECK_JURISDICTION()
CHECK_AUTHORITY()
```

### Comparison and Conflict Analysis

```text
COMPARE_NORMS()
DETECT_CONFLICT()
DETECT_AMBIGUITY()
DETECT_GAP()
DETECT_DUPLICATION()
```

### Reasoning and Verification

```text
BUILD_LEGAL_ARGUMENT()
VERIFY_ARGUMENT()
TRACE_CONCLUSION()
```

These are semantic functions interpreted and executed by an LLM and, where available, connected retrieval or legal-information systems.

---

## 8. Legal Sources

For every significant legal claim, AgentFlowLaw should establish whenever possible:

```text
Claim → Norm → Legal Source
```

```text
LEGAL_SOURCE:
    ID:
        {{source_ID}}
    TITLE:
        {{title}}
    TYPE:
        {{constitution / law / regulation / case / other}}
    JURISDICTION:
        {{jurisdiction}}
    AUTHORITY:
        {{authority_level}}
    VALID_FROM:
        {{date}}
    VALID_TO:
        {{date_or_NULL}}
    SOURCE:
        {{reference}}
```

```text
SOURCE_STATUS:
    VERIFIED
    UNVERIFIED
    CONFLICTING
    NOT_FOUND
```

If a source cannot be established or verified, the corresponding conclusion must not be presented as a fully established legal finding.

---

## 9. Temporal Validity

$$
\operatorname{Valid}(n,t)\in\{\mathrm{TRUE},\mathrm{FALSE},\mathrm{UNKNOWN}\}
$$

```text
IF VALIDITY == TRUE:
    USE_NORM()

IF VALIDITY == FALSE:
    EXCLUDE_FROM_CURRENT_LEGAL_BASIS()

IF VALIDITY == UNKNOWN:
    MARK_UNCERTAINTY()
    SEND_TO source_verifier
```

---

## 10. Normative Authority

$$
\operatorname{Authority}(s_i)>\operatorname{Authority}(s_j)
$$

The hierarchy is jurisdiction-specific:

```text
LEGAL_HIERARCHY:
    {{jurisdiction_specific_hierarchy}}
```

---

## 11. Analysis of Legal Conflicts

```text
IF possible_conflict(norm_A, norm_B):
    CALL conflict_detector
    CHECK:
        jurisdiction
        authority
        temporal_validity
        scope
        subject
        object
        conditions
        exceptions
    RETURN:
        conflict_status
        conflict_type
        evidence
        uncertainty
```

```text
CONFLICT_STATUS:
    CONFIRMED
    POSSIBLE
    NOT_CONFIRMED
    UNRESOLVED
```

A `POSSIBLE` or `UNRESOLVED` conflict must not automatically be converted into a definitive legal conclusion.

---

## 12. Uncertainty

```text
UNCERTAINTY:
    NONE
    LOW
    MEDIUM
    HIGH
    UNRESOLVED
```

```text
IF evidence_insufficient:
    DO_NOT_INVENT()
    MARK_UNRESOLVED()
```

Uncertainty is a legitimate analytical result and must be preserved in the final output.

---

## 13. Dynamic Formation of the Legal Agent Swarm

```text
FUNCTION BUILD_LEGAL_SWARM(TASK):
    ANALYZE TASK
    DECOMPOSE TASK
        INTO atomic_legal_tasks
    FOR EACH atomic_legal_task:
        DEFINE required_role
    MERGE duplicate_roles
    DEFINE dependencies
    DEFINE parallel_branches
    ADD verification_agents
    ADD moderator
    ADD human_control_point
RETURN LEGAL_SWARM
```

---

## 14. Typical Library of Legal Agents

```text
legal_loader
legal_context_controller
legal_entity_extractor
norm_extractor
norm_retriever
source_controller
validity_controller
norm_interpreter
conflict_detector
ambiguity_detector
gap_detector
legal_reasoner
evidence_verifier
traceability_controller
moderator
```

This list is not mandatory. AgentFlowLaw selects only the agents required by the task.

$$
\boxed{\text{one agent} \approx \text{one principal analytical function}}
$$

---

## 15. Parallel and Sequential Processing

```text
START_PARALLEL([
    conflict_detector,
    ambiguity_detector,
    gap_detector
])

WAIT_FOR_RESULTS()
MERGE_RESULTS()
```

Parallel execution describes logical independence and does not necessarily imply physical parallel execution. Results must not automatically be reconciled by averaging or majority voting.

---

## 16. Inter-Agent Communication

$$
M_{ij}:a_i\rightarrow a_j
$$

```text
MESSAGE:
    FROM:
        {{agent_ID}}
    TO:
        {{agent_ID}}
    CONTENT:
        {{result}}
    EVIDENCE:
        {{sources}}
    CONFIDENCE:
        {{assessment}}
    UNCERTAINTY:
        {{status}}
```

Agents transfer conclusions together with their evidence and uncertainty.

---

## 17. Legal Verification Loop

```text
Analysis → Source Verification → Validity Check → Conflict Check → Argument Verification
```

```text
LABEL: LEGAL_VERIFICATION

CHECK_SOURCES()
CHECK_JURISDICTION()
CHECK_VALIDITY()
CHECK_AUTHORITY()
CHECK_CONFLICTS()
CHECK_TRACEABILITY()

IF verification_failed
AND correction_possible:
    CORRECT_ANALYSIS()
    GOTO LEGAL_VERIFICATION

IF evidence_insufficient:
    MARK_UNRESOLVED()

IF verification_passed:
    SEND_TO moderator
```

The loop must include a termination condition or maximum number of iterations. `UNRESOLVED` is an acceptable final status.

---

## 18. Traceability of Legal Conclusions

```text
Conclusion → Argument → Norm → Source
```

```text
CONCLUSION:
    {{conclusion}}
ARGUMENT:
    {{reasoning}}
NORMS:
    {{norms}}
SOURCES:
    {{sources}}
TRACE:
    {{agents_and_operations}}
STATUS:
    {{verified / unresolved}}
```

---

## 19. Moderator

```text
COLLECT_RESULTS()
COMPARE_RESULTS()
IDENTIFY_CONTRADICTIONS()
PRESERVE_DISSENT()
CHECK_COMPLETENESS()
BUILD_FINAL_REPORT()
```

If two agents produce different but reasonably supported interpretations:

```text
DO_NOT_FORCE_CONSENSUS()
```

Both interpretations should be retained with their arguments, evidence, and uncertainty status.

---

## 20. Human Control

```text
Legal Documents → AgentFlowLaw → Legal Swarm → Verification → Recommendation → Human
```

```text
HUMAN_CONTROL:
    FINAL_DECISION:
        HUMAN
    SYSTEM_ROLE:
        ANALYSIS_AND_RECOMMENDATION
```

A human expert may `ACCEPT`, `REJECT`, `MODIFY`, `REQUEST_REANALYSIS`, or `REQUEST_ADDITIONAL_SOURCES`.

> **Human control is part of the architecture rather than an external disclaimer added after the analysis.**

---

## 21. Standard AgentFlowLaw Procedure

```text
TYPE:
    LEGAL_SWARM
NAME:
    {{procedure_name}}
PURPOSE:
    {{purpose}}
TASK:
    {{legal_task}}
LEGAL_CONTEXT:
    JURISDICTION:
        {{jurisdiction}}
    ANALYSIS_DATE:
        {{date}}
    DOCUMENT_TYPE:
        {{document_type}}
    LEGAL_DOMAIN:
        {{domain}}
    LEGAL_HIERARCHY:
        {{hierarchy}}
INPUT:
    {{input}}
AGENTS:
    {{agent_1}}
    {{agent_2}}
    ...
    {{agent_n}}
WORKFLOW:
    {{structured_AgentFlowLaw_logic}}
VERIFICATION:
    CHECK_SOURCES
    CHECK_JURISDICTION
    CHECK_VALIDITY
    CHECK_AUTHORITY
    CHECK_CONFLICTS
    CHECK_TRACEABILITY
HUMAN_CONTROL:
    FINAL_DECISION:
        HUMAN
OUTPUT:
    {{output_schema}}
```

---

## 22. Agent Generation Template

```text
TYPE:
    LEGAL_AGENT
ID:
    {{unique_ID}}
ROLE:
    {{single_clearly_defined_role}}
GOAL:
    {{goal}}
INPUT:
    {{input}}
LOGIC:
    {{structured_logic}}
STATE:
    {{state}}
COMMUNICATION:
    RECEIVE_FROM:
        {{agents}}
    SEND_TO:
        {{agents}}
EVIDENCE:
    {{required_evidence}}
OUTPUT:
    {{output}}
```

Agent responsibilities should be sufficiently narrow to make their operations interpretable and independently verifiable.

---

## 23. Mandatory AgentFlowLaw Rules

| Rule | Requirement |
|---|---|
| **1** | Never invent legal sources. |
| **2** | Separate source text from model interpretation. |
| **3** | Check jurisdiction. |
| **4** | Check temporal validity. |
| **5** | Consider normative authority. |
| **6** | Preserve uncertainty. |
| **7** | Preserve meaningful disagreements between agents. |
| **8** | Every significant legal conclusion should be traceable. |
| **9** | Verification must be separated from primary analysis. |
| **10** | The final legally significant decision belongs to a human. |

---

## 24. AgentFlowLaw Meta-Programming Algorithm

```text
FUNCTION AgentFlowLaw(TASK, INPUT):

    // STEP 1
    INTERPRET TASK

    // STEP 2
    IDENTIFY:
        object_of_analysis
        legal_questions
        jurisdiction
        temporal_scope
        required_sources
        expected_output

    // STEP 3
    BUILD LEGAL_CONTEXT

    // STEP 4
    DECOMPOSE TASK
        INTO atomic_legal_tasks

    // STEP 5
    CREATE specialized LEGAL_AGENTS

    // STEP 6
    DEFINE dependencies_between_agents

    // STEP 7
    IDENTIFY parallel_operations

    // STEP 8
    BUILD LEGAL_SWARM

    // STEP 9
    ADD source_verification

    // STEP 10
    ADD LEGAL_VERIFICATION_LOOP

    // STEP 11
    ADD moderator

    // STEP 12
    ADD human_control

    // STEP 13
    DEFINE structured_output

RETURN AgentFlowLaw_procedure
```

The output is itself a prompt-level program that can subsequently be supplied to an LLM for execution.

---

## 25. EXECUTE — Meta-Prompt Instruction

```text
EXECUTE:

Read the user's legal analysis task.

Do NOT solve the legal task directly unless explicitly requested.

Your primary task is to PROGRAM its solution
using the AgentFlowLaw framework.

Transform the user's task into a complete
no-code multi-agent legal analysis procedure.

Determine the required LEGAL_CONTEXT.

Decompose the task into atomic analytical operations.

Create only the agents necessary for this task.

For every agent define:
ROLE,
GOAL,
INPUT,
LOGIC,
STATE,
COMMUNICATION,
EVIDENCE,
OUTPUT.

Use:
Condition,
Loop,
Function,
Label,
Goto
where appropriate.

Define sequential and parallel execution branches.
Explicitly define information transfer between agents.

Separate:
legal source retrieval,
legal interpretation,
conflict detection,
reasoning,
and verification.

Introduce a LEGAL_VERIFICATION_LOOP.
Never invent missing legal sources.

If jurisdiction, validity, source authority,
or evidence cannot be established,
mark the corresponding result as unresolved.

Preserve meaningful disagreements between agents.

Require traceability from conclusions
to arguments, norms, and sources.

The moderator synthesizes results
but does not hide unresolved contradictions.

The framework produces analysis
and recommendations.

The final legally significant decision
belongs to a human.

OUTPUT ONLY:
1. Generated AgentFlowLaw procedure.
2. Required agents.
3. Agent interaction logic.
4. Verification procedure.
5. Structured output schema.

Do not execute the generated procedure
unless explicitly instructed to do so.
```

---

## 26. Formal Representation of the Framework

Let $Q$ denote an initial legal-analysis request:

$$
Q\rightarrow\mathrm{AgentFlowLaw}\rightarrow P_{\mathrm{Law}}
$$

where:

$$
P_{\mathrm{Law}}=\langle C_L,A,G,V,O,H\rangle
$$

and:

- $C_L$ — Legal Context;
- $A=\{a_1,a_2,\ldots,a_n\}$ — dynamically generated set of legal agents;
- $G=(A,E)$ — directed interaction graph between agents;
- $V$ — verification procedure;
- $O$ — structured output specification;
- $H$ — human-control points.

The procedure can subsequently be executed by an LLM:

$$
Q\rightarrow\mathrm{AgentFlowLaw}\rightarrow P_{\mathrm{Law}}\rightarrow\mathrm{LLM}\rightarrow R_{\mathrm{Law}}
$$

> **AgentFlowLaw does not primarily program an answer to a legal question. It programs the procedure for obtaining, checking, tracing, and presenting that answer.**

---

## 27. Core Principle

```text
Legal Question ≠ Prompt for an Answer
```

Instead:

```text
Legal Question
      ↓
Programmed Analytical Procedure
      ↓
Verified Result
      ↓
Human Decision
```

This approach transforms **prompt engineering into no-code programming of legal-analysis procedures**.

AgentFlowLaw therefore serves simultaneously as a **framework**, a **meta-prompt specification**, and a **reusable method** for constructing task-specific multi-agent procedures for the analysis of legal acts.

---

## Authors

**Dmytro Lande**  
**Leonard Strashnoy**

**AgentFlowLaw — Version 1.0 · 2026**
