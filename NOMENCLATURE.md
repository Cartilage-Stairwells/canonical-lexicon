# Triune-Oracle Nomenclature & Acronym Key

## Canonical Lexicon v0.1

**Status:** Working canonical reference
**Purpose:** Terminology, acronym, abbreviation, and nomenclature index for the Triune-Oracle / Continuity Engineering corpus.

---

## 1. Purpose

This document defines the canonical vocabulary used throughout the Triune-Oracle engineering, verification, evidence, formalization, custody, kernel, and research corpus.

It exists to prevent terminology drift as the project expands across specifications, implementations, tests, formal proofs, evidence artifacts, repositories, correspondence, grant materials, and external review.

This document is an index and terminology authority, not a replacement for the specifications that define individual contracts.

Where a specification and this index appear to conflict, the applicable frozen specification governs. This document should then be corrected so that the index reflects the authoritative definition.

---

## 2. Entry Schema

Each canonical term should be recorded using the following structure:

| Field | Meaning |
|-------|---------|
| Term | Canonical name |
| Acronym | Abbreviated form, if applicable |
| Literal | Literal expansion of the acronym |
| Definition | Formal meaning |
| Practical meaning | What the term means operationally |
| Domain | Architectural or conceptual domain |
| Status | Proposed / Active / Frozen / Superseded |
| Authority | Artifact or specification governing the term |
| Related terms | Closely coupled concepts |
| Do not confuse with | Known semantic collisions |

---

## 3. Core System Terms

### Triune-Oracle

- **Acronym:** TO
- **Literal:** Triune-Oracle
- **Definition:** The overarching project/system identity encompassing the continuity, evidence, verification, agent, kernel, protocol, and related engineering work.
- **Practical meaning:** The umbrella under which the individual protocols, engines, artifacts, research programs, and verification systems are organized.
- **Domain:** System / Project
- **Status:** Active

---

### Triune System Hive

- **Acronym:** TSH
- **Literal:** Triune System Hive
- **Definition:** The broader multi-component system architecture in which the Triune components and agents operate.
- **Practical meaning:** The system-level environment rather than one individual implementation or protocol.
- **Domain:** Architecture
- **Status:** Active

---

### Triumvirate Continuity Engineering Runtime

- **Acronym:** TCER
- **Literal:** Triumvirate Continuity Engineering Runtime
- **Definition:** The platform/runtime identity used for the continuity-engineering stack.
- **Practical meaning:** The engineering-runtime framing of the system and its continuity mechanisms.
- **Domain:** Runtime / Architecture
- **Status:** Active

---

## 4. Continuity and Protocol Terms

### TSCP

- **Literal:** Telemetry Sign-Off and Concurrency Protocol
- **Definition:** The protocol family governing telemetry sign-off, concurrency, verification, and associated evidence/transition semantics.
- **Practical meaning:** The principal protocol framework through which system transitions and their evidence are constrained and verified.
- **Domain:** Protocol / Verification
- **Status:** Frozen family
- **Related:** TSCP-FCO, TSCP-PL, TSCP-AUDIT-CANON

---

### TSCP-FCO

- **Literal:** Telemetry Sign-Off and Concurrency Protocol — Field Coherence Object
- **Definition:** The TSCP evidence-boundary framework centered on the Field Coherence Object.
- **Practical meaning:** The custody/evidence mechanism used to carry admissible evidence across transformations without granting the evidence object authority.
- **Domain:** Evidence / Custody
- **Status:** Active / Constitutional specification

---

### FCO

- **Literal:** Field Coherence Object
- **Canonical definition:** An Evidence Boundary, not an Authority Boundary.
- **Practical meaning:** An FCO packages and constrains evidence relevant to continuity and admissibility while explicitly possessing no authority of its own.
- **Constitutional invariant:** `Authority(FCO) = 0`
- **Critical distinction:** An FCO does not establish truth, value, authorization, execution authority, or promotion authority.
- **Domain:** Evidence / Custody
- **Status:** Frozen
- **Do not confuse with:** Certificate, authorization token, truth assertion, approval object.

