---
title: "Neurotransparency Specification (NTS)"
short_title: "NTS"
version: "2.0.0"
status: "Active"
type: "specification"
layer: "normative-disclosure"
created: "2025-12-18"
updated: "2025-12-18"
author: "Waveframe Labs"
maintainer: "Waveframe Labs"
contact: "swright@waveframelabs.org"
license: "CC-BY-4.0"
doi: "TBD"
orcid: "0009-0006-6043-9295"
related:
  - "Neurotransparency Doctrine (NTD)"
  - "Aurora Research Initiative (ARI)"
  - "Aurora Workflow Orchestration (AWO)"
  - "CRI-CORE"
ai_assisted: "partial"
ai_assistance_details: "AI-assisted structural drafting and consistency review under full human direction and final approval."
policy_version: "ARI-Metadata-2.0.0"
---

# Neurotransparency Specification (NTS) v2.0.0
*Normative Disclosure Requirements for Cognitive Influence in AI–Human Systems*

## Introduction — Specification Position & Authority

This document defines the **Neurotransparency Specification (NTS)** — a **normative compliance specification** governing the disclosure of epistemically relevant AI influence in AI–human scientific and technical artifacts.

NTS specifies **what must be disclosed** for an artifact to be considered epistemically legitimate under Neurotransparency. It does not define why these requirements exist, how they are operationalized, or how they are enforced.

---

### Nature of the Specification

NTS is a **structural disclosure standard**.

It defines:
- minimum attribution requirements for AI involvement,
- minimum provenance and reconstruction expectations,
- explicit failure conditions for epistemic legitimacy.

NTS does **not**:
- prescribe workflows,
- mandate tools, vendors, or models,
- require access to internal model reasoning,
- enforce compliance mechanically,
- evaluate scientific correctness or merit.

Compliance with NTS is binary: required disclosures either exist and are coherent, or they do not.

---

### Position Within the Aurora Stack

NTS occupies the **normative disclosure layer** of the Aurora governance stack.

Its role is strictly bounded:

- **Neurotransparency Doctrine (NTD)**  
  Defines *why* cognitive traceability is required for epistemic legitimacy.

- **Neurotransparency Specification (NTS)**  
  Defines *what must be disclosed* when AI or other non-local cognition influences claims or decisions.

- **Aurora Research Initiative (ARI)**  
  Adopts NTS as a binding standard and determines institutional legitimacy and consequences.

- **Aurora Workflow Orchestration (AWO)**  
  Defines *when* and *where* NTS-compliant artifacts are produced within workflows.

- **CRI-CORE**  
  Determines *whether* required NTS artifacts exist and enforces declared constraints mechanically.

NTS does not override or substitute for any other layer.  
If NTS attempts to answer *why*, *when*, *how*, or *whether*, it is operating out of scope.

---

### Authority and Adoption

NTS has **no inherent enforcement authority**.

Its authority derives exclusively from:
- formal adoption by an institution (e.g., ARI), or
- explicit declaration by a project, workflow, or artifact.

Once adopted, NTS requirements are **non-optional** for all claim-affecting cognition within scope. Selective or partial compliance is not considered valid.

NTS governs disclosure obligations only.  
Judgment, enforcement, and remediation are defined downstream.

---

### Normative Boundary

NTS establishes a single normative boundary:

> Cognition that materially influences a claim or decision must be externally attributable and reconstructible at a summary level.

NTS does not require exposure of internal reasoning, raw prompts, or proprietary model details. It requires only the minimum information necessary to make epistemic influence **discoverable, auditable, and human-owned**.

This boundary preserves legitimacy without mandating surveillance or interpretability.

---

### Relationship to Scientific Legitimacy

NTS does not evaluate:
- correctness,
- rigor,
- novelty,
- or empirical validity.

It evaluates **epistemic legitimacy only**.

An artifact may be scientifically correct and still be non-compliant with NTS.  
Conversely, NTS compliance does not imply correctness — only that the influence of AI-assisted cognition is transparently disclosed and attributable.

## 1. Scope of the Specification

This section defines the **normative scope** of the Neurotransparency Specification (NTS): what it governs, what it applies to, and what it explicitly excludes.

NTS applies only to **epistemically relevant cognition** — human or synthetic — that materially influences a claim, conclusion, decision, or published artifact.

