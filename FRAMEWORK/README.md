# AgentFlowLaw

## A No-Code Framework for Programming Agentic Procedures for Legal Act Analysis

**Dmytro Lande, Leonard Strashnoy**\
**Version 1.0**

------------------------------------------------------------------------

## 1. Purpose and Scope

AgentFlowLaw (AFL) is a domain-specific extension of the AgentFlow
framework designed for no-code programming of agentic procedures for the
analysis of legal acts and other legal and regulatory documents using
Large Language Models (LLMs).

The framework is intended to be used primarily as a meta-prompt. It does
not merely instruct an LLM to solve a legal task directly. Instead, it
transforms a description of a legal analysis task into a structured
no-code agentic procedure that can subsequently be executed by an LLM or
an LLM-based system.

The general processing model is:

``` text
Legal Task → AgentFlowLaw → Agentic Procedure → LLM → Analysis Result
```

AgentFlowLaw defines:

-   the structure of the legal task;
-   the legal context of the analysis;
-   the composition of specialized agents;
-   the functions assigned to individual agents;
-   sequential and parallel execution paths;
-   communication and information transfer between agents;
-   legal-source verification procedures;
-   mechanisms for handling uncertainty and contradictions;
-   the structure of the final output;
-   points of human control.

The purpose of the framework is therefore not to prescribe a particular
legal conclusion, but to program the procedure through which such a
conclusion can be obtained, verified, traced to its sources, and
presented to a human expert.

------------------------------------------------------------------------

## 2. General Concept

AgentFlowLaw is not a programming language in the traditional sense.

The program is represented as a structured natural-language description
of an analytical procedure, while the LLM performs the functions of both
the execution environment and the interpreter.

The basic transformation can be represented as:

**P_Law = F_AFL(T, C, S, R, O)**

where:

-   **T** -- legal analysis task (Task);
-   **C** -- legal context (Legal Context);
-   **S** -- available legal and other relevant sources (Sources);
-   **R** -- requirements and constraints (Requirements);
-   **O** -- required output (Output);
-   **F_AFL** -- AgentFlowLaw framework;
-   **P_Law** -- generated no-code agentic procedure.

Thus, AgentFlowLaw operates at a level above an ordinary prompt:

``` text
Prompt → Meta-Prompt → Agentic Procedure
```

------------------------------------------------------------------------

## 3. Relationship to AgentFlow

AgentFlowLaw inherits the fundamental logical primitives of AgentFlow:

``` text
Condition
Loop
Function
Label
Goto
```

It also preserves the basic agent structure:

``` text
ROLE
STATE
LOGIC
COMMUNICATION
```

In the original AgentFlow model, an agent is defined through its role,
internal state, logic, and communication protocol. AgentFlowLaw retains
this model but extends it to address the requirements of legal analysis.

The following domain-specific components are introduced:

``` text
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

**AgentFlowLaw = AgentFlow + Legal Context + Legal Sources + Legal
Verification + Traceability + Human Control**

These additions reflect the fact that legal analysis requires not only
logical processing of text but also consideration of jurisdiction,
temporal validity, normative authority, provenance of information, and
the possibility of conflicting or insufficient evidence.

------------------------------------------------------------------------

## 4. Input to AgentFlowLaw

AgentFlowLaw accepts a legal task expressed in natural language.

The minimal input is:

``` text
TASK:
{{description_of_legal_task}}

INPUT:
{{legal_document_or_documents}}
```

A more complete input may contain:

``` text
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

If some parameters are not explicitly provided, AgentFlowLaw may derive
them from the available context only when this can be done reliably.

Otherwise, the value must be explicitly represented as:

``` text
UNKNOWN
```

Missing information must not be silently replaced by assumptions.

------------------------------------------------------------------------

## 5. Legal Context

Before constructing an agentic procedure, AgentFlowLaw forms a Legal
Context describing the environment in which the legal task is to be
analyzed.