---

### TSCP-AUDIT-CANON

- **Literal:** TSCP Audit Canon
- **Definition:** The identity-first audit/admission plane establishing canonical identity before downstream evaluation.
- **Practical meaning:** Identity is established before an artifact or state can enter subsequent evaluation processes.
- **Authority:** 0
- **Architectural restriction:** The audit plane cannot approve, authorize, execute, or promote.
- **Domain:** Audit / Identity Admission
- **Status:** Active / Canonical

---

### TSCP-PL

- **Literal:** TSCP Protocol Layer
- **Definition:** The protocol-layer specification governing TSCP behavior and contracts.
- **Practical meaning:** The protocol specification layer against which implementations and verification artifacts are evaluated.
- **Domain:** Protocol
- **Status:** Active

---

## 5. Evidence and Admissibility

### REO

- **Literal:** Resonance Evaluation Object
- **Definition:** An object representing the structured subject of resonance/evaluation processes without implying certification authority.
- **Practical meaning:** A neutral evaluation object rather than an authorization certificate.
- **Domain:** Evaluation / Evidence
- **Status:** Active
- **Do not confuse with:** Certificate, authorization, approval.

---

### AdmittedEvidence

- **Literal:** Admitted Evidence
- **Definition:** Evidence that satisfies the declared admissibility predicate.
- **Practical meaning:** The system has established that the evidence meets the requirements for admission into a specified evidence context.
- **Critical semantic restriction:** AdmittedEvidence means admissible, not necessarily true.
- It does not independently establish:
  - truth
  - authority
  - correctness of the underlying claim
  - authorization
  - execution permission
  - promotion permission
- **Domain:** Admissibility / Evidence
- **Status:** Active

---

### Admissibility Contract

- **Acronym:** AC
- **Literal:** Admissibility Contract
- **Definition:** The contract specifying the conditions under which an artifact/evidence object may be admitted into a declared context.
- **Practical meaning:** The gate that determines whether evidence satisfies the required structural and semantic admission conditions.
- **Domain:** Admissibility
- **Status:** Active

---

### Semantic Non-Invention Gate

- **Acronym:** SNIG
- **Literal:** Semantic Non-Invention Gate
- **Definition:** A proposed gate preventing downstream stages from introducing semantic claims not supported by the admitted evidence or declared contract.
- **Practical meaning:** A defense against semantic laundering or accidental invention of meaning during transformations.
- **Domain:** Evidence / Semantics
- **Status:** Candidate / Proposed

---

## 6. Observation and Integrity

### INTEGRITY

- **Acronym:** —
- **Definition:** Adversarial evaluation over a declared structural-context boundary.
- **Formally:** `O_SHARK ⊆ O_INTEGRITY ⊆ O_global`
- **Practical meaning:** Integrity is not simply whatever can be determined from the currently exposed observation. It may require observations beyond the local SHARK observation boundary.
- **Domain:** Integrity / Epistemology / Verification
- **Status:** Frozen definition

---

### SHARK

- **Acronym:** SHARK
- **Literal:** Canonical expansion to be retained from the governing artifact when formally fixed.
- **Definition:** The local observation/evaluation framework used in the SHARK/INTEGRITY audit program.
- **Practical meaning:** The declared local observable through which specific integrity questions are evaluated.
- **Domain:** Observation / Integrity
- **Status:** Active / Frozen audit framework
- **Critical property:** If two states are locally indistinguishable under the SHARK observation: `O_SHARK(G_v) = O_SHARK(G_i)` then no predicate operating solely on that observation can distinguish them.

---

### O_SHARK

- **Literal:** SHARK Observation
- **Definition:** The observation available to the SHARK-local evaluator.
- **Practical meaning:** The information boundary visible to SHARK.
- **Domain:** Observation
- **Status:** Frozen