---

### 1.1 What NTS Governs

NTS governs **disclosure requirements** for cognition that affects epistemic outcomes.

Specifically, NTS applies to:

- scientific, technical, analytical, or policy claims,
- research artifacts, reports, specifications, and governance documents,
- AI–human collaborative workflows where AI output influences outcomes,
- automated or semi-automated reasoning pipelines that affect conclusions,
- derivative artifacts whose content depends on prior AI-influenced cognition.

If a cognitive process influences **what is asserted**, **what is concluded**, or **what is decided**, that process is within scope.

NTS is agnostic to:
- domain (science, engineering, governance, policy),
- toolchain,
- model architecture,
- institutional affiliation.

---

### 1.2 Epistemic Influence Threshold

NTS applies only when a cognitive contribution crosses the **epistemic influence threshold**.

A contribution is considered *in scope* if it:

- introduces novel content,
- alters interpretation, framing, or weighting of evidence,
- affects selection among alternatives,
- shapes conclusions, claims, or decisions,
- meaningfully constrains downstream reasoning.

Purely mechanical or clerical operations do **not** cross this threshold.

---

### 1.3 What NTS Explicitly Excludes

NTS does **not** govern:

- internal cognition of humans or models that does not influence outputs,
- private brainstorming, exploration, or discarded drafts,
- spelling, grammar, formatting, or stylistic edits,
- compilation, rendering, or file conversion steps,
- deterministic execution of already-approved logic,
- model internals, hidden states, or proprietary reasoning traces,
- prompt content unless explicitly designated as epistemically relevant.

NTS does **not** require:
- disclosure of chain-of-thought,
- access to internal model reasoning,
- exposure of proprietary systems,
- surveillance of human cognition.

If a process does not alter epistemic justification, it is out of scope.

---

### 1.4 Artifact-Level Scope

NTS applies at the **artifact level**, not the repository or individual level.

An artifact is within scope if:

- it asserts claims,
- it depends on AI-influenced reasoning,
- it is published, shared, or treated as authoritative.

An artifact may be:
- compliant,
- non-compliant,
- or out of scope.

NTS makes no assumptions about the intent, competence, or credibility of the author.

---

### 1.5 Temporal Scope

NTS applies to:

- cognition performed during the creation of an artifact,
- cognition incorporated from prior artifacts,
- cognition reused or referenced from earlier workflows.

Legacy artifacts MAY be retroactively annotated for compliance but are not automatically invalidated by lack of prior disclosure unless explicitly governed.

---

### 1.6 Boundary Condition

The scope of NTS is intentionally minimal.

NTS governs **disclosure of epistemic influence**, nothing more.

If a requirement cannot be expressed as a disclosure obligation, it does not belong in this specification.

---

This section establishes the enforceable boundaries of NTS applicability.

## 2. Normative Compliance Model

This section defines what it means for an artifact, workflow, or release to be **Neurotransparency-compliant** under NTS.

NTS defines **minimum normative compliance**, not best practices, not maximal disclosure, and not correctness of results.

---

### 2.1 Definition of NTS Compliance

An artifact is **NTS-compliant** if and only if:

- all required NTS disclosure fields are present,
- all epistemically relevant AI influence is explicitly declared,
- attribution of cognitive roles is unambiguous,
- human decision ownership is clearly identified,
- required disclosures are sufficient to permit reconstruction **in principle** of how AI influenced the outcome.

Compliance is binary.

An artifact is either compliant or non-compliant under this specification.

---

### 2.2 Minimum Disclosure Standard

NTS establishes a **minimum disclosure floor**, not a ceiling.

An artifact MAY disclose more than required by NTS, but MUST NOT disclose less.

Compliance requires that no epistemically relevant AI influence is:
- hidden,
- implied without declaration,
- retroactively rationalized,
- or attributed to “the model” as an autonomous agent.

---

### 2.3 Artifact-Level Compliance

NTS compliance is evaluated at the **artifact level**.

Each artifact is independently assessed based on:
- its own disclosures,
- its declared dependencies,
- and the epistemic influence embedded in its content.

A compliant artifact MAY depend on:
- other compliant artifacts,
- non-AI artifacts,
- or legacy artifacts with explicit disclosure.