``` text
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

The Legal Context constitutes a global state of the procedure and is
made available to all agents for which it is relevant.

This distinction is fundamental:

**Context_Law = Data + Jurisdiction + Time + Authority + Sources**

------------------------------------------------------------------------

## 6. Legal Agent Model

The basic AgentFlow agent is represented as:

**a = ⟨R, S, L, C⟩**

where R denotes role, S state, L logic, and C communication.

For AgentFlowLaw, this model is extended as follows:

**a_Law = ⟨R, S, L, C, J, A, E, V, T⟩**

where:

-   **J** -- jurisdiction;
-   **A** -- normative authority;
-   **E** -- evidence and supporting sources;
-   **V** -- temporal validity;
-   **T** -- traceability.

A typical legal agent is defined as:

``` text
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

The extended model does not require every legal agent to perform every
legal operation. Instead, the relevant legal attributes are inherited
from the common context and used according to the agent's specific role.

------------------------------------------------------------------------

## 7. Basic Legal Operations

AgentFlowLaw does not impose a closed vocabulary of legal operations.
However, it defines a reusable set of typical operations that may be
incorporated into generated procedures.

### Extraction operations

``` text
EXTRACT_NORM()
EXTRACT_LEGAL_ENTITY()
EXTRACT_RIGHT()
EXTRACT_OBLIGATION()
EXTRACT_PROHIBITION()
EXTRACT_PERMISSION()
EXTRACT_EXCEPTION()
```

### Source and validity operations

``` text
IDENTIFY_LEGAL_SOURCE()
RETRIEVE_NORM()
CHECK_SOURCE()
CHECK_VALIDITY()
CHECK_JURISDICTION()
CHECK_AUTHORITY()
```

### Comparative and conflict-analysis operations

``` text
COMPARE_NORMS()
DETECT_CONFLICT()
DETECT_AMBIGUITY()
DETECT_GAP()
DETECT_DUPLICATION()
```

### Reasoning and verification operations

``` text
BUILD_LEGAL_ARGUMENT()
VERIFY_ARGUMENT()
TRACE_CONCLUSION()
```

These operations are semantic functions rather than executable software
functions in the traditional sense. Their interpretation and execution
are delegated to an LLM and, where available, connected
information-retrieval or legal-information systems.

------------------------------------------------------------------------

## 8. Legal Sources

A central principle of AgentFlowLaw is the separation of an
LLM-generated interpretation from the legal sources on which that
interpretation is based.

For every significant legal claim, the framework should establish,
whenever possible, the following chain:

``` text
Claim → Norm → Legal Source
```

A legal source can be represented as:

``` text
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

The status of a source is explicitly represented:

``` text
SOURCE_STATUS:
VERIFIED
UNVERIFIED
CONFLICTING
NOT_FOUND
```

If a source cannot be established or verified, the corresponding
conclusion must not be presented as a fully established legal finding.

------------------------------------------------------------------------

## 9. Temporal Validity

Legal norms must be interpreted in relation to the relevant point in
time.

For a norm n and time t, AgentFlowLaw introduces:

**Valid(n, t) ∈ {TRUE, FALSE, UNKNOWN}.**

The corresponding procedure may be expressed as:

``` text
IF VALIDITY == TRUE:
    USE_NORM()

IF VALIDITY == FALSE:
    EXCLUDE_FROM_CURRENT_LEGAL_BASIS()

IF VALIDITY == UNKNOWN:
    MARK_UNCERTAINTY()
    SEND_TO source_verifier
```

This mechanism is intended to prevent the unintentional mixing of
current, repealed, amended, or otherwise temporally incompatible
versions of legal provisions.

------------------------------------------------------------------------

## 10. Normative Authority

AgentFlowLaw explicitly considers the normative authority of legal
sources.

In abstract form:

**Authority(s_i) \> Authority(s_j)**

indicates that source s_i has a higher normative status than source s_j
within the specified legal context.

The framework does not prescribe a universal hierarchy applicable to all
legal systems. Instead, the hierarchy must be defined within the Legal
Context:

``` text
LEGAL_HIERARCHY:
{{jurisdiction_specific_hierarchy}}
```

This makes the procedure adaptable to different jurisdictions and legal
systems.

------------------------------------------------------------------------

## 11. Analysis of Legal Conflicts

Potential conflicts between legal provisions require a separate
analytical procedure.

``` text
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

The resulting status is represented as:

``` text
CONFLICT_STATUS:
CONFIRMED
POSSIBLE
NOT_CONFIRMED
UNRESOLVED
```

A POSSIBLE or UNRESOLVED conflict must not automatically be converted
into a definitive legal conclusion.

