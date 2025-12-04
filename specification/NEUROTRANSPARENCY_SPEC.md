---
filetype: specification
title: Neurotransparency Specification (NTS)
version: 1.1.0
release_date: 2025-12-03
maintainer: Waveframe Labs
contact: swright@waveframelabs.org
license: CC BY 4.0
related: Neurotransparency Doctrine v1.0.0; AWO v1.2.x; CRI-CORE v0.1+
orcid: 0009-0006-6043-9295
doi: (assigned upon publication)
---

# Neurotransparency Specification (NTS) v1.1.0
**Status:** Normative  
**Scope:** Cognitive Traceability Requirements for AI–Human Scientific Workflows  
**Authority:** Aurora Research Initiative (ARI)

---

# 1. Scope

This specification defines the normative requirements for **neurotransparency**: the mandatory conditions under which any reasoning step—human or synthetic—may influence a scientific claim within an AI–human research workflow.

NTS governs:

- the structure and minimal fields of a reasoning record,
- attribution rules for cognitive roles,
- evidence-linkage and dereferenceability requirements,
- hashing and integrity guarantees,
- attestation-independence constraints,
- ledger continuity and run-level conformance conditions.

This specification applies to all workflows operating under:

- **Aurora Workflow Orchestration (AWO)** governance,
- **CRI-CORE** enforcement systems,
- **ARI-aligned repositories**, releases, and scientific artifacts.

This document does **not** define philosophy, motivation, or interpretive guidance.  
It defines **strict, normative, testable rules** for admissible cognition in scientific processes.

---

# 2. Terminology

The following terms are normative for this specification.

### 2.1 Normative Keywords
The keywords **MUST**, **MUST NOT**, **SHALL**, **SHALL NOT**, **SHOULD**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

### 2.2 Reasoning Step
A transformation that introduces, modifies, evaluates, or interprets information in a manner that can influence a scientific claim.

### 2.3 Reasoning Record
The minimal admissible artifact representing a reasoning step, containing all required fields defined in Section 4.

### 2.4 Role
The declared epistemic identity under which a reasoning step is performed (e.g., Orchestrator, Auditor, Synthesizer, Validator). A reasoning step without a declared role is invalid.

### 2.5 Evidence Pointer
A dereferenceable reference to one or more artifacts that justify the reasoning step. A pointer MUST resolve to a stable artifact under hash verification.

### 2.6 Hash
A SHA-256 digest representing a reasoning record's exact content. A mismatch between the recorded hash and the computed hash constitutes a hash-integrity violation.

### 2.7 Ledger
The ordered, deterministic collection of all reasoning records for a workflow run, maintained by CRI-CORE.

### 2.8 Attestation
A validation action performed by a role other than the role that produced the reasoning step being validated.

### 2.9 Non-Conformance Event
Any violation of the rules defined in this specification. A non-conformance event invalidates the affected reasoning record and all dependent claims.

### 2.10 Run
A full execution cycle of an AWO-aligned workflow, producing a complete ledger and associated artifacts.

### 2.11 Claim
Any scientific statement, conclusion, or output whose epistemic validity depends on one or more reasoning records.

---

## 3. Normative Requirements for Neurotransparency

This section defines the mandatory requirements governing attribution, evidence-linkage, hashing, ledger continuity, attestation, and run-level conformance for any workflow producing, modifying, or approving **AI-influenced claims, analyses, or decisions**.  
All requirements in this section are normative and use the keywords SHALL, MUST, SHOULD, and MAY as defined in RFC 2119.

Neurotransparency compliance is satisfied only when **all** mandatory requirements are met within a single workflow run.

---

### 3.1 Attribution of Reasoning

**R3.1.1** — Every reasoning step influencing an AI-influenced claim, analysis, or decision SHALL declare the role under which the step is executed (e.g., Orchestrator, Auditor, Synthesizer, Validator, or other defined roles).

**R3.1.2** — Reasoning lacking explicit role attribution SHALL be treated as inadmissible and MUST NOT influence any downstream outcome.

**R3.1.3** — Role identifiers MUST be drawn from a predefined, version-controlled role registry to prevent ambiguity or aliasing.

**R3.1.4** — Any transformation that introduces, modifies, interprets, or evaluates information in a way that can influence an AI-influenced claim SHALL be considered a reasoning step and SHALL be attributed accordingly.

---

### 3.2 Evidence-Linkage Requirements

**R3.2.1** — Each reasoning step SHALL include one or more evidence pointers referencing the artifacts, inputs, or prior reasoning steps that justify the inference.

**R3.2.2** — Evidence pointers MUST be stable, versioned identifiers resolvable without external context.

**R3.2.3** — Ephemeral, session-dependent, or model-state-dependent evidence sources MUST NOT be used unless captured and serialized as durable artifacts within the same run.

**R3.2.4** — Reasoning lacking verifiable evidence-linkage SHALL be rejected prior to influencing any outcome.

---

### 3.3 Hash Integrity Requirements

**R3.3.1** — All reasoning outputs SHALL be hashed using SHA-256 unless superseded by a future mandatory algorithm specified in a later version of this standard.

**R3.3.2** — The resulting content hash SHALL be recorded in the project’s `SHA256SUMS.txt` file prior to the reasoning step being used by any downstream process.

**R3.3.3** — Any mismatch between a recorded hash and the computed hash of an artifact SHALL invalidate that artifact and all reasoning steps dependent upon it.

**R3.3.4** — Hashes MUST be computed after attribution and evidence-linkage fields are finalized to ensure complete content stability.

---

### 3.4 Ledger Construction and Continuity

**R3.4.1** — The workflow SHALL construct an append-only `reasoning_ledger` capturing all admissible reasoning steps in the order they occur.

**R3.4.2** — Each ledger entry SHALL contain:
- role identifier,  
- timestamp,  
- evidence pointers,  
- content hash,  
- deterministic reasoning identifier.

**R3.4.3** — The reasoning identifier MUST be derived deterministically from the artifact’s hash and the workflow run context.

**R3.4.4** — The ledger SHALL be treated as a normative, canonical record of cognitive provenance for the run.

**R3.4.5 (New — Hash-Chain Hardening)** — Each ledger entry SHOULD include the hash of the previous ledger entry.  
If implemented, any break in the hash-chain MUST be treated as a tamper-evident failure and SHALL invalidate the run.

---

### 3.5 Attestation Requirements (Separation of Duties)

**R3.5.1** — A role SHALL NOT attest to or approve reasoning that originates from the same role.

**R3.5.2** — Attestation independence SHALL be enforced at runtime, preventing circular or self-referential approval paths.

**R3.5.3** — Attestations SHALL be recorded in the ledger as separate cognitive events with their own role, timestamp, hash, and evidence pointer referencing the reasoning they validate.

**R3.5.4** — Any violation of attestation independence SHALL invalidate the attestation and the run.

---

### 3.6 Run-Level Conformance and Invalidity Propagation

**R3.6.1** — A run SHALL be considered conformant only if all mandatory requirements in Sections 3.1–3.5 are satisfied.

**R3.6.2** — If a reasoning record becomes invalid (e.g., missing evidence, hash mismatch, role ambiguity), all downstream reasoning steps that depend upon it SHALL be marked invalid.

**R3.6.3** — A workflow engine SHOULD halt immediately upon detection of an invalid reasoning step unless operating in diagnostic or audit-only mode.

**R3.6.4** — A run reaching a terminal invalid state MUST NOT produce or approve any AI-influenced claim, analysis, or decision.

---

### 3.7 Prohibitions

**R3.7.1** — Undocumented or implicit reasoning SHALL NOT be admissible, regardless of whether it originates from a human or synthetic agent.

**R3.7.2** — Model-internal, non-serialized, or non-reconstructible states SHALL NOT be used as evidence for any reasoning step unless captured and bound via hash within the same run.

**R3.7.3** — Any attempt to bypass hashing, ledgering, or attestation SHALL be treated as a non-conformance event.

**R3.7.4 (New — Recomputability Requirement)** — A reasoning step SHALL contain sufficient information to permit independent revalidation or recomputation without access to internal model states or transient cognition.

---

### 3.8 Minimal Epistemic Unit

**R3.8.1** — The minimal admissible unit of reasoning SHALL consist of:
- a role-attributed transformation,  
- one or more evidence pointers,  
- a deterministic output hash.

**R3.8.2** — Reasoning fragments lacking any of these components SHALL be considered metadata and MAY NOT influence any outcome.

**R3.8.3** — Aggregated reasoning steps SHALL NOT obscure internal cognitive transitions if those transitions alter the justification structure of any output.

---

These requirements establish the formal, enforceable conditions under which cognitive provenance is captured and validated in AI-human workflows.  
They provide the normative basis for CRI-CORE enforcement and SHALL govern all compliant systems beginning with NTS v1.1.0.

---  

# 4. Neurotransparency Data Model  
This section defines the **mandatory structural fields** that constitute a valid reasoning record.  
All fields defined herein are normative unless explicitly marked otherwise.

A reasoning record is the minimal serialized unit of cognitive provenance.  
CRI-CORE SHALL reject any record that does not conform to this data model.

---

## 4.1 Required Fields

### **4.1.1 `role` (string, REQUIRED)**  
The declared epistemic role responsible for producing the reasoning step.  
- MUST match an entry in the version-controlled role registry.  
- MUST be stable across versions.  
- Undeclared or ambiguous roles SHALL render the record invalid.

### **4.1.2 `evidence` (array of objects, REQUIRED)**  
A non-empty list of evidence pointers.  
Each entry MUST contain:  
- `path`: a resolvable, versioned artifact identifier  
- `sha256`: the expected SHA-256 hash of the referenced artifact  

Evidence entries MUST be dereferenceable without external context.  
Missing or malformed evidence entries SHALL invalidate the record.

