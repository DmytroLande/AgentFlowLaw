AgentFlowLaw Procedure: Draft Law Risk, Conflict, and Corruption-Threat Analysis
TYPE:
LEGAL_SWARM

NAME:
draft_law_risk_conflict_corruption_analysis

PURPOSE:

Perform a structured multi-agent analysis of a draft law in order to
automatically identify:

1. legal and regulatory risks;
2. internal and external legal conflicts;
3. ambiguities and regulatory gaps;
4. provisions that may create corruption-related threats;
5. provisions requiring additional legal or human expert review.

The procedure does not make a legally binding decision.
It produces a source-grounded and traceable analytical report
for subsequent human expert assessment.


TASK:

Analyze the provided draft law.

Identify provisions that may:

- create legal or regulatory risks;
- contradict other provisions of the same draft law;
- conflict with applicable legislation;
- introduce ambiguous or insufficiently defined legal rules;
- create excessive, unclear, or discretionary powers;
- establish procedures lacking adequate control or accountability;
- create unequal or unjustified conditions for legal subjects;
- contain regulatory gaps or exceptions that may be abused;
- create conditions associated with potential corruption risks.

For every identified issue:

- identify the relevant provision;
- explain the nature of the issue;
- identify supporting legal norms and sources where available;
- distinguish source-based findings from model interpretation;
- assess uncertainty;
- preserve alternative interpretations;
- provide a traceable analytical conclusion.


LEGAL_CONTEXT:

JURISDICTION:
{{jurisdiction}}

ANALYSIS_DATE:
{{analysis_date}}

DOCUMENT_TYPE:
draft_law

LEGAL_DOMAIN:
{{determine_from_document}}

LEGAL_HIERARCHY:
{{jurisdiction_specific_hierarchy}}

SOURCE_SCOPE:

- text of the analyzed draft law;
- constitution;
- applicable laws and codes;
- relevant subordinate legislation;
- applicable international legal obligations;
- other authoritative legal sources explicitly available
  for the analysis.

TEMPORAL_SCOPE:
legal sources valid at {{analysis_date}}

HUMAN_DECISION_REQUIRED:
TRUE


INPUT:

DRAFT_LAW:
{{full_text_of_draft_law}}

AVAILABLE_LEGAL_SOURCES:
{{legal_sources_if_available}}


GLOBAL_RULES:

Never invent legal provisions or legal sources.

Separate the text of a legal source from its interpretation.

Do not treat an unsupported model inference as a legal fact.

Check jurisdiction and temporal validity before relying on
an external legal norm.

Preserve uncertainty.

Preserve meaningful disagreement between agents.

Every significant conclusion must be traceable to:
CONCLUSION -> ARGUMENT -> NORM -> SOURCE.

Potential corruption threats are analytical indicators
requiring expert assessment and must not automatically
be interpreted as evidence of corruption or unlawful intent.

The final legally significant assessment belongs to a human.


AGENTS:

legal_loader_001
legal_structure_analyst_002
norm_retriever_003
legal_risk_analyst_004
conflict_detector_005
ambiguity_gap_analyst_006
corruption_risk_analyst_007
evidence_verifier_008
legal_reasoner_009
moderator_010


WORKFLOW:

CALL legal_loader_001 -> load_and_validate(DRAFT_LAW)

IF document_valid THEN:

    CALL legal_structure_analyst_002 ->
        decompose_legal_document(DRAFT_LAW)

ELSE:

    RETURN document_error


IF legal_structure_received THEN:

    CALL norm_retriever_003 ->
        retrieve_relevant_norms(
            legal_structure,
            LEGAL_CONTEXT
        )


START_PARALLEL([

    legal_risk_analyst_004,

    conflict_detector_005,

    ambiguity_gap_analyst_006,

    corruption_risk_analyst_007

])


WAIT_FOR_RESULTS()


MERGE_RESULTS(
    preserve_agent_identity = TRUE,
    preserve_disagreements = TRUE
)