A non-compliant artifact SHALL NOT be treated as epistemically legitimate under NTS-aligned systems.

---

### 2.4 Human Epistemic Authority Invariant

NTS enforces a non-negotiable invariant:

**AI systems do not make epistemic decisions. Humans do.**

Therefore:
- AI outputs are advisory by default,
- acceptance, rejection, or weighting of AI input is always a human action,
- responsibility for claims rests with an identifiable human decision owner.

Any artifact that attributes decisions, conclusions, or authority to an AI system is **non-compliant**.

---

### 2.5 Reconstruction Principle

NTS compliance requires **reconstructibility in principle**, not full replay.

A compliant artifact MUST provide enough structured disclosure to allow a competent reviewer to understand:

- what kind of AI cognition occurred,
- where it influenced the artifact,
- how it was used,
- and who accepted responsibility for its use.

NTS does not require:
- access to proprietary systems,
- disclosure of internal model reasoning,
- exact prompt transcripts.

If epistemic influence cannot be reconstructed even conceptually, the artifact is non-compliant.

---

### 2.6 Non-Judgment Clause

NTS does not evaluate:

- scientific correctness,
- methodological rigor,
- quality of reasoning,
- validity of conclusions,
- ethical desirability.

NTS evaluates **legitimacy of epistemic disclosure only**.

A compliant artifact may still be wrong.
A correct artifact may still be non-compliant.

---

### 2.7 Failure Conditions

An artifact SHALL be considered **non-compliant** if:

- AI materially influenced reasoning and was undeclared,
- decision ownership is ambiguous or missing,
- AI is treated as an epistemic authority,
- required disclosures are absent or misleading,
- AI influence cannot be reconstructed in principle.

Non-compliance invalidates epistemic legitimacy under NTS-aligned review, tooling, and governance systems.

---

This section defines the normative conditions under which an artifact may be considered Neurotransparency-compliant.

## 3. Definitions & Terminology

This section defines the **normative vocabulary** used throughout the Neurotransparency Specification (NTS).  
All terms defined here are authoritative for this document and SHALL be interpreted consistently wherever they appear.

Terms are included **only** where they are required for enforcement, review, or unambiguous interpretation.  
Undefined terms SHALL be interpreted according to their plain meaning in technical and scientific usage.

---

### 3.1 Artifact

An **artifact** is any produced object whose content may carry epistemic weight, including but not limited to:

- research papers and reports  
- technical specifications  
- analyses, models, simulations, or datasets  
- governance documents  
- derived outputs (e.g., summaries, conclusions, recommendations)

An artifact is considered **epistemically relevant** if it asserts, supports, or depends upon a claim.

---

### 3.2 Claim

A **claim** is any assertion, conclusion, decision, or statement presented as true, probable, justified, or authoritative.

Claims may be:
- scientific  
- technical  
- analytical  
- normative  
- policy-relevant  

If an artifact contains claims, it is subject to NTS evaluation.

---

### 3.3 Cognition

**Cognition** refers to any process that transforms information in a way that may affect epistemic outcomes.

Cognition includes, but is not limited to:
- reasoning  
- inference  
- synthesis  
- evaluation  
- interpretation  
- selection among alternatives  

Cognition may be performed by humans, AI systems, or hybrid workflows.

---

### 3.4 Cognitive Influence

**Cognitive influence** exists when a cognitive process materially affects:

- the content of an artifact,  
- the structure of reasoning,  
- the selection or weighting of evidence,  
- the formulation, acceptance, or rejection of claims.

Cognitive influence is evaluated by effect, not intent.

---

### 3.5 Cognitive Influence Threshold

The **cognitive influence threshold** is the point at which cognition becomes epistemically relevant and triggers NTS disclosure obligations.

The threshold is crossed when cognition:
- introduces novel content,  
- alters justification structure, or  
- constrains downstream reasoning or decisions.

Purely mechanical or cosmetic transformations do not cross this threshold.

---

### 3.6 AI System

An **AI system** is any computational system that produces outputs via learned, probabilistic, heuristic, or non-deterministic processes, including but not limited to:

- large language models  
- generative models  
- decision-support systems  
- automated analysis tools  

Tool classification is functional, not vendor-based.