### **4.1.3 `hash` (string, REQUIRED)**  
The SHA-256 digest of the reasoning record’s complete serialized content.  
- MUST match the corresponding entry in `SHA256SUMS.txt`.  
- MUST be computed only after `role` and `evidence` fields are finalized.

### **4.1.4 `timestamp` (string, REQUIRED)**  
An ISO-8601 timestamp marking when the reasoning record was finalized.  
- Timestamps MUST be monotonic within a run.  
- Timestamps MAY NOT be modified after hashing.

### **4.1.5 `id` (string, REQUIRED)**  
The deterministic identifier for the reasoning record, generated by CRI-CORE.  
- MUST be computed as a deterministic function of:  
  - the record’s `hash`,  
  - the run identifier,  
  - and the prior ledger state (if hash-chaining is implemented).  
- Collisions SHALL be treated as non-conformance events.

---

## 4.2 Optional Fields

### **4.2.1 `metadata` (object, OPTIONAL)**  
Non-epistemic supplementary information.  
Metadata MUST NOT influence claim validity and MUST NOT be treated as evidence.

---

## 4.3 Serialization Requirements

**R4.3.1** — Records MUST be serialized to canonical JSON prior to hashing.  
**R4.3.2** — Field ordering MUST follow the sequence defined in Section 4.1.  
**R4.3.3** — Additional fields not defined in this specification SHALL be ignored by validators but MUST cause a warning.  
**R4.3.4** — Whitespace and formatting MUST NOT affect the hash.  
Canonical serialization rules MUST be used.

---

## 4.4 Example Record (Non-Normative)

```json
{
  "role": "Synthesizer",
  "evidence": [
    {
      "path": "docs/source_claims/claim_001.md",
      "sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e..."
    }
  ],
  "hash": "9f1c7e2a6d7bc3df4c1fd874897ce0cd59eafce...",
  "timestamp": "2025-12-03T18:22:41Z",
  "id": "nts-run123-rec-0007",
  "metadata": {
    "note": "Optional explanatory annotation; non-epistemic."
  }
}
```  
This example is illustrative only and does not impose any normative constraints.  

---

# 5. Minimal Reasoning Unit Specification

This section defines the **minimal epistemic unit** required for neurotransparency compliance.  
A minimal reasoning unit (MRU) is the smallest admissible artifact that may influence an AI-influenced claim, analysis, or decision within an AWO/CRI-CORE governed workflow.

Any transformation that fails to meet the requirements in this section SHALL be treated as metadata and MUST NOT influence any downstream epistemic outcome.

---

## 5.1 Definition

A **Minimal Reasoning Unit (MRU)** is a role-attributed, evidence-linked, hash-bound reasoning artifact complying with the data model and invariants defined in Sections 3 and 4.

An MRU MUST satisfy all requirements in this section to be admissible.

---

## 5.2 Mandatory Components of an MRU

### **5.2.1 Role Attribution (REQUIRED)**
An MRU MUST include a `role` field that:
- is explicitly declared,
- matches a valid entry in the role registry,
- is stable and versioned.

Reasoning lacking explicit role attribution SHALL be treated as inadmissible.

### **5.2.2 Evidence Pointer Set (REQUIRED)**
An MRU MUST contain a non-empty `evidence` array referencing stable, hash-verifiable artifacts.

Each evidence entry MUST contain:
- `path` (resolvable artifact identifier),
- `sha256` (expected hash of the referenced artifact).

Absence, ambiguity, or non-dereferenceability of evidence SHALL invalidate the MRU.

### **5.2.3 Deterministic Output Hash (REQUIRED)**
The MRU MUST include a `hash` field representing the SHA-256 digest of the fully serialized MRU.

A mismatch between the stored hash and the recomputed hash SHALL invalidate the MRU.

### **5.2.4 Timestamp (REQUIRED)**
The MRU MUST include a `timestamp` field:
- in ISO-8601 format,
- finalized prior to hashing,
- strictly monotonic within a given run.

### **5.2.5 Deterministic Reasoning Identifier (REQUIRED)**
The MRU MUST include an `id` field generated deterministically from:
- the MRU’s own hash,
- the workflow run identifier,
- (optionally) the previous ledger entry’s hash, if hash-chaining is implemented.

Identifiers MUST be collision-resistant; collisions SHALL trigger non-conformance.

---

## 5.3 Stability Requirements

### **5.3.1 Content Stability**
No field within an MRU may change after hashing.  
Any post-hash modification SHALL be treated as a hash-integrity violation.

### **5.3.2 Serialization Stability**
MRUs MUST be serialized using canonical JSON per Section 4.3.  
Differences in whitespace or formatting MUST NOT produce different hashes.

### **5.3.3 Evidence Stability**
Evidence artifacts referenced by an MRU MUST remain unchanged for the duration of the run.  
If any referenced artifact changes, all dependent MRUs SHALL be invalidated.

---

## 5.4 Boundary Conditions

### **5.4.1 Notational Metadata**
Comments, annotations, or non-epistemic metadata MUST NOT influence the MRU’s epistemic role.

### **5.4.2 Multi-Step Transformations**
Complex outputs MAY be decomposed into multiple MRUs.  
Aggregation MUST NOT obscure internal cognitive transitions if such transitions alter epistemic justification.

### **5.4.3 Non-Epistemic Operations**
Formatting, ordering, cosmetic edits, and other non-epistemic transformations MUST NOT produce MRUs.

Only transformations that alter the justification structure of a claim MAY be serialized as MRUs.

---

## 5.5 Admissibility Rules

### **5.5.1 Mandatory Inclusion**
If a transformation alters epistemic content, an MRU MUST be produced.

### **5.5.2 Prohibited Omissions**
Silent reasoning (human or synthetic) SHALL NOT be admissible.

### **5.5.3 Epistemic Invalidity Propagation**
If an MRU becomes invalid, all dependent MRUs SHALL inherit its invalidity.

---

## 5.6 Minimality Constraint

An MRU MUST contain exactly the fields required in Section 4.  
Additional fields:
- MAY be included only as optional metadata,
- MUST NOT alter epistemic content,
- MUST NOT affect the validity or hash of mandatory fields.

An artifact containing fewer fields than required SHALL NOT be considered a reasoning unit.  
An artifact containing additional epistemically-meaningful fields SHALL be considered an improperly structured reasoning unit and SHALL be rejected.

---

This section defines the enforceable minimal unit of cognitive provenance in AWO/CRI-CORE governed workflows.

---

# 6. Evidence-Linkage Requirements

This section defines the normative rules governing the structure, stability, dereferenceability, and validity of evidence pointers within any neurotransparency-compliant workflow.  
Evidence-linkage is a structural invariant: no reasoning step SHALL be admissible unless its evidence pointers satisfy all requirements in this section.

---

## 6.1 Evidence Pointer Definition

An **evidence pointer** is a dereferenceable, hash-verifiable reference to an artifact used to justify a reasoning step.  
Evidence pointers MUST be represented as objects containing at minimum:

- `path`: a stable, resolvable artifact identifier,
- `sha256`: the expected content hash of the referenced artifact.

Any pointer lacking one or more required fields SHALL be treated as malformed and MUST invalidate the corresponding reasoning unit.

---

## 6.2 Mandatory Evidence-Linkage

### **6.2.1 Required Evidence Set**
Every admissible reasoning unit MUST include one or more evidence pointers.  
A reasoning unit with an empty or missing evidence set SHALL be rejected.

### **6.2.2 Stable Referencing**
Evidence pointers MUST reference stable, versioned artifacts.  
Paths SHALL NOT depend on:
- ephemeral context windows,
- model-internal states,
- transient runtime caches,
- platform-specific temporary files.

### **6.2.3 Hash Verification Requirement**
For each evidence pointer, the referenced artifact’s SHA-256 digest MUST match the value recorded in the pointer.  
If the digest does not match, the evidence pointer SHALL be treated as invalid and MUST invalidate the reasoning unit.

### **6.2.4 Local Availability Requirement**
All referenced evidence artifacts MUST be available within the same workflow run.  
External or remote dependencies MUST be serialized and hashed as part of the run.

---

## 6.3 Dereferenceability and Resolution

### **6.3.1 Guaranteed Resolution**
Evidence pointers MUST resolve deterministically and without requiring:
- additional credentials,
- online services,
- model-dependent reasoning,
- or external reinterpretation.

### **6.3.2 Non-Resolvable Evidence**
If an evidence pointer cannot be resolved at validation time:
- the pointer SHALL be marked invalid,
- the reasoning unit SHALL be marked invalid,
- all dependent reasoning units SHALL also be invalidated.

### **6.3.3 Interpretation-Free Resolution**
Evidence pointers MUST NOT require interpretive or heuristic lookup.  
Resolution MUST be exact, mechanical, and deterministic.

---

## 6.4 Ephemeral and Model-State Evidence

### **6.4.1 Ephemeral Evidence Prohibition**
Evidence that depends on volatile model states, temporary contexts, or non-serialized cognition SHALL NOT be admissible unless captured and serialized as a stable artifact within the run.

### **6.4.2 Serialization Requirement**
If evidence originates from a model’s internal state, the workflow MUST serialize:
- the content,
- its hash,
- and any structural metadata required for reconstruction.

Unserialized model-state evidence SHALL be treated as absent evidence.

---

## 6.5 Evidence Integrity and Preservation

### **6.5.1 Immutability**
Referenced evidence artifacts MUST remain unchanged for the duration of the run.  
Any mutation SHALL invalidate all reasoning units that reference the mutated artifact.

### **6.5.2 Ledger Binding**
Evidence pointers MUST be included in the serialized reasoning record and SHALL be part of the ledger entry for that reasoning unit.