---

### MinObs

- **Literal:** Minimal Observation
- **Definition:** The set of minimal sufficient observation domains required to establish a specified predicate.
- **Conceptually:** `ObsDepth_𝒪(P) = min_≼ { O ∈ 𝒪 : Sufficient_P(O) }`
- **Practical meaning:** The smallest observation level — or set of minimal levels — capable of answering a particular question.
- **Important:** MinObs is predicate-relative. There is no universally minimal observation independent of the question being asked.
- **Domain:** Observation Lattice
- **Status:** Active

---

### ObsDepth

- **Literal:** Observation Depth
- **Definition:** The minimum position, under the observation partial order, at which a predicate becomes sufficient to evaluate.
- **Practical meaning:** How much structural context must be exposed before a particular property becomes decidable.
- **Domain:** Observation Lattice
- **Status:** Active

---

### O₀

- **Literal:** Observation Level 0
- **Definition:** Base observation consisting of the relevant initial and resulting states/context without additional relational or provenance information.
- **Practical meaning:** The weakest observation level in the current lattice.
- **Known limitation:** Cannot distinguish CE16–CE18.

---

### O₁

- **Literal:** Observation Level 1
- **Definition:** Observation expanded with relationship information.
- **Practical meaning:** Adds relationships but remains insufficient for the relevant CE16–CE18 distinctions.

---

### O₂

- **Literal:** Observation Level 2
- **Definition:** Observation expanded with local provenance.
- **Practical meaning:** Sufficient to distinguish CE16 and CE17 in the established audit construction.

---

### O₂.₁

- **Literal:** Observation Level 2.1 — EvidenceLookup
- **Definition:** Observation domain incorporating evidence lookup.
- **Practical meaning:** A refinement of the observation boundary that can retrieve evidence necessary for particular predicates.
- **Domain:** Observation / Evidence
- **Status:** Active

---

### O₂.₂

- **Literal:** Observation Level 2.2 — EdgeSet
- **Definition:** Observation consisting of the local pair plus the complete relevant edge set without exposing the complete node set.
- **Practical meaning:** Provides graph-edge context without escalating all the way to full graph observation.
- **Important:** O₂.₁ and O₂.₂ are not assumed to dominate one another.

---

### O₃

- **Literal:** Observation Level 3
- **Definition:** Full graph observation.
- **Practical meaning:** The complete graph is exposed to the evaluator and can distinguish all three established CE16–CE18 cases.

---

## 7. Observation Lattice

### Observation Lattice

- **Acronym:** 𝒪 / observation lattice
- **Definition:** A partially ordered set of observation domains related by an expansion relation.
- **Current established structure:** `O₀ ≼ O₁ ≼ O₂ ≼ O₂.₁ ≼ O₃` with O₂.₂ forming an incomparable branch relative to O₂ and O₂.₁.
- **Practical meaning:** More observation is not necessarily a simple linear ladder. Different observation expansions can expose different information.
- **Domain:** Formal Semantics / Verification
- **Status:** Active

---

### Eᵢ→ⱼ

- **Literal:** Observation Expansion Relation from i to j
- **Definition:** The transformation that expands one observation domain into another while preserving semantic identity.
- **Practical meaning:** Defines how additional observable structure is introduced without changing the underlying semantic object.
- **Domain:** Observation Lattice
- **Status:** Active

---

## 8. Counterexample / Boundary Terms

### CE16

- **Literal:** Counterexample 16
- **Definition:** One of the canonical locally-indistinguishable integrity boundary constructions.
- **Practical meaning:** Demonstrates that the relevant distinction cannot be established from insufficient observation.
- **Domain:** SHARK / Integrity
- **Status:** Frozen

---

### CE17

- **Literal:** Counterexample 17
- **Definition:** Canonical integrity-boundary construction demonstrating insufficiency of the applicable lower observation domain.
- **Domain:** SHARK / Integrity
- **Status:** Frozen