------------------------------------------------------------------------

## 12. Uncertainty

Uncertainty is treated as a legitimate analytical result rather than an
error that must always be eliminated.

AgentFlowLaw uses:

``` text
UNCERTAINTY:
NONE
LOW
MEDIUM
HIGH
UNRESOLVED
```

The general rule is:

``` text
IF evidence_insufficient:
    DO_NOT_INVENT()
    MARK_UNRESOLVED()
```

Uncertainty may result from missing sources, unclear wording,
conflicting provisions, unknown validity, insufficient contextual
information, or disagreement between specialized agents.

The system must preserve such uncertainty in the final result.

------------------------------------------------------------------------

## 13. Dynamic Formation of the Legal Agent Swarm

AgentFlowLaw does not require every task to use the same predefined set
of agents.

The composition of the agent swarm is generated dynamically according to
the legal task.

The general procedure is:

``` text
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

This principle prevents unnecessary growth of the agent architecture and
allows simple tasks to use compact procedures while complex legal
analyses can employ larger specialized swarms.

------------------------------------------------------------------------

## 14. Typical Library of Legal Agents

AgentFlowLaw provides a reusable library of typical agent roles:

``` text
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

This list is not a mandatory swarm configuration.

The framework selects only those agents that are required by the task
and may generate additional specialized agents when necessary.

A useful design principle is:

**one agent ≈ one principal analytical function**

An agent should therefore not simultaneously retrieve sources, interpret
norms, identify conflicts, verify evidence, and formulate the final
conclusion when these operations can reasonably be separated.

------------------------------------------------------------------------

## 15. Parallel and Sequential Processing

AgentFlowLaw inherits the AgentFlow mechanism for describing logically
parallel execution branches. In AgentFlow, separate branches may be
represented through `START_PARALLEL([...])` followed by the merging of
results.

For example:

``` text
START_PARALLEL([
    conflict_detector,
    ambiguity_detector,
    gap_detector
])

WAIT_FOR_RESULTS()
MERGE_RESULTS()
```

Parallel execution in this context describes the logical independence of
analytical branches. It does not necessarily imply physical parallel
execution by an underlying LLM.

Importantly, the results of independent agents must not automatically be
reconciled by averaging or majority voting.

A disagreement between agents may itself represent an analytically
significant result.

------------------------------------------------------------------------

## 16. Inter-Agent Communication

Communication between legal agents is represented as directed
information transfer:

**M_ij: a_i → a_j.**

A message may have the following structure:

``` text
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

Agents should transfer not only conclusions but also the evidence and
uncertainty associated with them. This makes downstream verification
possible.

------------------------------------------------------------------------

## 17. Legal Verification Loop

A distinctive component of AgentFlowLaw is the Legal Verification Loop.

The basic cycle is:

``` text
Analysis → Source Verification → Validity Check → Conflict Check → Argument Verification
```

It may be represented as:

``` text
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

The verification cycle must include a termination condition or a maximum
number of iterations to prevent uncontrolled repetition.

The purpose of this loop is not to force every result into a verified
state. If verification cannot be completed because the available
evidence is insufficient, UNRESOLVED is an acceptable final status.

------------------------------------------------------------------------

## 18. Traceability of Legal Conclusions

AgentFlowLaw requires that significant legal conclusions remain
traceable to the information from which they were derived.

The preferred chain is:

``` text
Conclusion → Argument → Norm → Source
```

A result may therefore be represented as:

``` text
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

Traceability makes it possible for a human expert to inspect not only
the generated conclusion but also the path through which it was
obtained.

------------------------------------------------------------------------

## 19. Moderator

The moderator integrates the outputs of the specialized agents.

Its principal functions are:

``` text
COLLECT_RESULTS()
COMPARE_RESULTS()
IDENTIFY_CONTRADICTIONS()
PRESERVE_DISSENT()
CHECK_COMPLETENESS()
BUILD_FINAL_REPORT()
```

The moderator must not arbitrarily modify the outputs of other agents
merely to obtain a consistent final answer.

If two agents produce different but reasonably supported
interpretations:

``` text
DO_NOT_FORCE_CONSENSUS()
```

Both interpretations should be retained together with their respective
arguments, evidence, and uncertainty status.

------------------------------------------------------------------------

## 20. Human Control

AgentFlowLaw is intended to support legal analysis rather than
autonomously replace legally significant human decision-making.

The complete conceptual chain is:

``` text
Legal Documents → AgentFlowLaw → Legal Swarm → Verification → Recommendation → Human
```

The framework therefore includes:

``` text
HUMAN_CONTROL:

FINAL_DECISION:
HUMAN

SYSTEM_ROLE:
ANALYSIS_AND_RECOMMENDATION
```

A human expert may:

``` text
ACCEPT
REJECT
MODIFY
REQUEST_REANALYSIS
REQUEST_ADDITIONAL_SOURCES
```

The human-control point is part of the architecture rather than an
external disclaimer added after the analysis.

------------------------------------------------------------------------

## 21. Standard AgentFlowLaw Procedure

The primary output of AgentFlowLaw is a structured no-code agentic
procedure.

Its recommended general form is:

``` text
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

This structure serves as a template rather than a rigid syntax. It can
be adapted to the complexity and requirements of a particular legal
task.

------------------------------------------------------------------------

## 22. Agent Generation Template

For every agent included in the generated procedure, AgentFlowLaw should
define at least:

``` text
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

Agent responsibilities should be sufficiently narrow to make their
operations interpretable and independently verifiable.

------------------------------------------------------------------------

## 23. Mandatory AgentFlowLaw Rules

Every procedure generated through AgentFlowLaw must follow the following
general rules:

**RULE 1:**\
Never invent legal sources.

**RULE 2:**\
Separate source text from model interpretation.

**RULE 3:**\
Check jurisdiction.

**RULE 4:**\
Check temporal validity.

**RULE 5:**\
Consider normative authority.

**RULE 6:**\
Preserve uncertainty.

**RULE 7:**\
Preserve meaningful disagreements between agents.

**RULE 8:**\
Every significant legal conclusion should be traceable.

**RULE 9:**\
Verification must be separated from primary analysis.

**RULE 10:**\
The final legally significant decision belongs to a human.

These rules constitute invariant constraints of the framework regardless
of the particular composition of the generated agent swarm.

------------------------------------------------------------------------

## 24. AgentFlowLaw Meta-Programming Algorithm

When a legal task is received, AgentFlowLaw performs the following
transformation:

``` text
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

The output of this algorithm is itself a prompt-level program that can
subsequently be supplied to an LLM for execution.

------------------------------------------------------------------------

## 25. EXECUTE: Meta-Prompt Instruction

The following block constitutes the operational core of AgentFlowLaw.
When the framework is used directly as a meta-prompt, this instruction
determines how the LLM should transform the user's task.

``` text
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

------------------------------------------------------------------------

## 26. Formal Representation of the Framework

Let **Q** denote an initial legal-analysis request.

AgentFlowLaw transforms it into a structured procedure **P_Law**:

**Q → AgentFlowLaw → P_Law**

where:

**P_Law = ⟨C_L, A, G, V, O, H⟩**

and:

-   **C_L** -- Legal Context;
-   **A = {a₁, a₂, ..., aₙ}** -- dynamically generated set of legal
    agents;
-   **G = (A, E)** -- directed interaction graph between agents;
-   **V** -- verification procedure;
-   **O** -- structured output specification;
-   **H** -- human-control points.

The procedure **P_Law** can subsequently be executed by an LLM:

**Q → AgentFlowLaw → P_Law → LLM → R_Law**

Consequently, AgentFlowLaw does not primarily program an answer to a
legal question. It programs the procedure for obtaining, checking,
tracing, and presenting that answer.

------------------------------------------------------------------------

## 27. Core Principle

The conceptual distinction underlying AgentFlowLaw can be summarized as
follows:

**Legal Question ≠ Prompt for an Answer**

Instead:

``` text
Legal Question → Programmed Analytical Procedure → Verified Result → Human Decision
```

This approach transforms prompt engineering into no-code programming of
legal-analysis procedures.

AgentFlowLaw therefore serves simultaneously as a framework, a
meta-prompt specification, and a reusable method for constructing
task-specific multi-agent procedures for the analysis of legal acts.

------------------------------------------------------------------------

**AgentFlowLaw -- Version 1.0**\
**Dmytro Lande, Leonard Strashnoy**\
© 2026