---

### 3.7 AI Influence

**AI influence** refers to cognitive influence originating from an AI system that contributes to epistemically relevant outcomes.

AI influence MAY be:
- editorial  
- analytical  
- generative  
- comparative  
- decision-informing  

AI influence does not constitute decision authority.

---

### 3.8 Human Decision Owner

The **human decision owner** is the identifiable human agent who:

- evaluates AI output,  
- accepts, rejects, or modifies it, and  
- assumes epistemic responsibility for resulting claims.

All claims governed by NTS MUST have an identifiable human decision owner.

---

### 3.9 Disclosure

**Disclosure** is the structured declaration of epistemically relevant AI influence as required by this specification.

Disclosure MUST be:
- explicit,  
- attributable,  
- sufficient for reconstruction in principle.

Disclosure does not require exposure of proprietary or internal reasoning.

---

### 3.10 Reconstruction

**Reconstruction** is the ability for an independent reviewer to understand, after the fact:

- what kind of cognition occurred,  
- where AI influenced outcomes,  
- how that influence was incorporated,  
- and who assumed responsibility.

Reconstruction is conceptual and procedural, not computational replay.

---

### 3.11 Compliance

**Compliance** refers to satisfaction of all mandatory NTS requirements applicable to an artifact.

Compliance is evaluated independently of correctness, quality, or merit.

---

### 3.12 Non-Compliance

**Non-compliance** is the failure to meet one or more mandatory requirements of NTS.

A non-compliant artifact SHALL NOT be considered epistemically legitimate within NTS-aligned systems.

---

This section locks the vocabulary used throughout NTS and SHALL govern interpretation of all subsequent requirements.

## 4. Cognitive Influence Threshold

This section defines the conditions under which cognition becomes **epistemically relevant** and therefore triggers mandatory disclosure obligations under the Neurotransparency Specification (NTS).

NTS does not require disclosure of all cognition.  
It requires disclosure only when cognition materially influences epistemic outcomes.

---

### 4.1 Threshold Principle

A cognitive process crosses the **cognitive influence threshold** if and only if it has a material effect on:

- the content of an artifact,
- the structure of reasoning,
- the interpretation or weighting of evidence,
- the selection among competing alternatives,
- or the formulation, acceptance, or rejection of a claim.

Threshold evaluation is outcome-based, not intent-based.

---

### 4.2 In-Scope Cognitive Influence

The following categories of cognition SHALL be considered to cross the cognitive influence threshold:

- generation of novel claims, hypotheses, or explanations,
- synthesis or abstraction that alters meaning or emphasis,
- analytical reasoning contributing to conclusions,
- comparative evaluation of alternatives where selection impacts outcomes,
- framing or reframing that affects interpretation,
- constraint of downstream reasoning paths,
- decision-informing recommendations that are accepted or relied upon.

If cognition affects **what is asserted** or **why it is justified**, it is in scope.

---

### 4.3 Out-of-Scope Cognitive Activity

The following activities do **not** cross the cognitive influence threshold and SHALL NOT trigger disclosure obligations:

- spelling, grammar, or formatting corrections,
- stylistic rephrasing that preserves meaning,
- file conversion or rendering (e.g., Markdown to PDF),
- deterministic execution of already-approved logic,
- clerical organization or sorting without interpretive change,
- private exploration or discarded drafts that do not influence outputs.

Out-of-scope activity MAY involve AI systems without triggering NTS.

---

### 4.4 AI-Specific Threshold Clarification

AI involvement alone does not trigger disclosure.

Disclosure is required only when AI output:

- is incorporated into an artifact,
- influences reasoning or decisions,
- or constrains epistemic outcomes.

AI outputs that are generated but not used, adopted, or relied upon do not cross the threshold.

---

### 4.5 Decision Boundary

The cognitive influence threshold is crossed at the moment when a human decision owner:

- accepts AI-generated content,
- incorporates AI-assisted analysis,
- relies on AI output to justify a claim,
- or allows AI influence to shape conclusions.

Human acceptance, not AI generation, determines threshold crossing.

---

### 4.6 Ambiguous Cases

In cases of ambiguity, the following rule SHALL apply:

**When in doubt, disclose.**

Ambiguous influence SHOULD be treated as in scope to preserve epistemic legitimacy.