---

### CE18

- **Literal:** Counterexample 18
- **Definition:** Canonical integrity-boundary construction completing the established local-indistinguishability family.
- **Domain:** SHARK / Integrity
- **Status:** Frozen

---

## 9. Kernel / Mathematical Terms

### NTT

- **Literal:** Number-Theoretic Transform
- **Definition:** The finite-field analogue of the discrete Fourier transform used in the project's computational kernels.
- **Practical meaning:** The transform underlying the relevant polynomial/field computations and optimized butterfly implementations.
- **Domain:** Cryptographic Computing / Kernel
- **Status:** Active

---

### DIT

- **Literal:** Decimation-In-Time
- **Definition:** An NTT/FFT decomposition strategy in which the input is recursively decomposed by time/index structure.
- **Practical meaning:** One of the transform organizations used by the optimized NTT implementation.

---

### DIF

- **Literal:** Decimation-In-Frequency
- **Definition:** An NTT/FFT decomposition strategy organized around frequency/output structure.
- **Practical meaning:** The alternate transform organization whose ordering conventions must match the implementation and verification expectations.

---

### SIMD

- **Literal:** Single Instruction, Multiple Data
- **Definition:** A computation model in which one instruction operates on multiple data lanes.
- **Practical meaning:** The vectorization mechanism used to accelerate field and butterfly operations.

---

### AVX-512

- **Literal:** Advanced Vector Extensions 512-bit
- **Definition:** A 512-bit SIMD instruction-set extension supported by relevant x86 processors.
- **Practical meaning:** The 16-lane vector execution path used in the optimized field/butterfly kernel.

---

### NEON

- **Literal:** ARM Advanced SIMD / NEON
- **Definition:** ARM's SIMD instruction architecture.
- **Practical meaning:** The 4-wide vector execution path used for portable acceleration on ARM hardware.

---

### Montgomery Reduction

- **Acronym:** MR
- **Literal:** Montgomery Reduction
- **Definition:** Modular reduction technique using a Montgomery representation to avoid expensive division operations.
- **Practical meaning:** The reduction mechanism used by the field arithmetic implementation and formalization.

---

### R

- **Literal:** Montgomery radix
- **Definition:** The Montgomery representation radix used by the implementation.
- **Current value:** 2³²

---

### SimdField<16>

- **Literal:** 16-lane SIMD Field
- **Definition:** A field-arithmetic representation operating on sixteen lanes of data.
- **Practical meaning:** The AVX-512 vectorized field abstraction used by the optimized kernel.

---

## 10. Proof / Formalization

### Lean

- **Literal:** Lean theorem prover / proof assistant
- **Definition:** The formal verification environment used for the mathematical backbone.
- **Practical meaning:** The environment in which the project's formal propositions and arithmetic properties are mechanically checked.

---

### P0

- **Literal:** Priority-0 / foundational specification designation
- **Definition:** The highest-priority designation currently used for frozen foundational contracts that establish prerequisites for downstream implementation or verification.
- **Practical meaning:** A P0 document is not merely ordinary project documentation. It establishes a foundational contract against which subsequent work must be constructed or evaluated.
- **Current P0 family includes:**
  1. P0-CANONICAL-SERIALIZATION-SPEC-001
  2. P0-ARTIFACT-REFERENCE-SPEC-001
  3. The associated P0 resolver/contract chain.
- **Domain:** Specification / Architecture
- **Status:** Active / Foundational
- **Important:** P0 is a priority/classification designation, not itself a technical subsystem.

---

### P0-CANONICAL-SERIALIZATION-SPEC-001

- **Literal:** Priority-0 Canonical Serialization Specification 001
- **Definition:** Foundational contract defining canonical serialization behavior.
- **Practical meaning:** Establishes the deterministic representation required for artifact identity, comparison, hashing, and downstream evidence operations.

---

