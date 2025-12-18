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
Locks vocabulary used throughout the specification.

## 4. Cognitive Influence Threshold
Defines when cognition triggers disclosure obligations.

## 5. Disclosure Requirements
Defines mandatory disclosure elements once the threshold is met.

## 6. Attribution & Role Separation Requirements
Specifies how cognitive roles must be distinguished.

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