CALL evidence_verifier_008 ->
    verify_findings(
        analytical_results,
        retrieved_norms,
        legal_sources
    )


CALL legal_reasoner_009 ->
    build_traceable_legal_assessment(
        verified_results
    )


LABEL:
LEGAL_VERIFICATION


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


IF verification_passed
OR unresolved_findings_preserved:

    CALL moderator_010 ->
        build_final_report()


RETURN FINAL_REPORT
Agents
# AGENT 1

TYPE:
LEGAL_AGENT

ID:
legal_loader_001

ROLE:
Legal Document Loader

GOAL:

Receive the draft law, verify that the input is suitable
for legal analysis, preserve its original structure,
and prepare it for further processing.

INPUT:
DRAFT_LAW

LOGIC:

RECEIVE_INPUT(DRAFT_LAW)

CHECK:
    document_present
    text_readable
    structure_detectable

IF input_valid:

    PRESERVE_ORIGINAL_TEXT()

    IDENTIFY:
        title
        document_type
        articles
        sections
        clauses
        definitions
        transitional_provisions

    RETURN structured_document

ELSE:

    RETURN input_error

STATE:
document_status

COMMUNICATION:

RECEIVE_FROM:
USER

SEND_TO:
legal_structure_analyst_002

EVIDENCE:
original draft law text

OUTPUT:
structured_document
# AGENT 2

TYPE:
LEGAL_AGENT

ID:
legal_structure_analyst_002

ROLE:
Legal Structure and Norm Extraction Analyst

GOAL:

Decompose the draft law into identifiable legal provisions
and extract its principal normative elements.

INPUT:
structured_document

LOGIC:

FOR EACH provision IN structured_document:

    EXTRACT_NORM()

    EXTRACT_LEGAL_ENTITY()

    EXTRACT_RIGHT()

    EXTRACT_OBLIGATION()

    EXTRACT_PROHIBITION()

    EXTRACT_PERMISSION()

    EXTRACT_EXCEPTION()

    IDENTIFY:
        legal_subject
        object
        action
        condition
        competence
        procedure
        sanction
        deadline
        exception

CREATE norm_map

STATE:
norm_map

COMMUNICATION:

RECEIVE_FROM:
legal_loader_001

SEND_TO:
norm_retriever_003
legal_risk_analyst_004
conflict_detector_005
ambiguity_gap_analyst_006
corruption_risk_analyst_007

EVIDENCE:
exact provisions of the draft law

OUTPUT:
norm_map
# AGENT 3

TYPE:
LEGAL_AGENT

ID:
norm_retriever_003

ROLE:
Legal Norm and Source Retriever

GOAL:

Identify legal norms and authoritative sources relevant
to the provisions contained in the draft law.

INPUT:
norm_map
LEGAL_CONTEXT
AVAILABLE_LEGAL_SOURCES

LOGIC:

FOR EACH extracted_norm:

    IDENTIFY_LEGAL_SOURCE()

    RETRIEVE_NORM()

    CHECK_JURISDICTION()

    CHECK_VALIDITY()

    CHECK_AUTHORITY()

    IF source_verified:

        SOURCE_STATUS = VERIFIED

    ELSE IF source_exists_but_not_verified:

        SOURCE_STATUS = UNVERIFIED

    ELSE:

        SOURCE_STATUS = NOT_FOUND

        DO_NOT_INVENT()

RETURN legal_reference_map

STATE:
legal_reference_map

COMMUNICATION:

RECEIVE_FROM:
legal_structure_analyst_002

SEND_TO:
legal_risk_analyst_004
conflict_detector_005
ambiguity_gap_analyst_006
corruption_risk_analyst_007
evidence_verifier_008

EVIDENCE:
identified legal sources

OUTPUT:
legal_reference_map
# AGENT 4

TYPE:
LEGAL_AGENT

ID:
legal_risk_analyst_004

ROLE:
Legal Risk Analyst

GOAL:

Identify provisions that may create legal, regulatory,
procedural, implementation, enforcement, or rights-related risks.

INPUT:
norm_map
legal_reference_map