### P0-ARTIFACT-REFERENCE-SPEC-001

- **Literal:** Priority-0 Artifact Reference Specification 001
- **Definition:** Foundational contract defining how artifact references are represented and resolved.
- **Practical meaning:** Makes artifact resolution semantics explicit and prevents implementation-specific interpretation of references.

---

## 11. Custody / State Terms

### Custody Plane

- **Definition:** The architectural plane responsible for maintaining and constraining evidence/state custody through declared transitions.
- **Practical meaning:** Controls what may happen to evidence as it moves through the system.
- **Authority:** Does not inherently grant authority to evidence objects.

---

### Evolution Plane

- **Definition:** The architectural plane concerned with system evolution/transformation rather than custody authority.
- **Practical meaning:** Separates system change from evidence custody and prevents transformation semantics from silently becoming authority semantics.

---

### Fail-Closed

- **Definition:** A security/verification property in which an unrecognized, invalid, or unauthorized transition is rejected rather than interpreted permissively.
- **Practical meaning:** Missing evidence or invalid state does not silently become acceptance.

---

## 12. Artifact / Evidence Terms

### TSCP-CANON-001

- **Literal:** TSCP Canonical Artifact Specification 001
- **Definition:** Canonical serialization/identity contract for TSCP artifacts.
- **Practical meaning:** Establishes deterministic artifact representation and identity.
- **Status:** Frozen

---

### SHA256SUMS

- **Literal:** SHA-256 Checksums
- **Definition:** A collection of SHA-256 cryptographic hashes used to bind artifacts to their recorded byte representations.
- **Practical meaning:** Provides integrity evidence for archived artifacts.

---

### Receipt

- **Definition:** A structured record documenting an event, transition, artifact, or evidence claim according to the applicable receipt contract.
- **Practical meaning:** A receipt is evidence about a declared event; it is not automatically authority or truth.

---

### Evidence Boundary

- **Definition:** A declared boundary governing what evidence is admitted, visible, or transferable for a particular operation.
- **Practical meaning:** Defines the epistemic scope of an operation.
- **Critical distinction:** Evidence boundary ≠ authority boundary.

---

## 13. Architectural Semantics

### Authority

- **Definition:** The capability or standing to authorize, execute, approve, promote, or otherwise cause an action according to a declared authority model.
- **Practical meaning:** Authority is an architectural capability, not a property automatically produced by evidence or observation.

---

### Observation

- **Definition:** The information exposed to an evaluator.
- **Practical meaning:** Observation determines what a predicate can distinguish.
- **Critical distinction:** Observation ≠ Authority and Admissibility ≠ Truth.

---

### Semantic Laundering

- **Definition:** The implicit transformation of weak, local, or merely admissible information into a stronger semantic claim without an explicit contract establishing that transformation.
- **Practical meaning:** A system must not silently turn "this evidence was admitted" into "this claim is true," or "this object was observed" into "this object is authorized."

---

### Type-Level Enforcement

- **Definition:** Enforcement of semantic or structural constraints through the programming-language type system.
- **Practical meaning:** Types can make invalid states harder to construct, but types are not by themselves the complete security boundary.
- **Known boundary threats:** serialization, FFI, reflection, persistence, generated code, type erasure, external representations.

---

## 14. Agent / System Components

### Legio

- **Literal:** Legio
- **Definition:** The project's agentic/orchestration component and associated protocol framework.
- **Practical meaning:** Coordinates agent/system operations within the broader Triune architecture.

---

### Watchtower

- **Definition:** Monitoring/observation component of the broader system.
- **Practical meaning:** Provides surveillance/monitoring functions over system activity and evidence.

---

### Memory Core

- **Definition:** Persistent memory/context component of the system architecture.
- **Practical meaning:** Stores and retrieves continuity-relevant system information.

---

### Vaultfire

- **Definition:** Named subsystem/artifact family within the Triune ecosystem.
- **Practical meaning:** A project-specific component whose exact contract is defined by its governing artifacts.