This rule favors transparency without mandating maximal disclosure.

---

### 4.7 Threshold Enforcement

Threshold determination is a normative requirement of this specification.

NTS defines:
- when disclosure is required,
- not how threshold detection is implemented.

Enforcement MAY be manual, procedural, or tool-assisted in downstream systems.

---

This section defines the activation condition for all subsequent NTS disclosure and compliance requirements.
## 5. Disclosure Requirements

This section defines the **mandatory disclosure elements** required once the cognitive influence threshold defined in Section 4 is crossed.

Disclosure under NTS is **structured, proportional, and minimal**.  
It exists to make epistemic influence visible without exposing internal cognition or proprietary details.

---

### 5.1 General Disclosure Obligation

When the cognitive influence threshold is crossed, an artifact MUST include an explicit disclosure of AI involvement.

Disclosure SHALL be:
- truthful,
- complete with respect to epistemically relevant influence,
- attributable to a human decision owner,
- sufficient to permit reconstruction in principle.

Partial or implied disclosure SHALL be treated as non-compliance.

---

### 5.2 AI Involvement Declaration

Each artifact crossing the threshold MUST declare whether AI was involved.

If AI was involved, the artifact MUST specify the **type of involvement** using one or more of the following classifications:

- **None** — no AI influence on epistemic content  
- **Editorial** — language, clarity, or presentation without meaning change  
- **Analytical** — analysis, comparison, or evaluation contributing to conclusions  
- **Generative** — creation of novel content, hypotheses, or structures  
- **Decision-Critical** — AI output directly informed accepted decisions

These classifications describe *influence*, not capability.

---

### 5.3 Prompt Provenance (Without Content Disclosure)

For each epistemically relevant AI interaction, the artifact MUST disclose:

- the **intent** of the prompt (what was asked),
- the **role** of the prompt (e.g., drafting, critique, exploration, validation),
- the **model identity** (name and version, if known),
- the **linkage** between the AI interaction and the affected artifact or decision.

Raw prompt text is NOT required.

Prompt disclosure MUST be sufficient to characterize the nature of AI cognition without revealing proprietary or sensitive content.

---

### 5.4 Decision Attribution

Artifacts MUST explicitly identify:

- the **human decision owner**, and
- each **decision point** where AI input was considered.

For each decision point, the artifact MUST declare whether AI input was:

- **advisory** — considered but not relied upon,
- **comparative** — used to evaluate alternatives,
- **influential** — materially shaped reasoning,
- **determinative** — accepted with human approval.

AI systems SHALL NOT be identified as decision owners.

---

### 5.5 Epistemic Weight Classification

Each disclosed instance of AI influence MUST be assigned an **epistemic weight classification**, indicating its relative impact.

Permissible classifications include:

- cosmetic or editorial,
- conceptual exploration,
- analytical support,
- model or structure construction,
- hypothesis selection,
- parameter determination.

This classification enables proportional review and prevents both overstatement and minimization of AI influence.

---

### 5.6 Rejection and Non-Adoption Disclosure

Artifacts SHOULD disclose, at a summary level:

- materially considered AI-generated alternatives that were rejected,
- high-level human rationale for rejection.

Exhaustive logging is NOT required.

This disclosure supports falsifiability, auditability, and post-hoc understanding of epistemic paths not taken.

---

### 5.7 Completeness Requirement

Disclosure SHALL be considered incomplete if:

- any epistemically relevant AI influence is omitted,
- decision ownership is unclear,
- AI influence is described vaguely or euphemistically,
- AI is credited with autonomous reasoning or authority.

Incomplete disclosure constitutes non-compliance.

---

### 5.8 Disclosure Scope Limitation

NTS disclosure requirements do NOT extend to:

- internal model reasoning,
- chain-of-thought,
- proprietary system internals,
- full prompt transcripts,
- real-time logging of cognition.

Disclosure obligations end at epistemic influence visibility.

---

This section defines the mandatory disclosure elements required for NTS compliance once AI influence becomes epistemically relevant.

## 6. Attribution & Role Separation Requirements

This section defines the mandatory rules governing **attribution of cognition** and the separation of epistemic roles in NTS-compliant artifacts.