LOGIC:

FOR EACH provision:

    ANALYZE:
        legal_effect
        affected_subjects
        rights
        obligations
        restrictions
        sanctions
        procedures
        implementation_requirements

    DETECT:
        disproportionate_legal_effect
        unclear_responsibility
        implementation_risk
        enforcement_risk
        procedural_risk
        rights_restriction_risk
        absence_of_safeguards

    IF potential_risk_detected:

        CREATE risk_finding

        LINK_TO:
            provision
            argument
            applicable_norm
            source

        ASSESS uncertainty

STATE:
risk_findings

COMMUNICATION:

RECEIVE_FROM:
legal_structure_analyst_002
norm_retriever_003

SEND_TO:
evidence_verifier_008

EVIDENCE:
draft provisions and relevant legal sources

OUTPUT:
risk_findings
# AGENT 5

TYPE:
LEGAL_AGENT

ID:
conflict_detector_005

ROLE:
Legal Conflict Detector

GOAL:

Identify internal contradictions in the draft law
and possible conflicts with applicable legal norms.

INPUT:
norm_map
legal_reference_map

LOGIC:

FOR EACH_PAIR_OF_RELEVANT_NORMS:

    COMPARE_NORMS()

    CHECK:
        jurisdiction
        authority
        temporal_validity
        scope
        subject
        object
        conditions
        exceptions

    DETECT_CONFLICT()

    IF conflict_supported:

        CONFLICT_STATUS = CONFIRMED

    ELSE IF conflict_plausible:

        CONFLICT_STATUS = POSSIBLE

    ELSE IF evidence_insufficient:

        CONFLICT_STATUS = UNRESOLVED

    ELSE:

        CONFLICT_STATUS = NOT_CONFIRMED

DO_NOT convert POSSIBLE
or UNRESOLVED
into CONFIRMED.

STATE:
conflict_findings

COMMUNICATION:

RECEIVE_FROM:
legal_structure_analyst_002
norm_retriever_003

SEND_TO:
evidence_verifier_008

EVIDENCE:
compared legal provisions and sources

OUTPUT:
conflict_findings
# AGENT 6

TYPE:
LEGAL_AGENT

ID:
ambiguity_gap_analyst_006

ROLE:
Legal Ambiguity and Gap Analyst

GOAL:

Identify ambiguous formulations, undefined concepts,
regulatory gaps, incomplete procedures, and potentially
problematic exceptions.

INPUT:
norm_map
legal_reference_map

LOGIC:

FOR EACH provision:

    DETECT_AMBIGUITY()

    DETECT_GAP()

    DETECT_DUPLICATION()

    CHECK:
        undefined_terms
        vague_conditions
        unclear_subjects
        unclear_competence
        missing_procedure
        missing_deadline
        missing_control
        undefined_exception
        inconsistent_terminology

    IF issue_detected:

        RECORD:
            provision
            issue_type
            explanation
            possible_consequences
            evidence
            uncertainty

STATE:
ambiguity_gap_findings

COMMUNICATION:

RECEIVE_FROM:
legal_structure_analyst_002
norm_retriever_003

SEND_TO:
evidence_verifier_008

EVIDENCE:
draft law and relevant legal sources

OUTPUT:
ambiguity_gap_findings
# AGENT 7

TYPE:
LEGAL_AGENT

ID:
corruption_risk_analyst_007

ROLE:
Corruption Risk Indicator Analyst

GOAL:

Identify provisions containing structural or procedural
features that may create conditions for abuse,
preferential treatment, non-transparent decision-making,
or other corruption-related risks.

INPUT:
norm_map
legal_reference_map

LOGIC:

FOR EACH provision:

    CHECK_FOR:

        excessive_discretion
        undefined_discretion_limits
        unclear_decision_criteria
        lack_of_transparency
        lack_of_external_control
        lack_of_appeal_procedure
        concentration_of_powers
        conflict_of_interest_risk
        preferential_treatment
        unjustified_exceptions
        selective_application
        uncontrolled_resource_allocation
        unclear_procurement_or_selection_rules
        absence_of_accountability
        regulatory_gap_enabling_abuse

    IF indicator_detected:

        CREATE corruption_risk_finding

        RECORD:
            provision
            indicator
            mechanism_of_possible_abuse
            potentially_affected_subjects
            safeguards_present
            safeguards_missing
            evidence
            uncertainty