### **6.5.3 Forward Evidence Continuity**
If a reasoning unit references a prior reasoning unit as evidence, the entire chain MUST remain hash-consistent.  
A break in any link SHALL invalidate all downstream dependencies.

---

## 6.6 Compound Evidence Structures

### **6.6.1 Multi-Evidence Requirement**
Reasoning units MAY reference multiple evidence artifacts.  
If multiple pointers are present, each pointer MUST independently satisfy all requirements in this section.

### **6.6.2 Evidence Sets MUST NOT be Aggregated Loosely**
Loose aggregation (e.g., lists of evidence without per-item hashes) SHALL NOT be admissible.  
Each evidence element MUST be explicitly identified and hash-verified.

### **6.6.3 Evidence Normalization**
Evidence pointers MUST be serialized using canonical JSON to ensure hashing consistency and prevent aliasing.

---

## 6.7 Evidence Validity and Failure Modes

The following conditions SHALL invalidate a reasoning unit:

- **missing evidence pointers**,  
- **empty evidence list**,  
- **non-resolvable evidence path**,  
- **hash mismatch**,  
- **ephemeral evidence lacking serialization**,  
- **evidence dependent on non-deterministic states**,  
- **changes to referenced artifacts**,  
- **pointer aliasing or ambiguity**.

When any invalid evidence condition is detected, all dependent reasoning units SHALL inherit invalidity.

---

## 6.8 Evidence-Linkage and Claim Validity

No claim, analysis, or decision MAY be approved within a workflow unless every supporting reasoning unit includes complete, valid, and hash-verifiable evidence pointers.

A claim supported by any non-conformant evidence SHALL be considered epistemically invalid for that workflow run.

---

This section defines the enforceable structural rules for evidence-linkage under NTS v1.1.0 and forms the basis for CRI-CORE evidence validation.

---

# 7. Role Attribution Requirements

This section defines the mandatory rules governing epistemic role attribution for all reasoning units within neurotransparency-compliant workflows.  
A reasoning unit SHALL NOT be admissible unless all requirements in this section are met.

---

## 7.1 Role Definition and Registry

### **7.1.1 Role Registry Requirement**
A workflow SHALL maintain a version-controlled **Role Registry** enumerating all valid epistemic roles (e.g., Orchestrator, Auditor, Synthesizer, Validator).

### **7.1.2 Registry Stability**
Roles in the registry MUST be stable for the duration of a run.  
A role SHALL NOT be added, removed, or modified mid-run.

### **7.1.3 Role Identifier Format**
Role identifiers MUST be:
- unambiguous,
- unique,
- canonicalized (e.g., uppercase snake case),
- serializable in canonical JSON.

Aliases, abbreviations, or free-form role identifiers SHALL NOT be admissible.

---

## 7.2 Mandatory Role Attribution for Reasoning

### **7.2.1 Required Role Field**
Each reasoning unit MUST declare a `role` field matching an entry in the Role Registry.

### **7.2.2 Non-Attributed Reasoning**
A reasoning unit lacking a role field SHALL be invalid.  
Reasoning without a role MUST NOT influence any claim, analysis, or decision.

### **7.2.3 Unrecognized Roles**
If a reasoning unit declares a role not present in the Role Registry, the unit SHALL be invalid and MUST invalidate all dependent reasoning.

### **7.2.4 Internal Reasoning Visibility**
Any cognitive transformation performed by a role—human or synthetic—MUST be captured as a reasoning unit if it affects epistemic justification.

Internal cognition without explicit role attribution SHALL NOT be admissible.

---

## 7.3 Role Semantics and Accountability

### **7.3.1 Role Ownership**
The role declared on a reasoning unit MUST be the epistemic agent responsible for producing the reasoning content.

### **7.3.2 Role Accountability**
A role MUST NOT:
- attribute reasoning to another role,
- manipulate role identifiers,
- or perform reasoning while omitting its role attribution.

Any such behavior SHALL be treated as a non-conformance event.

---

## 7.4 Separation of Duties

### **7.4.1 Attestation Independence**
Roles performing attestations MUST NOT perform the reasoning they validate.  
(See Section 9.)

### **7.4.2 Multi-Role Prohibition**
A single reasoning unit MUST NOT declare multiple roles.  
Reasoning requiring multi-role collaboration SHALL be represented as discrete units.

### **7.4.3 Role Cross-Contamination**
A role SHALL NOT act in two epistemic capacities within the same reasoning unit (e.g., Orchestrator + Validator).  
Any such record SHALL be invalid.

---

## 7.5 Role Transition and Continuity

### **7.5.1 Role Stability Within a Run**
A role MAY produce multiple reasoning units across a run, but the meaning of that role MUST remain constant.

### **7.5.2 Transient Roles**
Transient or context-derived roles SHALL NOT be allowed.  
All roles MUST be explicitly defined in the Role Registry prior to run initialization.

### **7.5.3 Role Retirement**
If a role becomes deprecated, it MUST remain valid for ledger reconstruction but MUST NOT be used in new reasoning units beyond the deprecation point.

---

## 7.6 Role Metadata and Provenance

### **7.6.1 Required Metadata Block**
A reasoning unit MAY include optional metadata (e.g., version, environment, configuration), but the metadata MUST NOT substitute for the required role field.

### **7.6.2 Provenance Binding**
Role attribution MUST be included in:
- the reasoning record,
- its hash,
- the ledger entry,
- and the project’s `SHA256SUMS.txt`.

### **7.6.3 Inference Equivalence**
A role MUST NOT depend on unstated attributes (author identity, platform, model version) to infer role meaning.  
Role semantics MUST be explicit.

---

## 7.7 Failure Modes and Invalidity Conditions

The following conditions SHALL invalidate a reasoning unit:

- missing role field,  
- role not present in the Role Registry,  
- multiple roles declared for a single unit,  
- role ambiguity (e.g., conflicting metadata),  
- role mutation mid-run,  
- role inferred but not explicitly declared,  
- transient or emergent roles,  
- role attempting to perform both reasoning and attestation for the same unit.

Invalid role attribution SHALL propagate invalidity to all dependent reasoning units.

---

## 7.8 Requirements for CRI-CORE Enforcement

CRI-CORE MUST enforce:

- schema-level validation of the `role` field,  
- cross-checking role identifiers against the Role Registry,  
- rejection of ambiguous or missing role fields,  
- prevention of role misuse (self-attestation, multi-role contamination),  
- deterministic replay of role attribution during ledger reconstruction.

---

This section defines the full normative role-attribution rules for NTS v1.1.0 and forms the epistemic accountability layer for all compliant systems.

---

# 8. Hash Integrity Requirements

This section defines the mandatory rules governing hashing, integrity verification, and tamper-evidence for all reasoning units produced within a neurotransparency-compliant workflow.  
Hash integrity is a foundational invariant: any violation SHALL invalidate the affected reasoning unit and all dependent claims, analyses, or decisions.

---

## 8.1 Hash Algorithm Requirements

### **8.1.1 Mandatory Algorithm**
All reasoning units SHALL be hashed using **SHA-256** unless superseded by a future mandatory algorithm defined in a subsequent version of this specification.

### **8.1.2 Algorithm Stability**
The hashing algorithm MUST remain constant within a run.  
Algorithm changes mid-run SHALL be prohibited.

### **8.1.3 Future Algorithm Migration**
If SHA-256 is superseded in a future version, migration MUST:
- occur only at a new version boundary,
- be explicitly declared in the Specification,
- preserve backward-compatibility for ledger reconstruction.

---

## 8.2 Hash Scope and Content Inclusion

### **8.2.1 Full-Content Hashing**
The hash MUST be computed over the **exact canonical serialization** of the reasoning unit, including:
- `role`,
- `evidence`,
- `timestamp`,
- `metadata` (if present),
- `id` (if pre-assigned),
- all normative fields.

### **8.2.2 Post-Finalization Hashing**
The hash MUST be computed **after** all required fields have been finalized.  
Hashing partial or pre-attribution content SHALL be invalid.

### **8.2.3 Stable Serialization Format**
The workflow SHALL use a deterministic, canonical serialization format (e.g., canonical JSON).  
Any non-determinism in ordering, whitespace, or encoding SHALL invalidate hash reproducibility.

### **8.2.4 Metadata Inclusion**
Optional metadata MUST be included in the hash to prevent silent mutation.  
Metadata MAY be omitted only if omitted entirely.

---

## 8.3 Hash Recording Requirements

### **8.3.1 SHA256SUMS Inclusion**
Each reasoning unit’s hash MUST be recorded in the project’s `SHA256SUMS.txt` file prior to any downstream use.

### **8.3.2 Exact Matching Requirement**
The recorded hash MUST match the computed hash **exactly**, including case and formatting.

### **8.3.3 One-Hash–One-Artifact Rule**
Each artifact MUST correspond to exactly one hash entry.  
Duplicate hash entries SHALL NOT be permitted.

### **8.3.4 Missing Hash Entries**
Any reasoning unit lacking a hash entry in `SHA256SUMS.txt` SHALL be invalid.

---

## 8.4 Hash Verification and Mutation Detection

### **8.4.1 Verification Timing**
Hash verification MUST occur:
- before attestation,
- before inclusion in the ledger,
- before any use in a claim, analysis, or decision.

### **8.4.2 Mutation Detection**
If the computed hash of an artifact differs from its recorded hash, the artifact SHALL be considered mutated and therefore invalid.

### **8.4.3 Immutable Artifact Rule**
Once hashed and recorded, the artifact MUST NOT be modified.  
Any post-hash modification SHALL trigger an invalidity cascade.

### **8.4.4 Hash Reproducibility Requirement**
A hash MUST be reproducible across:
- independent verifiers,
- different machines,
- different implementations of the hashing algorithm.

---