---

### Codex

- **Definition:** The project's structured knowledge/artifact corpus.
- **Practical meaning:** The durable knowledge layer containing specifications, definitions, records, and related canonical material.

---

## 15. Status Vocabulary

### Proposed
A term or construct under consideration that has not yet been canonically frozen.

### Candidate
A proposed concept being evaluated for formal adoption.

### Active
A currently used term or mechanism whose definition remains operative.

### Frozen
A definition or contract that has been explicitly fixed and should not be changed casually.

### Superseded
A former canonical definition replaced by a later artifact or specification.

### Deprecated
A term that remains historically recognizable but should no longer be used for new artifacts.

### Informal
A useful descriptive term that has not been granted canonical semantic authority.

---

## 16. Canonical Semantic Rules

The following distinctions should remain globally stable unless explicitly revised by a higher-order specification.

### 16.1 Observation is not Authority
An evaluator seeing information does not thereby acquire authority over the object being observed.

### 16.2 Admissibility is not Truth
Satisfying an admissibility predicate means that the evidence satisfies the declared admission conditions. It does not independently establish truth.

### 16.3 Evidence is not Authority
Evidence may support a decision without possessing authority to make the decision.

### 16.4 FCO is an Evidence Boundary
The FCO must be interpreted as an evidence boundary, never as an authority boundary. `Authority(FCO) = 0`

### 16.5 Identity Precedes Evaluation
The identity-first architecture establishes canonical identity before downstream evaluation.

### 16.6 Audit Has Authority Zero
The audit/identity admission plane cannot approve, authorize, execute, or promote.

### 16.7 Observation Sufficiency is Predicate-Relative
The observation required to establish one predicate may be insufficient or excessive for another.

### 16.8 More Observation is Not Necessarily a Linear Hierarchy
The observation structure is a lattice/partial order. Different expansions may be incomparable.

### 16.9 Type Systems Are Not the Entire Security Boundary
Type-level guarantees do not automatically survive serialization, FFI, reflection, persistence, generated code, or type erasure.

### 16.10 Canonical Specifications Govern Implementations
Implementations are downstream of frozen contracts. Implementation behavior must not silently redefine the contract.

---

## 17. Naming Convention

Canonical artifacts should prefer: `DOMAIN-SCOPE-TYPE-NUMBER`

Examples:
- `TSCP-CANON-001`
- `P0-ARTIFACT-REFERENCE-SPEC-001`
- `P0-CANONICAL-SERIALIZATION-SPEC-001`

Version information should remain separate from the stable artifact identifier where practical.

---

## 18. Encyclopedia Architecture

This acronym key should serve as Volume 0 / Index Layer of the broader Triune-Oracle Encyclopedia.

Suggested future volumes:

| Volume | Topic |
|--------|-------|
| I | Ontology — entities, states, relations, properties, semantic categories |
| II | Protocols — TSCP and related protocol contracts |
| III | Evidence & Admissibility — FCO, admissibility, receipts, provenance, evidence boundaries, semantic non-invention |
| IV | Observation & Integrity — SHARK, INTEGRITY, observation domains, MinObs, ObsDepth, lattice structure, counterexamples |
| V | Kernel & Mathematics — NTT, DIT, DIF, SIMD, AVX-512, NEON, Montgomery arithmetic, field representations, formal proofs |
| VI | Architecture — Custody Plane, Evolution Plane, Audit Plane, authority boundaries, execution boundaries, system components |
| VII | Formal Verification — Lean formalization, theorem libraries, proof obligations, verification predicates, mechanically checked contracts |
| VIII | Artifact & Provenance — Canonical serialization, artifact references, hashes, receipts, evidence chains, custody transitions |
| IX | Implementation — Repositories, modules, feature gates, test suites, CI gates, benchmarks, implementation mappings |
| X | Research & External Interface — Grant terminology, invention inventory, patent terminology, external correspondence, research claims |