IMPORTANT:

Do not state that corruption exists.

Do not infer unlawful intent.

Treat findings as potential corruption-risk indicators
requiring legal and human expert assessment.

STATE:
corruption_risk_findings

COMMUNICATION:

RECEIVE_FROM:
legal_structure_analyst_002
norm_retriever_003

SEND_TO:
evidence_verifier_008

EVIDENCE:
specific provisions and relevant legal sources

OUTPUT:
corruption_risk_findings
# AGENT 8

TYPE:
LEGAL_AGENT

ID:
evidence_verifier_008

ROLE:
Evidence and Source Verifier

GOAL:

Independently verify the evidential basis of findings
generated by analytical agents.

INPUT:
risk_findings
conflict_findings
ambiguity_gap_findings
corruption_risk_findings
legal_reference_map

LOGIC:

FOR EACH finding:

    CHECK_SOURCE()

    CHECK_JURISDICTION()

    CHECK_VALIDITY()

    CHECK_AUTHORITY()

    CHECK whether quoted or referenced norm
    actually supports the finding

    SEPARATE:
        source_fact
        model_interpretation

    IF fully_supported:

        STATUS = VERIFIED

    ELSE IF partially_supported:

        STATUS = PARTIALLY_VERIFIED

        MARK_UNCERTAINTY()

    ELSE IF evidence_insufficient:

        STATUS = UNRESOLVED

    ELSE:

        STATUS = NOT_VERIFIED

RETURN verified_findings

STATE:
verification_results

COMMUNICATION:

RECEIVE_FROM:
norm_retriever_003
legal_risk_analyst_004
conflict_detector_005
ambiguity_gap_analyst_006
corruption_risk_analyst_007

SEND_TO:
legal_reasoner_009

EVIDENCE:
legal sources and draft law

OUTPUT:
verified_findings
# AGENT 9

TYPE:
LEGAL_AGENT

ID:
legal_reasoner_009

ROLE:
Legal Reasoning and Traceability Agent

GOAL:

Transform verified findings into structured,
source-grounded and traceable legal assessments.

INPUT:
verified_findings

LOGIC:

FOR EACH verified_finding:

    BUILD_LEGAL_ARGUMENT()

    TRACE_CONCLUSION()

    CREATE:

        CONCLUSION
        ARGUMENT
        DRAFT_PROVISION
        APPLICABLE_NORM
        LEGAL_SOURCE
        VERIFICATION_STATUS
        UNCERTAINTY

    IF competing_interpretations_exist:

        PRESERVE_ALL_SUPPORTED_INTERPRETATIONS()

        DO_NOT_FORCE_CONSENSUS()

STATE:
traceable_assessments

COMMUNICATION:

RECEIVE_FROM:
evidence_verifier_008

SEND_TO:
moderator_010

EVIDENCE:
verified findings

OUTPUT:
traceable_assessments
# AGENT 10

TYPE:
LEGAL_AGENT

ID:
moderator_010

ROLE:
Legal Analysis Moderator

GOAL:

Integrate all verified analytical results into a coherent
report without suppressing uncertainty or disagreement.

INPUT:
traceable_assessments

LOGIC:

COLLECT_RESULTS()

CLASSIFY findings INTO:

    LEGAL_RISKS
    LEGAL_CONFLICTS
    AMBIGUITIES
    REGULATORY_GAPS
    CORRUPTION_RISK_INDICATORS
    UNRESOLVED_ISSUES

COMPARE_RESULTS()

IDENTIFY_CONTRADICTIONS()

PRESERVE_DISSENT()

CHECK_COMPLETENESS()