## 8.5 Ledger and Hash Continuity

### **8.5.1 Ledger Hash Inclusion**
Each ledger entry SHALL include the reasoning unit’s content hash.

### **8.5.2 Hash-Chain Continuity (Recommended)**
A ledger entry SHOULD include the previous ledger entry’s hash.  
If implemented, any break in chain continuity SHALL invalidate the run.

### **8.5.3 Append-Only Guarantee**
Hash-bound ledger entries MUST be append-only and SHALL NOT be retroactively modified.

---

## 8.6 Forbidden Hash Practices

### **8.6.1 Hashing of Partial Artifacts**
Hashing incomplete or pre-finalized artifacts SHALL be prohibited.

### **8.6.2 Hashing of Implicit Inputs**
Implicit model states, cached variables, or internal contexts SHALL NOT be hashed unless serialized as durable artifacts.

### **8.6.3 Post-Hoc Hash Patching**
Altering an artifact to match an earlier hash SHALL be treated as tampering.

### **8.6.4 Hashing of Unattributed Reasoning**
Reasoning lacking a valid role SHALL NOT be hashed or included in the ledger.

### **8.6.5 Out-of-Band Hashes**
Hashes recorded outside `SHA256SUMS.txt` SHALL NOT be considered authoritative.

---

## 8.7 CRI-CORE Enforcement Requirements

CRI-CORE MUST enforce:

- deterministic serialization before hashing,
- hash verification prior to ledger insertion,
- immediate run invalidation upon hash mismatch,
- immutability of hashed artifacts,
- correct ordering of hash computation (post-attribution, post-evidence-linkage),
- canonical construction of the tamper-evident ledger,
- hash reproducibility during replay or revalidation.

---

## 8.8 Invalidity Conditions

A reasoning unit SHALL be marked invalid if any of the following occur:

- missing hash,
- mismatch between recorded and computed hash,
- multiple hashes for one artifact,
- hash mutation,
- non-deterministic serialization,
- hashing performed before mandatory fields are finalized,
- modification after hashing,
- incorrect registry location (not in `SHA256SUMS.txt`).

Invalidity MUST propagate to all downstream reasoning units.

---

This section defines the full normative hashing requirements for NTS v1.1.0 and forms the integrity foundation for CRI-CORE enforcement.

---

# 9. Attestation Independence Requirements

Attestation independence is a mandatory epistemic and procedural constraint in neurotransparency-compliant workflows.  
No reasoning unit may influence any claim, analysis, or decision unless it has been validated by a role **independent** from the role that produced it.  
These rules SHALL be enforced deterministically by CRI-CORE.

---

## 9.1 Separation-of-Duties (SoD) Constraint

### **9.1.1 Mandatory Separation**
The role that produces a reasoning unit (the “originating role”) SHALL NOT validate, approve, or attest to that unit under any circumstances.

### **9.1.2 Cyclical Dependency Prohibition**
No pair or group of roles MAY form a circular approval chain  
(e.g., A validates B and B validates A).  
Such cycles SHALL be treated as violations of attestation independence.

### **9.1.3 Hierarchical Integrity**
Supervisory or “meta” roles MUST adhere to the same separation requirements.  
A supervising role SHALL NOT attest to the reasoning outputs of a role it directly governs if doing so bypasses independence.

---

## 9.2 Attestation Structure and Content Requirements

### **9.2.1 Required Fields**
Each attestation event SHALL be represented as a reasoning unit with:
- `role` (attesting role),
- `evidence` (pointer to the reasoning unit being attested),
- `timestamp`,
- `hash`,
- `id`,
- any additional metadata required by the neurotransparency data model.

### **9.2.2 Attestation as a First-Class Cognitive Event**
An attestation SHALL itself be treated as a reasoning step and MUST be:
- hashed,
- recorded in the ledger,
- included in `SHA256SUMS.txt`,
- subject to all hashing, evidence-linkage, and attribution rules.

### **9.2.3 Single-Scope Attestation**
An attestation MUST refer to exactly one reasoning unit unless explicitly allowed by a future version of this Specification.  
Batch attestations SHALL be prohibited.

---

## 9.3 Validation Requirements

### **9.3.1 Role Independence Verification**
CRI-CORE SHALL validate that the attesting role is different from the originating role.  
Validation MUST fail if roles are identical.

### **9.3.2 Evidence Dereferenceability**
The attestation MUST contain a valid pointer to the exact reasoning unit being validated.  
Broken, ambiguous, or non-dereferenceable pointers SHALL render the attestation invalid.

### **9.3.3 Hash Pre-Validation**
Before any attestation is accepted:
- the referenced reasoning unit’s hash MUST be verified,
- the attestation’s own hash MUST be verified.

### **9.3.4 Ledger Ordering**
The attestation MUST appear in the ledger **after** the reasoning unit it validates.  
Out-of-order attestations SHALL be rejected.

---

## 9.4 Prohibitions

### **9.4.1 Self-Attestation**
A role SHALL NOT attest to its own reasoning.

### **9.4.2 Transitive Self-Attestation (Indirect Self-Attestation)**
A role SHALL NOT attest to a reasoning unit that is downstream of one of its own earlier un-attested reasoning units.

### **9.4.3 Implicit or Undeclared Attestations**
Validation actions performed outside the explicit attestation mechanism SHALL be prohibited.

### **9.4.4 Attestation After Context Expiry**
An attestation referencing reasoning that cannot be fully reconstructed under the current workflow context SHALL be treated as invalid.

---

## 9.5 Invalidity Handling

### **9.5.1 Invalid Attestation Invalidation**
An attestation that fails independence or structural requirements SHALL be invalid.

### **9.5.2 Downstream Invalidation**
A reasoning unit that depends on an invalid attestation SHALL itself be marked invalid.

### **9.5.3 Run-Level Invalidity**
If an attestation independence violation occurs and cannot be resolved:
- the run SHALL enter a non-conformance state,
- the workflow MUST halt unless in audit mode,
- no claims, analyses, or decisions SHALL be produced.

---

## 9.6 CRI-CORE Enforcement Rules

CRI-CORE MUST enforce:

1. **Identity Check:** attesting role != originating role.  
2. **Hash Validation:** both the attested unit and the attestation must pass hash verification.  
3. **Evidence Pointer Verification:** dereferenceability and correctness.  
4. **Ordering Rule:** attestation must follow reasoning unit in the ledger.  
5. **Independence Graph:** no cycles, no indirect self-attestation, no delegation loops.  
6. **Ledger Consistency:** attestation must be append-only and immutable.  
7. **Context Validity:** attestation must reference reconstructible cognitive state.

Failure of any check SHALL invalidate the attestation, the dependent reasoning units, and potentially the entire run.

---

## 9.7 Minimal Attestation Unit

A minimal valid attestation SHALL consist of:
- a role distinct from the originating role,
- a dereferenceable pointer to the reasoning unit being validated,
- a timestamp,
- a hash,
- a deterministic identifier,
- canonical serialization under the data model.

This represents the irreducible, admissible form of an attestation event.

---

This section defines the strict normative conditions required to maintain epistemic independence and prevent circular or self-referential validation within AI–human workflows.  
CRI-CORE SHALL enforce all mandatory requirements beginning with NTS v1.1.0.

---

# 10. Run-Level Compliance Rules

A workflow run is the atomic unit of epistemic validity under the Neurotransparency Specification.  
A run is conformant only if **all** mandatory requirements in Sections 3–9 are met, all reasoning units are valid, and the ledger remains complete, ordered, and intact.  
CRI-CORE SHALL evaluate run-level conformance deterministically.

---

## 10.1 Definition of a Conformant Run

### **10.1.1 Mandatory Global Validity**
A run SHALL be considered conformant only when:
- all reasoning records pass attribution, evidence-linkage, and hash requirements,
- all attestations satisfy independence constraints,
- the ledger is complete, ordered, and non-tampered,
- no unresolved non-conformance events exist.

### **10.1.2 Completeness Requirement**
A run MUST produce:
- a complete `reasoning_ledger`,
- a complete and exact `SHA256SUMS.txt`,
- all required artifacts defined by the workflow’s operational specification.

Missing or partial artifacts SHALL mark the run as non-conformant.

### **10.1.3 Deterministic Reconstructibility**
A run SHALL be considered valid only if its outputs (claims, analyses, decisions) can be reproduced or independently revalidated from:
- the ledger,
- its evidence pointers,
- serialized artifacts,
- hash records.

If reconstructibility is not possible, the run is invalid.

---

## 10.2 Conditions for Invalidity

A run SHALL be considered invalid if **any** of the following conditions occur:

### **10.2.1 Hash Continuity Failure**
A mismatch, absence, or mutation of any hash in `SHA256SUMS.txt`.

### **10.2.2 Ledger Inconsistency**
If the ledger is:
- out of order,
- missing required entries,
- contains unauthorized deletions,
- exhibits breaks in hash-chain continuity (when implemented).

### **10.2.3 Evidence-Linkage Failure**
Any reasoning record without dereferenceable evidence pointers SHALL invalidate the run.

### **10.2.4 Role Ambiguity**
Any reasoning event lacking a valid role identifier SHALL invalidate the run.

### **10.2.5 Self-Attestation or Circular Attestation**
Any violation of attestation independence SHALL mark the run invalid.

### **10.2.6 Context Drift**
If a reasoning record relies on ephemeral or expired context state that cannot be reconstructed, the run is invalid.

### **10.2.7 Schema Non-Conformance**
Any reasoning record failing validation against the data model or schema SHALL invalidate the run.

---

## 10.3 Run Termination and Handling of Invalid States

### **10.3.1 Immediate Halt Requirement**
Upon encountering a non-conformance event (unless operating in audit or diagnostic mode):
- the workflow engine MUST halt execution,
- no claims, outputs, analyses, or decisions SHALL be finalized.