Attribution exists to ensure that epistemic responsibility is traceable, human-owned, and not conflated with tool behavior.

---

### 6.1 Attribution Requirement

Any cognition that crosses the cognitive influence threshold MUST be explicitly attributed.

Attribution MUST identify:
- the **epistemic role** under which the cognition occurred, and
- the **human decision owner** responsible for accepting its influence.

Attribution SHALL be explicit.  
Implicit, inferred, or retrospective attribution is not permitted.

---

### 6.2 Epistemic Roles

An **epistemic role** describes the functional capacity in which cognition is performed.

Common roles MAY include:
- drafting,
- synthesis,
- analysis,
- critique,
- validation,
- orchestration.

Roles describe **how cognition was used**, not who or what performed it.

---

### 6.3 Human Authority Invariant

NTS enforces the following invariant:

**Only humans may occupy epistemic authority roles.**

AI systems MAY support cognition but SHALL NOT:
- be listed as decision owners,
- be credited with epistemic authority,
- be described as having agency over claims or conclusions.

Any artifact violating this invariant is non-compliant.

---

### 6.4 Role Separation Requirement

Distinct epistemic roles MUST NOT be conflated.

Specifically:
- cognition generation,
- decision acceptance,
- and validation or approval

SHALL be attributed to distinct roles or explicitly distinct stages.

An artifact MUST make clear:
- where AI contributed,
- where humans decided,
- where validation occurred.

---

### 6.5 Prohibited Role Collapsing

The following practices SHALL be treated as non-compliance:

- attributing reasoning to “the model”,
- attributing decisions to automated systems,
- collapsing generation and validation into a single undisclosed step,
- implying that AI output is self-justifying.

Role collapsing obscures responsibility and violates epistemic transparency.

---

### 6.6 Multi-Stage Cognition

When cognition occurs across multiple stages, attribution MUST reflect:

- the sequence of roles,
- transitions between AI assistance and human decision-making,
- points at which influence was accepted or rejected.

Aggregation of stages is permitted only if it does not obscure epistemically significant transitions.

---

### 6.7 Attribution Sufficiency

Attribution SHALL be considered sufficient if a reviewer can determine:

- what role AI played,
- what role humans played,
- where responsibility lies for each claim.

If attribution does not allow this determination, it is insufficient.

---

### 6.8 Separation Without Enforcement

NTS defines attribution and role separation **normatively**.

It does not prescribe:
- workflow structure,
- tooling,
- enforcement mechanisms.

Downstream systems MAY enforce these requirements but MUST NOT reinterpret them.

---

This section defines how cognition must be attributed and separated to preserve epistemic accountability under NTS.

## 7. Provenance & Integrity Requirements
Defines requirements for preserving cognitive lineage.

## 8. Reconstruction & Re-evaluation Requirements
Defines reconstructibility standards for third-party review.

## 9. Independence & Validation Constraints
Defines separation between cognition, execution, and validation.

## 10. Non-Compliance Conditions
Defines conditions under which an artifact is not NTS-compliant.

## 11. Relationship to Downstream Systems
Clarifies interaction with ARI, AWO, and CRI-CORE.

## 12. Versioning & Change Control
Defines how changes to the NTS are governed.

## 13. Adoption Statement
Defines what it means to adopt NTS.

## 14. Limitations & Explicit Non-Goals
Prevents overreach and misinterpretation.

## 15. References & Citations
Authoritative references.

## Citation

### Human-Readable
Wright, Shawn C. (2025).  
**Neurotransparency Specification (NTS): Normative Disclosure Requirements for Cognitive Influence in AI–Human Systems.**  
Waveframe Labs · Governed under the Aurora Research Initiative (ARI).  
Version 2.0.0.  
DOI: TBD

### BibTeX
```bibtex
@misc{wright_neurotransparency_spec_2025,
  author       = {Wright, Shawn C.},
  title        = {Neurotransparency Specification (NTS): Normative Disclosure Requirements for Cognitive Influence in AI--Human Systems},
  year         = {2025},
  version      = {2.0.0},
  institution  = {Waveframe Labs},
  publisher    = {Aurora Research Initiative (ARI)},
  orcid        = {0009-0006-6043-9295},
  license      = {CC-BY-4.0},
  doi          = {TBD}
}
```