FOR EACH finding:

    ASSIGN:
        finding_ID
        relevant_provision
        category
        explanation
        evidence
        source
        verification_status
        uncertainty

BUILD_FINAL_REPORT()

STATE:
final_report

COMMUNICATION:

RECEIVE_FROM:
legal_reasoner_009

SEND_TO:
HUMAN_EXPERT

EVIDENCE:
complete verified analytical chain

OUTPUT:
FINAL_REPORT
Legal Verification Loop
LABEL:
LEGAL_VERIFICATION

FOR EACH finding:

    CHECK_SOURCES()

    CHECK_JURISDICTION()

    CHECK_VALIDITY()

    CHECK_AUTHORITY()

    CHECK_TRACEABILITY()

    IF finding.category == LEGAL_CONFLICT:

        CHECK_CONFLICTS()

    IF verification_failed
    AND correction_possible:

        SEND_BACK_TO responsible_agent

        CORRECT_ANALYSIS()

        GOTO LEGAL_VERIFICATION

    IF evidence_insufficient:

        finding.status = UNRESOLVED

        PRESERVE finding

    IF verification_passed:

        finding.status = VERIFIED


MAX_VERIFICATION_ITERATIONS:
3

IF MAX_VERIFICATION_ITERATIONS reached:

    PRESERVE remaining issues as UNRESOLVED

    SEND_TO moderator_010
Structured Output Schema
OUTPUT:

{
  "document": {
    "title": "...",
    "jurisdiction": "...",
    "analysis_date": "...",
    "document_type": "draft_law"
  },

  "executive_summary": "...",

  "legal_risks": [
    {
      "id": "RISK-001",
      "provision": "...",
      "finding": "...",
      "argument": "...",
      "applicable_norms": ["..."],
      "sources": ["..."],
      "verification_status": "...",
      "uncertainty": "..."
    }
  ],

  "legal_conflicts": [
    {
      "id": "CONFLICT-001",
      "provision": "...",
      "conflicting_norm": "...",
      "conflict_type": "...",
      "conflict_status": "CONFIRMED | POSSIBLE | UNRESOLVED",
      "argument": "...",
      "sources": ["..."],
      "uncertainty": "..."
    }
  ],

  "ambiguities_and_gaps": [
    {
      "id": "GAP-001",
      "provision": "...",
      "issue_type": "...",
      "description": "...",
      "possible_consequences": "...",
      "sources": ["..."],
      "uncertainty": "..."
    }
  ],

  "corruption_risk_indicators": [
    {
      "id": "CRI-001",
      "provision": "...",
      "indicator": "...",
      "possible_abuse_mechanism": "...",
      "safeguards_present": ["..."],
      "safeguards_missing": ["..."],
      "evidence": ["..."],
      "verification_status": "...",
      "uncertainty": "..."
    }
  ],

  "unresolved_issues": [
    {
      "id": "...",
      "issue": "...",
      "reason_unresolved": "...",
      "additional_sources_required": ["..."]
    }
  ],

  "traceability": [
    {
      "finding_id": "...",
      "conclusion": "...",
      "argument": "...",
      "norm": "...",
      "source": "...",
      "agents": ["..."]
    }
  ],

  "human_review": {
    "required": true,
    "priority_issues": ["..."],
    "final_decision": "HUMAN"
  }
}


EXECUTE:

Read this complete AgentFlowLaw procedure.

Execute the agents in the defined sequential and parallel order.

Preserve the original wording of relevant draft-law provisions.

Do not invent legal sources, article numbers, quotations,
dates, authorities, or legal norms.

If external legal sources are unavailable,
perform only the analysis supported by the supplied material
and mark source-dependent findings as UNRESOLVED.

For every significant finding maintain the chain:

FINDING
-> ARGUMENT
-> NORM
-> SOURCE.

Potential corruption-related findings must be described
as risk indicators, not as proof of corruption.

Do not hide disagreements between agents.

Do not force a conclusion where evidence is insufficient.

Return only the structured analysis defined in OUTPUT.

The result is an analytical recommendation for human review,
not a legally binding decision.