### **10.3.2 Non-Production of Outputs**
An invalid run MUST NOT produce:
- scientific claims,
- research findings,
- policy recommendations,
- analysis results,
- or any artifact that can be misinterpreted as a valid output.

### **10.3.3 Diagnostic Mode Exception**
If a workflow is explicitly operating in diagnostic or audit-only mode:
- it MAY continue execution for analysis,
- but MUST NOT output or publish results.

The run SHALL still be classified as invalid.

---

## 10.4 Invalidation Propagation Rules

### **10.4.1 Downstream Dependency Rule**
If a reasoning unit is invalid:
- all reasoning units that transitively depend on it SHALL be marked invalid,
- all claims derived from it SHALL be invalid.

### **10.4.2 Ledger-Wide Status Update**
CRI-CORE SHALL propagate invalidity through the ledger, marking all affected entries.

### **10.4.3 No Partial Validity**
A run MAY NOT be partially valid.  
If any mandatory requirement is violated, the entire run is invalid.

---

## 10.5 Run Completion Requirements

### **10.5.1 Canonical Finalization**
A conformant run MUST produce:
- a finalized ledger,
- a finalized `SHA256SUMS.txt`,
- all serialized reasoning artifacts,
- attestation and validation records.

### **10.5.2 Immutability Requirement**
Upon completion, all run artifacts SHALL become immutable.  
Post-run modifications SHALL be prohibited and detectable by hash mismatch.

### **10.5.3 Archival Requirement**
A conformant run SHALL be archived under the workflow’s archival policy and MUST be preserved indefinitely.

---

## 10.6 CRI-CORE Enforcement Rules

CRI-CORE SHALL enforce the following:

1. **Complete validation of every reasoning unit**  
   (role, evidence, hash, schema, timestamp, ID).

2. **Construction of a deterministic ledger**, with no gaps or reordering.

3. **Hash-chain verification** (if implemented).

4. **Detection of independent, indirect, and cyclic attestation violations**.

5. **Run termination upon invalidity**, unless diagnostic mode is declared.

6. **Ensuring reconstructibility** of all claims or outputs.

7. **Immutability and archival** of valid runs.

Failure to enforce any of these invariants SHALL itself constitute a non-conformance event.

---

These rules define the conditions under which entire workflow runs are considered valid, invalid, or diagnostically permissible.  
Strict run-level conformance is mandatory for all NTS v1.1.0–aligned systems.

---

# 11. Non-Conformance Conditions

A **non-conformance event** is any violation of the Neurotransparency Specification that renders a reasoning record, an attestation, a ledger, or an entire workflow run epistemically invalid.  
This section enumerates all conditions that SHALL trigger non-conformance.  
Unless explicitly stated otherwise, any non-conformance event invalidates the affected reasoning record and all downstream reasoning and SHALL cause the run to terminate per Section 10.

---

## 11.1 Attribution Violations

**NC-11.1.1 — Missing Role Attribution**  
A reasoning record lacking a declared role SHALL be non-conformant.

**NC-11.1.2 — Invalid or Undefined Role Identifier**  
A role not present in the version-controlled role registry SHALL invalidate the record.

**NC-11.1.3 — Role Ambiguity**  
If the role cannot be unambiguously resolved, the reasoning step is invalid.

---

## 11.2 Evidence-Linkage Violations

**NC-11.2.1 — Missing Evidence Pointer**  
A reasoning record without at least one dereferenceable evidence pointer SHALL be invalid.

**NC-11.2.2 — Broken Evidence Pointer**  
If the pointer cannot be resolved to a stable, versioned artifact, the reasoning step is invalid.

**NC-11.2.3 — Ephemeral Evidence Source**  
Use of unsaved model state, session state, or transient human reasoning without serialization SHALL invalidate the reasoning step.

**NC-11.2.4 — Circular Evidence Dependencies**  
Evidence chains forming a cycle (A → B → A) SHALL be invalid.

---

## 11.3 Hash Integrity Violations

**NC-11.3.1 — Missing Hash**  
Any reasoning record lacking a SHA-256 hash SHALL be invalid.

**NC-11.3.2 — Hash Mismatch**  
A mismatch between computed and recorded hash constitutes an integrity failure and SHALL invalidate the record and all dependent records.

**NC-11.3.3 — Hash Omission in `SHA256SUMS.txt`**  
If a reasoning artifact is missing from the canonical hash manifest, the reasoning step is invalid.

**NC-11.3.4 — Post-Hash Mutation**  
Any modification after hashing SHALL invalidate the artifact.

**NC-11.3.5 — Hash-Chain Discontinuity**  
If implemented, any break in hash-chain continuity SHALL be treated as tampering and SHALL invalidate the run.

---

## 11.4 Ledger Violations

**NC-11.4.1 — Missing Ledger Entry**  
Any reasoning step absent from the ledger is invalid.

**NC-11.4.2 — Ledger Reordering or Gap**  
Non-sequential ordering or missing indices SHALL invalidate the ledger.

**NC-11.4.3 — Unauthorized Ledger Modification**  
Any deletion, mutation, or post-hoc edit to the ledger SHALL invalidate the run.

**NC-11.4.4 — Non-Deterministic Reasoning Identifier**  
If an entry’s ID cannot be recomputed deterministically from the hash and workflow state, the record is invalid.

---

## 11.5 Attestation Violations

**NC-11.5.1 — Self-Attestation**  
A role validating its own reasoning step SHALL invalidate both the attestation and the run.

**NC-11.5.2 — Circular Attestation**  
Reciprocal validation (A attests B; B attests A) SHALL invalidate the run.

**NC-11.5.3 — Missing Attestation Record**  
If a required attestation is absent from the ledger, the reasoning step is invalid.

**NC-11.5.4 — Attestation Without Evidence**  
An attestation lacking a pointer to the reasoning it validates SHALL be invalid.

---

## 11.6 Schema and Data Model Violations

**NC-11.6.1 — Schema Non-Compliance**  
Any record failing validation against the Neurotransparency Data Model SHALL be invalid.

**NC-11.6.2 — Missing Required Fields**  
Absence of any required field (`role`, `evidence`, `hash`, `timestamp`, `id`) SHALL invalidate the record.

**NC-11.6.3 — Non-Canonical Field Types**  
Improper datatypes (e.g., timestamp not ISO8601) SHALL invalidate the record.

---

## 11.7 Context and State Violations

**NC-11.7.1 — Context Drift**  
If the cognitive context necessary for reconstructing a reasoning step is not available or serialized within the run, the record is invalid.

**NC-11.7.2 — Model Version Instability**  
If the model version producing a reasoning step cannot be confirmed, the step is invalid.

**NC-11.7.3 — Non-Reconstructible Cognitive State**  
Any reasoning dependent on transient internal model states not preserved in the run SHALL be invalid.

---

## 11.8 Minimal Reasoning Unit Violations

**NC-11.8.1 — Missing Role, Evidence, or Hash**  
A reasoning record lacking any component of the minimal epistemic unit SHALL be invalid.

**NC-11.8.2 — Aggregation Obscuring Internal Transitions**  
If reasoning steps are combined in a way that hides epistemically significant transformations, the record is invalid.

---

## 11.9 Prohibited Reasoning Conditions

**NC-11.9.1 — Implicit or Undocumented Reasoning**  
Uncaptured reasoning (human or synthetic) SHALL be invalid.

**NC-11.9.2 — Proprietary or Closed Internal States**  
Any reasoning dependent on inaccessible or unverifiable internal states SHALL be invalid.

**NC-11.9.3 — Covert Automation or Hidden Agents**  
Reasoning performed by undisclosed automated processes SHALL be invalid.

---

## 11.10 Run-Level Non-Conformance Conditions

These conditions SHALL invalidate the *entire run*:

**NC-11.10.1 — Ledger Missing, Partial, or Corrupted**

**NC-11.10.2 — SHA256SUMS Missing, Partial, or Modified**

**NC-11.10.3 — Any Downstream Dependency on an Invalid Record**

**NC-11.10.4 — Failure to Halt on Invalidity (unless in diagnostic mode)**

**NC-11.10.5 — Failure of Deterministic Reconstructibility**

**NC-11.10.6 — Missing Required Final Artifacts (ledger, sums file, outputs)**

---

## 11.11 Enforcement Requirement

CRI-CORE SHALL treat any non-conformance condition enumerated in this section as grounds for immediate invalidation, ledger propagation, and run termination, unless operating in explicitly declared diagnostic mode.

---

# 12. Archival and Preservation Requirements

This section defines the mandatory requirements governing the long-term storage, immutability, and preservation of reasoning artifacts, ledgers, hash manifests, and associated cognitive provenance records.  
All requirements in this section SHALL be enforced by CRI-CORE and MUST comply with ARI governance policy ADR-0017.

---

## 12.1 Immutability of Reasoning Records

**R12.1.1** — All reasoning records produced during a workflow run SHALL be immutable once written.

**R12.1.2** — Any post-hoc modification, deletion, or mutation of a reasoning record SHALL constitute a non-conformance event.

**R12.1.3** — Corrections SHALL be made only by producing **superseding records**, not by altering existing ones.

---

## 12.2 Ledger Preservation

**R12.2.1** — Each workflow run SHALL produce a complete, append-only `reasoning_ledger` that captures all reasoning steps in strict execution order.

**R12.2.2** — The ledger SHALL be preserved in the repository as a permanent artifact of the run.

**R12.2.3** — A ledger MUST NEVER be rewritten, compacted, re-ordered, or partially removed after a run concludes.

**R12.2.4** — Any archival ledger MUST remain fully dereferenceable by commit hash.

---

## 12.3 Hash Manifest Preservation