---

## 19. Maintenance Rule

Every newly introduced acronym should be added to this index at the moment it becomes operationally significant, rather than retrospectively after terminology has spread.

Before introducing a new acronym, check:

1. Does an existing term already describe the concept?
2. Does the proposed acronym collide with an existing term?
3. Is the term a subsystem, property, contract, artifact, observation domain, or merely a descriptive label?
4. Does the literal expansion accurately describe the canonical meaning?
5. Does the acronym accidentally imply authority, truth, certification, or another stronger semantic property than intended?
6. What artifact will be authoritative for its definition?
7. What is its lifecycle status?

The goal is not to maximize the number of acronyms. The goal is to make every acronym semantically expensive to misuse and cheap to understand.

---

## 20. Master Index

| Acronym / Term | Canonical Expansion | Domain | Status |
|---|---|---|---|
| TO | Triune-Oracle | System | Active |
| TSH | Triune System Hive | Architecture | Active |
| TCER | Triumvirate Continuity Engineering Runtime | Runtime | Active |
| TSCP | Telemetry Sign-Off and Concurrency Protocol | Protocol | Frozen family |
| TSCP-FCO | TSCP Field Coherence Object framework | Evidence/Custody | Active |
| FCO | Field Coherence Object | Evidence | Frozen |
| TSCP-AUDIT-CANON | TSCP Audit Canon | Audit/Identity | Active |
| TSCP-PL | TSCP Protocol Layer | Protocol | Active |
| REO | Resonance Evaluation Object | Evaluation | Active |
| AC | Admissibility Contract | Admissibility | Active |
| SNIG | Semantic Non-Invention Gate | Semantics | Candidate |
| SHARK | SHARK observation/evaluation framework | Integrity | Frozen framework |
| O_SHARK | SHARK Observation | Observation | Frozen |
| MinObs | Minimal Observation | Observation | Active |
| ObsDepth | Observation Depth | Observation | Active |
| O₀ | Observation Level 0 | Observation | Frozen |
| O₁ | Observation Level 1 | Observation | Frozen |
| O₂ | Observation Level 2 | Observation | Frozen |
| O₂.₁ | EvidenceLookup observation | Observation | Active |
| O₂.₂ | EdgeSet observation | Observation | Active |
| O₃ | Full Graph Observation | Observation | Frozen |
| Eᵢ→ⱼ | Observation Expansion Relation | Observation | Active |
| CE16 | Counterexample 16 | Integrity | Frozen |
| CE17 | Counterexample 17 | Integrity | Frozen |
| CE18 | Counterexample 18 | Integrity | Frozen |
| NTT | Number-Theoretic Transform | Kernel | Active |
| DIT | Decimation-In-Time | Kernel | Active |
| DIF | Decimation-In-Frequency | Kernel | Active |
| SIMD | Single Instruction, Multiple Data | Kernel | Active |
| AVX-512 | Advanced Vector Extensions 512-bit | Kernel | Active |
| NEON | ARM Advanced SIMD | Kernel | Active |
| MR | Montgomery Reduction | Mathematics | Active |
| P0 | Priority-0 foundational specification | Specification | Active |
| TSCP-CANON-001 | TSCP Canonical Artifact Specification | Artifact | Frozen |
| Authority | Authority capability | Architecture | Canonical concept |
| Evidence Boundary | Evidence scope boundary | Evidence | Canonical concept |
| Custody Plane | Evidence/state custody plane | Architecture | Active |
| Evolution Plane | System evolution plane | Architecture | Active |

---

## 21. Canonical Principle

The vocabulary is part of the architecture.

As the system becomes more formally specified, terminology is no longer merely documentation. Definitions determine what distinctions the system is capable of making, what claims an artifact is permitted to carry, what transitions are admissible, and where authority does — or does not — exist.

Accordingly, this lexicon should be treated as a maintained architectural artifact rather than a casual glossary.