**R12.3.1** — Every run SHALL produce a canonical `SHA256SUMS.txt` containing the exact hash of every reasoning artifact, ledger entry, and supporting file.

**R12.3.2** — This manifest SHALL be immutable and preserved exactly as produced.

**R12.3.3** — Missing or mutated hash manifests SHALL invalidate the entire run.

---

## 12.4 Version Archival and DOIs

**R12.4.1** — Any new public release of the specification or associated doctrine SHALL be archived and assigned a DOI prior to publication.

**R12.4.2** — Superseded versions SHALL be moved to an `archive/` directory within the repository, retaining their original filenames, timestamps, and checksums.

**R12.4.3** — No superseded version SHALL be deleted, overwritten, or retroactively edited.

**R12.4.4** — All archived versions SHALL remain publicly accessible and verifiable against their original DOI metadata.

---

## 12.5 Provenance Continuity

**R12.5.1** — Each archived artifact SHALL contain or reference:
- its creation timestamp,  
- its version number,  
- its hash,  
- its governing ADR(s),  
- and its DOI (if assigned).

**R12.5.2** — Artifacts MUST be stored such that their provenance can be reconstructed independently from the active branch.

**R12.5.3** — The provenance chain for any artifact SHALL be reconstructible from commit history, ledger entries, and hash manifests.

---

## 12.6 Schema and Model Preservation

**R12.6.1** — All schemas (including `neurotransparency.schema.json`) MUST be versioned and preserved in perpetuity.

**R12.6.2** — Changes to schemas SHALL require a version bump and SHALL be archived according to R12.4.x.

**R12.6.3** — Schema evolution SHALL NOT break reconstructibility of prior runs.

---

## 12.7 Long-Term Storage Requirements

**R12.7.1** — All reasoning artifacts, ledgers, manifests, and outputs SHALL be stored in durable, version-controlled storage systems (e.g., Git, DOI archives).

**R12.7.2** — No artifact SHALL rely on external, mutable, or ephemeral storage for dereferenceability.

**R12.7.3** — If external storage (e.g., Zenodo) is used, the artifact MUST be frozen and content-addressable.

---

## 12.8 Audit Trace Preservation

**R12.8.1** — Each archived run SHALL preserve:
- full ledger,  
- full hash manifest,  
- workflow metadata,  
- all reasoning artifacts,  
- and any diagnostics or error reports.

**R12.8.2** — Audit traces SHALL remain accessible for independent verification for the lifetime of the repository.

**R12.8.3** — Audit traces SHALL NOT be compressed or pruned in ways that affect reconstructibility.

---

## 12.9 Forbidden Archival Actions

**R12.9.1** — Deleting any cognitive provenance artifact SHALL be strictly prohibited.

**R12.9.2** — Retroactive editing of reasoning records, ledgers, manifests, or archived versions SHALL be prohibited.

**R12.9.3** — Renaming archived files in ways that break dereferenceability SHALL be prohibited.

**R12.9.4** — Repacking archives in ways that alter byte-level content SHALL be prohibited.

---

## 12.10 Archival Integrity Check

**R12.10.1** — CRI-CORE SHALL perform an archival integrity verification step, ensuring:
- hash manifest completeness,  
- ledger completeness,  
- schema consistency,  
- version correctness,  
- DOI consistency (if applicable).

**R12.10.2** — Failure of archival integrity SHALL invalidate the run and mark the repository state as non-conformant until corrected via superseding runs.

 ---

# 13. Compliance Test Matrix

This section defines the minimal set of tests required to validate conformance with the Neurotransparency Specification (NTS) v1.1.0.  
All tests SHALL be implementable as automated checks in CRI-CORE and executable against any AWO-governed workflow run.

A workflow run SHALL NOT be considered conformant unless **all mandatory tests pass**.

---

## 13.1 Test Categories

Tests are grouped according to the normative sections they validate:

- **T1 — Attribution Tests** (Section 3.1)  
- **T2 — Evidence-Linkage Tests** (Section 3.2)  
- **T3 — Hash Integrity Tests** (Section 3.3)  
- **T4 — Ledger Continuity Tests** (Section 3.4)  
- **T5 — Attestation Independence Tests** (Section 3.5)  
- **T6 — Run-Level Conformance Tests** (Section 3.6)  
- **T7 — Prohibition Tests** (Section 3.7)  
- **T8 — Minimal Reasoning Unit Tests** (Section 3.8)  
- **T9 — Data Model Conformance Tests** (Section 4)  
- **T10 — Archival and Preservation Tests** (Section 12)

Each test below SHALL be executed on every workflow run.

---

# 13.2 Test Definitions

---

## **T1 — Attribution Tests**

### **T1.1 — Role Presence Test (MANDATORY)**
- **Input:** Each reasoning record.  
- **Pass condition:** Every record contains a valid `role` drawn from the role registry.  
- **Fail condition:** Missing, empty, or undefined role → **non-conformance**.

### **T1.2 — Role Registry Consistency Test (MANDATORY)**
- Validate that all roles used in the run exist in the version-controlled role registry.

---

## **T2 — Evidence-Linkage Tests**

### **T2.1 — Evidence Pointer Dereference Test (MANDATORY)**
- Every evidence pointer MUST resolve to an existing artifact, prior reasoning record, or stable external artifact.
- Failure → **invalid reasoning record**.

### **T2.2 — Ephemeral Evidence Serialization Test**
- Verify that no evidence pointer references ephemeral model state or undocumented context.

---

## **T3 — Hash Integrity Tests**

### **T3.1 — Hash Match Test (MANDATORY)**
- Recompute hash for every reasoning artifact.
- Must match the corresponding line in `SHA256SUMS.txt`.

### **T3.2 — Manifest Completeness Test**
- Ensure `SHA256SUMS.txt` contains exactly one entry for each cognitive artifact.

### **T3.3 — Hash After Attribution/Evidence Test**
- Confirm that attribution + evidence-linkage precede hash computation.

---

## **T4 — Ledger Continuity Tests**

### **T4.1 — Ledger Ordering Test**
- Ledger MUST be strictly append-only and ordered by timestamp.

### **T4.2 — Deterministic Identifier Test**
- `id = f(hash, run_context)` MUST recompute identically for all entries.

### **T4.3 — Hash-Chain Test (IF IMPLEMENTED)**
- If hash chain is enabled, the `prev_hash` field MUST:
  - match the previous entry’s hash
  - form an unbroken chain from start to end.

---

## **T5 — Attestation Independence Tests**

### **T5.1 — Role Separation Test (MANDATORY)**
- Producer role MUST NOT equal attester role.

### **T5.2 — Attestation Record Integrity Test**
- Attestations MUST be recorded as standalone ledger entries with valid:
  - role  
  - timestamp  
  - evidence pointer  
  - hash

---

## **T6 — Run-Level Conformance Tests**

### **T6.1 — Invalidity Propagation Test**
- Any invalid reasoning step MUST mark all downstream dependent steps as invalid.

### **T6.2 — Terminal State Test**
- A run entering a terminal invalid state MUST NOT produce or approve final claims.

---

## **T7 — Prohibition Tests**

### **T7.1 — Implicit Reasoning Test**
- Detect undocumented or implicit reasoning transitions.

### **T7.2 — Forbidden Model-State Test**
- Reject reasoning that depends on non-serialized model states or transient memory.

### **T7.3 — Bypass Attempt Test**
- Detect attempts to bypass hashing, evidence-linkage, or attestation paths.

---

## **T8 — Minimal Reasoning Unit Tests**

### **T8.1 — Unit Structure Test**
- Verify presence of:
  - role  
  - evidence  
  - hash

### **T8.2 — Aggregation Ambiguity Test**
- Detect aggregated reasoning steps that obscure internal transitions.

---

## **T9 — Data Model Conformance Tests**

### **T9.1 — Schema Validation Test**
- Validate all reasoning records against `neurotransparency.schema.json`.

### **T9.2 — Required Field Test**
- Check for presence of:
  - `id`  
  - `role`  
  - `evidence`  
  - `hash`  
  - `timestamp`

---

## **T10 — Archival and Preservation Tests**

### **T10.1 — Immutable Archive Test**
- Confirm that archived artifacts match their historical hashes and timestamps.

### **T10.2 — Version Archival Test**
- Confirm that superseded versions:
  - are stored in `archive/`  
  - retain original metadata  
  - are never deleted or overwritten.

### **T10.3 — DOI Integrity Test**
- Validate DOI metadata against repository contents for all archived versions.

---

# 13.3 Conformance Scoring

A workflow run is:

### **COMPLIANT**
If **all mandatory tests** (T1.1, T2.1, T3.1, T4.1, T5.1, T6.1, T6.2, T9.1, T10.1) pass.

### **NON-CONFORMANT**
If **any mandatory test** fails.

### **DIAGNOSTIC**
If optional tests fail but mandatory tests pass (run is valid but suboptimal).

---

# 13.4 Automated Test Execution

CRI-CORE SHALL:

- load the run artifacts,  
- construct the test matrix,  
- execute all tests deterministically,  
- produce a `compliance_report.json` containing:
  - test results,  
  - violations,  
  - invalid artifacts,  
  - dependency graph impacts.

A run MUST NOT be approved without a passing compliance report.

---

# 14. Versioning and Governance

This section defines the authoritative governance rules for maintaining, updating, releasing, and archiving the Neurotransparency Specification (NTS).  
All requirements in this section are normative and SHALL be followed for every version of this specification, including minor corrections and patch updates.

NTS is a governed artifact under the **Aurora Research Initiative (ARI)** and inherits all provisions of **ADR-0017 — Documentation Governance Standard**.

---

## 14.1 Governance Authority

**G14.1.1** — NTS SHALL be governed under ARI’s Documentation Governance Framework.  
All modifications MUST follow the procedures defined in ADR-0017, including:

- mandatory metadata normalization,  
- immutable archival of all superseded versions,  
- independent attestation review,  
- provenance logging within the repository’s `INIT_LOG.md` and `GOVERNANCE_LOG.md`.

**G14.1.2** — No version of the specification MAY be modified retroactively.  
Once published, a version becomes an **immutable artifact** bound by its hash integrity.

**G14.1.3** — Governance authority for this specification resides with ARI and SHALL NOT be delegated to external entities or automated agents.

---

## 14.2 Version Numbering Scheme

**G14.2.1** — NTS SHALL follow semantic versioning of the form:  
```
MAJOR.MINOR.PATCH
```

Where:

- **MAJOR** — backward-incompatible or structural changes to normative rules,  
- **MINOR** — backward-compatible additions or clarifications,  
- **PATCH** — error corrections without normative changes.

**G14.2.2** — Publication of a new version MUST increment the appropriate segment and MUST NOT reuse any prior identifier.

---

## 14.3 Change Control and Attestation

**G14.3.1** — Any change to the specification MUST undergo:

1. **Author Role (Orchestrator)** — initial drafting  
2. **Reviewer Role (Auditor)** — independent verification  
3. **Approver Role (Validator)** — final attestation

No role MAY perform more than one stage of the change control process.

**G14.3.2** — Change control SHALL be recorded in:

- `INIT_LOG.md`  
- `GOVERNANCE_LOG.md`  
- hash entries in `SHA256SUMS.txt`

**G14.3.3** — Every proposal for modification MUST include:

- motivation for the change,  
- affected sections,  
- backward-compatibility assessment,  
- expected normative impact.

---

## 14.4 Release Process

**G14.4.1** — Each published version MUST be tagged in Git with:  
```
vMAJOR.MINOR.PATCH
```

**G14.4.2** — Each tag MUST correspond to:

- a fully validated hash manifest,  
- complete and exact repository contents,  
- a DOI-assigned release artifact,  
- an attached PDF generated by a deterministic workflow (Waveframe PDF Forge).

**G14.4.3** — Each release MUST include a `RELEASE_NOTES.md` documenting:

- new normative rules,  
- removed or superseded rules,  
- compatibility notes,  
- migration requirements (if any).

---

## 14.5 DOI Assignment and Metadata Governance

**G14.5.1** — Each release SHALL be assigned a unique DOI through Zenodo or an equivalent trusted archive.

**G14.5.2** — DOI metadata MUST match:

- version number,  
- release date,  
- authorship,  
- licensing terms,  
- repository URL,  
- hash-bound PDF artifact.

**G14.5.3** — DOIs MUST be permanent and SHALL NOT be updated once published.

---

## 14.6 Archival Requirements

**G14.6.1** — Superseded versions MUST be stored in:
```  
archive/versions/vMAJOR.MINOR.PATCH/  
```  

Including:

- complete markdown copy of the specification,  
- SHA256SUMS.txt,  
- RELEASE_NOTES.md,  
- assigned DOI,  
- PDF release artifact.

**G14.6.2** — No version MAY be deleted, rewritten, or replaced.  
All prior versions MUST remain permanently accessible.

**G14.6.3** — Archived versions MUST retain their original timestamps, metadata, and content hashes to preserve historical cognitive provenance.

---

## 14.7 Provenance and Traceability

**G14.7.1** — Every version SHALL include:

- hash-bound files,  
- metadata front matter,  
- provenance log entries,  
- deterministic build artifacts.

**G14.7.2** — Provenance records MUST be machine-verifiable and MUST NOT rely on external or ephemeral states.

**G14.7.3** — All changes to NTS MUST be accompanied by reasoning records subject to neurotransparency.  
Undocumented normative modifications SHALL be treated as non-conformant.

---

## 14.8 Relationship to Other ARI Artifacts

**G14.8.1** — NTS SHALL define the normative rules governing:

- cognitive provenance (doctrine implementation),  
- AWO workflow governance,  
- CRI-CORE runtime enforcement.

**G14.8.2** — The Doctrine provides philosophical justification but SHALL NOT override the normative requirements of this specification.

**G14.8.3** — CRI-CORE MUST enforce this specification exactly as written.  
Interpretive implementation SHALL NOT be permitted.

---

## 14.9 Governance Invariants

The following invariants MUST hold across all versions:

- **No normative rule may be weakened in a PATCH version.**  
- **No removal of archival material is ever permitted.**  
- **Governance MAY NOT be delegated to a single agent.**  
- **Evidence-linkage MUST remain mandatory in all future versions.**  
- **Hash integrity MUST remain mandatory in all future versions.**

---

## 14.10 Supersession Rules

**G14.10.1** — A newer version supersedes older versions but DOES NOT invalidate them.  
Superseded versions remain valid historical artifacts.

**G14.10.2** — A specification MAY NOT supersede itself retroactively.

---

## 14.11 Sunset and Replacement Policy

**G14.11.1** — If a future specification replaces NTS, the replacement MUST explicitly declare:

- its supersession lineage,  
- its compatibility or incompatibility,  
- its migration rules,  
- its archival obligations.

**G14.11.2** — Replacement specifications MUST NOT implicitly repeal NTS.

---

## 14.12 Governance Violations

Any deviation from the rules in this section SHALL be treated as:

- a **non-conformance event** under NTS Section 11,  
- an **invalid governance action**,  
- grounds for rejecting the affected version or run.

---

This section establishes the full governance envelope for NTS, ensuring that every version is immutable, traceable, independently attested, and permanently archivable as a governed scientific artifact.

---

# Appendix A — JSON Schema Stub (Non-Normative)

This appendix provides a forward-compatible **stub** for the future
`neurotransparency.schema.json` file.  
It is **non-normative**, incomplete, and SHALL NOT be treated as part of NTS v1.1.0’s normative requirements.

The purpose of this stub is to:

- provide a structural placeholder for CRI-CORE integration,
- indicate the minimal fields expected in future schema versions,
- support early validation tooling without prematurely fixing full schema semantics.

Future versions (NTS v1.2.x and CRI-CORE v0.2+) will provide the complete schema.

---

## A.1 Scope of the Stub

This stub includes the **required top-level fields** and their expected types, but omits:

- constraints,
- enumerations,
- pattern definitions,
- cross-field invariants,
- ledger or attestation structures,
- algorithmic validation logic.

Implementations MUST treat all omitted fields and behaviors as undefined.

---

## A.2 neurotransparency.schema.json (Stub)

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Neurotransparency Reasoning Record (Stub)",
  "description": "Non-normative placeholder schema for future CRI-CORE enforcement.",
  "type": "object",

  "properties": {
    "id": {
      "type": "string",
      "description": "Deterministic reasoning identifier (definition deferred)."
    },

    "role": {
      "type": "string",
      "description": "Epistemic role performing the reasoning step (e.g., Orchestrator, Auditor, Synthesizer)."
    },

    "timestamp": {
      "type": "string",
      "format": "date-time",
      "description": "ISO 8601 timestamp representing when the reasoning step occurred."
    },

    "evidence": {
      "type": "array",
      "items": { "type": "string" },
      "minItems": 1,
      "description": "Dereferenceable pointers to evidence artifacts. Future versions will restrict format."
    },

    "hash": {
      "type": "string",
      "pattern": "^[a-f0-9]{64}$",
      "description": "SHA-256 digest of the reasoning record after attribution and evidence binding."
    },

    "metadata": {
      "type": "object",
      "description": "Optional contextual metadata. Semantics to be defined in future versions."
    }
  },

  "required": [
    "id",
    "role",
    "timestamp",
    "evidence",
    "hash"
  ],

  "additionalProperties": false
}
```  
## A.3 Notes for Future Versions (Non-Normative)   

The following elements will be defined in future normative updates:    
- deterministic rules for generating id values,
- enumerated role registry integration,
- evidence-pointer type constraints,
- ledger-entry chaining,
- attestation-record schema,
- cross-record referential integrity,
- minimal reasoning unit compression semantics.

These elements are intentionally omitted from the v1.1.0 stub to allow CRI-CORE to define enforcement logic without prematurely constraining the NTS.  

## A.4 Conformance Notice  

This appendix is non-normative.
Implementations MUST NOT treat the stub as defining compliance rules.
Only Sections 1–14 of this specification are normative.  

---

# Appendix B — Non‑Normative Examples

> **Status:** Non‑normative  
> These examples illustrate how a neurotransparency‑compliant system MAY structure reasoning records, ledgers, and validation states. They are provided for clarification only and MUST NOT be treated as additional requirements beyond Section 3–14 of this specification.

---

## B.1 Minimal Conformant Reasoning Record (YAML)

The following example shows a **minimal conformant reasoning record** consistent with the NTS v1.1.0 data model and requirements in Sections 3–6.

```yaml
id: rr-2025-12-03T14-21-07Z-0001
role: Synthesizer
timestamp: 2025-12-03T14:21:07Z
evidence:
  - type: literature_summary
    ref: artifacts/lit_summaries/2025-12-03-paper-X.md#claim-3
    hash: 9f1c0c2c3f5a0c7e4a7f0d8a1e93b7b7742d0a8f6a4c2e7b9d3e5c7f1a2b3c4
output:
  type: draft_claim
  ref: artifacts/drafts/claim_001.md
  hash: 355b24f4d6b4a33724c579e456a063eec0759b3476c540293b421fd92c7dfec7
metadata:
  run_id: awo-run-2025-12-03T14-20-00Z
  workflow: literature_synthesis_v2
  model: gpt-5.1
  temperature: 0.2
```

This record satisfies:

- explicit **role** (`Synthesizer`)  
- dereferenceable **evidence** pointers  
- SHA‑256 **hash**es for both evidence and output  
- a deterministic **id** and **timestamp**  
- optional but useful **metadata** for audit and recomputation

---

## B.2 Example Reasoning Ledger Excerpt

The following example shows an excerpt from a **reasoning ledger** for a single run, capturing both reasoning and attestation events.

```yaml
run_id: awo-run-2025-12-03T14-20-00Z
ledger:
  - id: rr-2025-12-03T14-21-07Z-0001
    type: reasoning
    role: Synthesizer
    timestamp: 2025-12-03T14:21:07Z
    prev_entry_hash: null
    evidence:
      - type: literature_summary
        ref: artifacts/lit_summaries/2025-12-03-paper-X.md#claim-3
        hash: 9f1c0c2c3f5a0c7e4a7f0d8a1e93b7b7742d0a8f6a4c2e7b9d3e5c7f1a2b3c4
    output:
      ref: artifacts/drafts/claim_001.md
      hash: 355b24f4d6b4a33724c579e456a063eec0759b3476c540293b421fd92c7dfec7

  - id: rr-2025-12-03T14-25-40Z-0002
    type: attestation
    role: Auditor
    timestamp: 2025-12-03T14:25:40Z
    prev_entry_hash: c2a0d4f9e00b9d3c4f1a2b3c7e5c9f1c0c2c3f5a0c7e4a7f0d8a1e93b7b7742
    attests_to: rr-2025-12-03T14-21-07Z-0001
    evidence:
      - type: review_note
        ref: artifacts/reviews/claim_001_audit.md
        hash: 7b7742d0a8f6a4c2e7b9d3e5c7f1a2b3c49f1c0c2c3f5a0c7e4a7f0d8a1e93b
    output:
      ref: artifacts/approvals/claim_001_approved.json
      hash: a8f6a4c2e7b9d3e5c7f1a2b3c49f1c0c2c3f5a0c7e4a7f0d8a1e93b7b7742d0
```

This example illustrates:

- separation of **reasoning** and **attestation** events  
- hash‑chain via `prev_entry_hash`  
- independent **Auditor** role attesting to **Synthesizer** output  
- full trace from evidence → draft claim → audit note → approval artifact

---

## B.3 Non‑Conformant Example: Missing Evidence Pointer

The following reasoning record is **non‑conformant** with NTS:

```yaml
id: rr-2025-12-03T15-01-10Z-0003
role: Orchestrator
timestamp: 2025-12-03T15:01:10Z
evidence: []
output:
  ref: artifacts/drafts/claim_002.md
  hash: 0c7e4a7f0d8a1e93b7b7742d0a8f6a4c2e7b9d3e5c7f1a2b3c49f1c0c2c3f5a0
```

Violation:

- **R3.2.1** — Each reasoning step SHALL include one or more evidence pointers.  
- This record MUST be treated as a **non‑conformance event** and SHALL NOT influence any claim.

---

## B.4 Non‑Conformant Example: Self‑Attestation

```yaml
id: rr-2025-12-03T15-10-00Z-0004
type: attestation
role: Synthesizer
timestamp: 2025-12-03T15:10:00Z
attests_to: rr-2025-12-03T14-21-07Z-0001
evidence:
  - type: self_review
    ref: artifacts/reviews/claim_001_self_check.md
    hash: 3f5a0c7e4a7f0d8a1e93b7b7742d0a8f6a4c2e7b9d3e5c7f1a2b3c49f1c0c2c3
```

Violation:

- **R3.5.1** — A role SHALL NOT attest to or approve reasoning that originates from the same role.  
- This attestation and any dependent approvals MUST be invalidated.

---

## B.5 Non‑Conformant Example: Hash Mismatch

```yaml
id: rr-2025-12-03T15-20-30Z-0005
role: Validator
timestamp: 2025-12-03T15:20:30Z
evidence:
  - type: dataset
    ref: data/processed/experiment_07.parquet
    hash: 1111111111111111111111111111111111111111111111111111111111111111
output:
  ref: artifacts/results/exp07_summary.md
  hash: 2222222222222222222222222222222222222222222222222222222222222222
```

If recomputation yields a different hash for either `data/processed/experiment_07.parquet` or `artifacts/results/exp07_summary.md`, this violates:

- **R3.3.3** — Any mismatch between a recorded hash and the computed hash of an artifact SHALL invalidate that artifact and all reasoning steps dependent upon it.

The run MUST enter a non‑conformant state and SHALL NOT produce approved claims based on this record.

---

# Appendix C — File List & Release Packaging Notes

> **Status:** Non‑normative  
> This appendix describes recommended file layout, packaging conventions, and release assets for Neurotransparency Specification (NTS) v1.1.0 implementations and reference repositories. It is provided for guidance only and SHALL NOT be interpreted as adding new normative requirements.

---

## C.1 Recommended Repository Layout

A minimal NTS‑aligned repository MAY adopt the following structure:

```text
/
├── NTS_Specification_v1.1.0.md      # Canonical normative specification (this document)
├── LICENSE.md                       # CC BY 4.0 license text
├── CITATION.cff                     # Citation metadata
├── README.md                        # Repository overview and links
├── INIT_LOG.md                      # Initialization and governance log
├── figures/
│   └── nts_spec_banner.png          # Optional banner / diagrams
├── schemas/
│   └── neurotransparency.schema.json    # JSON Schema for reasoning records
├── tests/
│   ├── nts_compliance_matrix.md     # Human‑readable test matrix
│   └── nts_compliance_tests.json    # Optional machine‑readable test cases
└── archive/
    └── v1.0.x/                      # Previous versions (if applicable)
```

This layout ensures:

- clear separation between normative text, schemas, tests, and figures  
- stable paths for CRI‑CORE and AWO to reference  
- clean archival of superseded versions under `/archive/`

---

## C.2 Required Specification‑Level Files (Recommended)

The following files are RECOMMENDED for any repository hosting the canonical NTS text:

| File | Purpose |
|------|---------|
| `NTS_Specification_v1.1.0.md` | Canonical normative specification for NTS v1.1.0 |
| `LICENSE.md` | License for the specification (CC BY 4.0) |
| `CITATION.cff` | Citation metadata (author, version, year, DOI) |
| `README.md` | High‑level overview, scope, and navigation |
| `INIT_LOG.md` | Initialization and governance record for the repository |
| `figures/nts_spec_banner.png` | Optional banner / diagram used in README and PDF |
| `schemas/neurotransparency.schema.json` | Machine‑readable schema for reasoning records |
| `tests/nts_compliance_matrix.md` | Human‑readable mapping of tests → NTS requirements |
| `tests/nts_compliance_tests.json` | Optional machine‑readable test suite descriptor |

Implementations MAY add additional files (e.g., language bindings, SDKs, or CRI‑CORE integration examples) without affecting conformance, provided the normative specification remains unchanged.

---

## C.3 Release Assets and Packaging

For each tagged NTS release (e.g., `v1.1.0`), it is RECOMMENDED to publish the following assets as part of the GitHub (or equivalent) release:

| Asset | Description |
|-------|-------------|
| `NTS_Specification_v1.1.0.md` | Canonical Markdown source of the specification |
| `NTS_Specification_v1.1.0.pdf` | Scholar‑grade PDF build (e.g., via Waveframe PDF Forge) |
| `neurotransparency.schema.json` | JSON Schema describing the reasoning record data model |
| `nts_compliance_matrix.md` | Compliance matrix mapping R‑requirements to tests |
| `nts_compliance_tests.json` | Optional machine‑readable compliance test descriptions |
| `SHA256SUMS.txt` | Hash manifest covering **all** release artifacts |
| `RELEASE_NOTES_v1.1.0.md` | Human‑readable summary of changes for this version |

The **SHA256SUMS.txt** file SHOULD be treated as a normative anchor for the release:  
any modification to a tagged asset that changes its hash MUST result in a new tag and a new release.

---

## C.4 Zenodo / DOI Registration

It is RECOMMENDED that each NTS release be registered with a DOI provider such as Zenodo.

Suggested pattern:

- **Concept DOI** — assigned to the NTS specification family (e.g., all v1.x versions)  
- **Versioned DOIs** — one DOI per released version (e.g., v1.0.0, v1.1.0)

The following metadata SHOULD be included in Zenodo (or equivalent) records:

- title: `Neurotransparency Specification (NTS)`  
- version: `1.1.0`  
- resource type: `Software documentation` or `Technical specification`  
- authors: `Wright, Shawn C.`  
- affiliation: `Waveframe Labs / Aurora Research Initiative (ARI)`  
- license: `CC BY 4.0`  
- related identifiers: Doctrine DOI, AWO DOI, CRI‑CORE DOI (when applicable)

The DOI assigned to a given version SHOULD be propagated into:

- `CITATION.cff`  
- `README.md`  
- the header of `NTS_Specification_v1.1.0.md`  
- any generated PDF front‑matter

---

## C.5 Example Release Checklist (Non‑Normative)

Before publishing an NTS release, maintainers MAY use the following checklist:

- [ ] All normative text reviewed for internal consistency and ARI alignment  
- [ ] `NTS_Specification_v1.1.0.md` finalized and committed  
- [ ] `LICENSE.md` and `CITATION.cff` verified  
- [ ] `neurotransparency.schema.json` validated against example records  
- [ ] `nts_compliance_matrix.md` aligned with all R‑requirements  
- [ ] Scholar‑grade PDF generated and visually inspected  
- [ ] `SHA256SUMS.txt` regenerated and verified  
- [ ] Git tag created (e.g., `v1.1.0`) and pushed  
- [ ] Release created with all assets attached  
- [ ] DOI minted and back‑propagated into repo metadata

These practices help ensure that NTS remains a stable, citable, and reproducible specification within the broader Aurora ecosystem.

---
