# Volume I — Ontology

## Triune-Oracle Encyclopedia

**Volume:** I
**Title:** Ontology
**Status:** Draft v0.1
**Date:** 2026-08-26
**Depends on:** Volume 0 (NOMENCLATURE.md — Index Layer)

---

## 1. Purpose

This volume defines the foundational ontology of the Triune-Oracle system: what kinds of things exist, how they relate, what properties they carry, and what semantic distinctions separate them.

The ontology is not a specification. It does not define contracts or behavior. It defines categories — the conceptual scaffolding that specifications, implementations, and evidence artifacts occupy.

Where a specification and this ontology appear to conflict, the specification governs. This volume should then be corrected.

---

## 2. Entity Types

Entities are the kinds of things that exist in the Triune-Oracle system. Each entity type has a distinct ontological status.

### 2.1 Artifact

A persistent, byte-addressable object with a SHA-256 identity.

- **Identity:** SHA-256 of actual bytes (not path, not filename, not model assertion)
- **Examples:** A specification file, a source code file, a test file, a golden vector, a manifest
- **Critical distinction:** An artifact's identity is its content hash. Its location is not its identity. A path is not an identity. A filename is not an identity. A model saying "the file exists" is not an identity.
- **Governing specification:** P0-ARTIFACT-REFERENCE-SPEC-001

### 2.2 Artifact Reference

A structured reference to an artifact that carries enough information to resolve the artifact to bytes.

- **Fields:** `artifact_id`, `declared_sha256`, `source_kind`, `source_location`, `namespace`
- **Critical distinction:** A reference is not the artifact. A reference declares an expected identity; resolution determines whether the bytes at the location match that declaration.
- **Governing specification:** P0-ARTIFACT-REFERENCE-SPEC-001

### 2.3 Evidence

An observation or record that can support or refute a claim about an artifact, event, or state.

- **Critical property:** Evidence may support a decision without possessing authority to make the decision.
- **Critical distinction:** Evidence ≠ Authority. AdmittedEvidence means admissible, not necessarily true.
- **Related:** AdmittedEvidence, Evidence Boundary, FCO

### 2.4 Receipt

A structured record documenting an event, transition, artifact, or evidence claim according to the applicable receipt contract.

- **Properties:** `previous_receipt_hash` (chains to predecessor), `base_receipt_hash` (anchors to workspace history head)
- **Critical distinction:** A receipt is evidence about a declared event. It is not automatically authority or truth.
- **Invariants:** Receipt history does not roll back when transactional state rolls back. `#7 ABORT → receipt head = #8 → #9 chains from #8`.

### 2.5 Contract

A frozen specification that defines behavior, structure, or semantics that downstream implementations must satisfy.

- **Examples:** P0-CANONICAL-SERIALIZATION-SPEC-001, P0-ARTIFACT-REFERENCE-SPEC-001, P0-RESOLVER-SPEC-001
- **Critical distinction:** Contracts govern implementations. Implementation behavior must not silently redefine the contract.
- **Authority:** A contract is authoritative about what it specifies. The lexicon is not authoritative about contracts — it records what the names mean and where authority lives.

### 2.6 Authority

The capability or standing to authorize, execute, approve, promote, or otherwise cause an action according to a declared authority model.

- **Critical property:** Authority is an architectural capability, not a property automatically produced by evidence or observation.
- **Foundational invariant:** Authority follows verified state; verified state follows evidence; evidence never derives its own authority.
- **Three corollaries:**
  1. A declared state may constrain authority, but a declaration cannot itself grant authority.
  2. No component should manufacture its own authority merely by producing a claim about itself.
  3. Absence of evidence is not evidence of absence.

### 2.7 Observation

The information exposed to an evaluator.

- **Critical distinction:** Observation ≠ Authority. An evaluator seeing information does not thereby acquire authority over the object being observed.
- **Structure:** Observations form a lattice (partially ordered set), not necessarily a linear hierarchy. Different observation expansions may be incomparable.
- **Related:** O_SHARK, MinObs, ObsDepth, Observation Lattice

### 2.8 Agent

A system component that acts within the Triune-Oracle architecture.

- **Examples:** Legio (orchestration), Watchtower (monitoring), Memory Core (persistence), Vaultfire (subsystem), Codex (knowledge corpus)
- **Critical distinction:** Agents are implementation-level entities. Their contracts are defined by their governing artifacts, not by the lexicon.

---

## 3. States

States are the distinct conditions an entity can occupy. The system maintains strict separation between different state dimensions.

### 3.1 Custody States

The epistemic status of an artifact's byte identity.

| State | Meaning |
|-------|---------|
| UNVERIFIED | No independent byte-resolution has been performed |
| OBSERVED | Bytes have been read but identity not yet confirmed |
| VERIFIED | Independent byte-resolution + hash recomputation + comparison passed |
| FAILED | Verification attempted and identity mismatch detected |
| FROZEN | Verified + persistent evidence artifact + immutable reference established |

- **Critical distinction:** Custody state is about whether we have epistemic grounds for believing an artifact's bytes are what they claim to be. It is NOT about whether the object is part of a transaction.
- **Promotion rule:** No independently resolvable bytes = no byte-identity verification = no VERIFIED/FROZEN promotion.
- **Fail-closed:** The resolver cannot promote custody by construction.

### 3.2 Transaction States

The transactional status of an object within a prepare/commit cycle.

| State | Meaning |
|-------|---------|
| NONE | Not part of any active transaction |
| STAGED | Prepared against a specific workspace history head |
| COMMITTING | Transition in progress |
| COMMITTED | Transition completed successfully |
| ABORTED | Transition rejected; transactional state rolls back |

- **Critical distinction:** Transaction state is about whether the object is part of a transaction. It is NOT about whether we have epistemic grounds for believing its bytes.
- **Rollback rule:** Rollback restores transactional state. It does not roll back receipt history.
- **Separation:** Custody state and transaction state are orthogonal dimensions. The system must not confuse "this object is part of a transaction" with "we have epistemic grounds for believing this artifact's bytes."

### 3.3 Provenance States

The evidential status of a claim about the system's history.

| State | Meaning |
|-------|---------|
| ESTABLISHED | Directly supported by recoverable, independently inspectable evidence |
| UNESTABLISHED | Plausible or asserted, but evidence not recovered |
| CONTRADICTED | Available evidence shows the claim cannot be true as stated |

- **Critical distinction:** A claim is not false merely because the artifact doesn't establish it — it is UNESTABLISHED until evidence is recovered. A claim is CONTRADICTED only when positive evidence shows it cannot be true.
- **Governing rule:** Never promote a narrative claim into an established fact merely because an artifact contains the claim. Promote only when an independently inspectable evidence object supports it.

### 3.4 Term Lifecycle States

The canonical status of a terminology entry in the lexicon.

| State | Meaning |
|-------|---------|
| Proposed | Under consideration; not yet canonically frozen |
| Candidate | Under evaluation for formal adoption |
| Active | Currently operative; definition is stable |
| Frozen | Explicitly fixed; changes require revision process |
| Superseded | Replaced by a later artifact; historically valid but not for new specifications |
| Deprecated | Recognizable but should not be used for new artifacts |
| Informal | Useful descriptively; no canonical semantic authority |

---

## 4. Relations

Relations define how entities connect to, depend on, or transform into each other.

### 4.1 Resolution

The process of reading bytes from an authorized source and computing their SHA-256.

```
Artifact Reference → Resolver → Observation (bytes) → Identity Comparison → Verification Result
```

- **Invariants:**
  - INV-REF-001 (Reference Determinacy): A reference deterministically resolves to at most one byte source.
  - INV-REF-002 (Location ≠ Identity): A path is not an identity. A location change does not alias a previous identity.
  - INV-REF-003 (Authorized Source): Only declared source kinds may resolve. Unauthorized locations are rejected.
- **Critical distinction:** Resolution produces an observation. It does not produce custody promotion or authority.

### 4.2 Verification

The process of independently computing SHA-256 of actual bytes and comparing against the declared hash.

- **Independence property A (from the claim):** The verifier does not trust the declared digest. It reads bytes and computes SHA-256(actual_bytes), then compares.
- **Independence property B (from the implementation under test):** If the verifier, tests, and implementation were all written from the same assumptions, "tests pass" does not constitute independent verification. A genuinely independent implementation is required.
- **Recursive custody:** Verification evidence itself is subjected to the resolver/custody boundary. The evidence artifact must be independently resolvable.

### 4.3 Custody Promotion

The transition from one custody state to a stronger one, gated by evidence.

```
UNVERIFIED → OBSERVED → VERIFIED → FROZEN
```

- **Gate:** No independently resolvable bytes = no promotion. No independent verification = no VERIFIED. No persistent evidence artifact = no FROZEN.
- **Two-channel model:** PLAY (proposals, hypotheses, conversation) cannot jump directly to CUSTODY. The path is:
  ```
  PLAY → PERSISTENCE → RESOLVE → OBSERVE → BIND → INDEPENDENT VERIFY → CUSTODY PROMOTION → RECEIPT
  ```
- **Critical invariant:** No independently resolvable bytes = no byte-identity verification = no VERIFIED/FROZEN promotion.

### 4.4 Admission

The process of evaluating evidence against an admissibility predicate.

```
Evidence → Admissibility Contract → Admitted / Rejected
```

- **Critical distinction:** Admissibility ≠ Truth. Satisfying an admissibility predicate means evidence meets declared admission conditions. It does not independently establish truth, authority, correctness, authorization, execution permission, or promotion permission.
- **Identity-first:** Identity is established before an artifact or state can enter subsequent evaluation. The audit plane has authority zero — it cannot approve, authorize, execute, or promote.

### 4.5 Observation Expansion

The transformation that expands one observation domain into another while preserving semantic identity.

```
O₀ ≼ O₁ ≼ O₂ ≼ O₂.₁ ≼ O₃
```

with O₂.₂ forming an incomparable branch relative to O₂ and O₂.₁.

- **Critical distinction:** More observation is not necessarily a linear hierarchy. The observation structure is a lattice (partial order). Different expansions expose different information and may be incomparable.
- **Predicate-relativity:** The observation required to establish one predicate may be insufficient or excessive for another. MinObs is predicate-relative.

### 4.6 Authority Flow

The directional constraint on how authority propagates through the system.

```
Evidence → Verified State → Authority
```

- **Never:** Authority → Evidence (authority cannot produce its own evidence)
- **Never:** Evidence → Authority (evidence cannot grant itself authority)
- **Foundational invariant:** Authority follows verified state; verified state follows evidence; evidence never derives its own authority.

---

## 5. Properties

Properties are characteristics that entities may possess. These are the load-bearing distinctions the system enforces.

### 5.1 Identity

An artifact's identity is the SHA-256 of its actual bytes.

- **Not:** A path, a filename, a model assertion, a declared hash without recomputation, a content-addressed store reference without recompute.
- **Even a recorded SHA-256 is not proof that the bytes producing it exist.** The bytes must be independently resolved and the hash recomputed.

### 5.2 Integrity

Adversarial evaluation over a declared structural-context boundary.

- **Formally:** `O_SHARK ⊆ O_INTEGRITY ⊆ O_global`
- **Experimentally witnessed:** Structural integrity is not a predicate of SHARK-visible observations. CE16–CE18 demonstrate locally indistinguishable states with different integrity properties.
- **Engineering consequence:** Insufficient observation ⇒ cannot establish integrity (not "assume integrity"). The correct response is to expand the observation boundary, not to add more predicates.

### 5.3 Admissibility

Whether evidence satisfies the declared admission conditions for a specified context.

- **Not equivalent to:** Truth, authority, correctness, authorization.
- **AdmittedEvidence means admissible, not necessarily true.**

### 5.4 Fail-Closed

Unrecognized, invalid, or unauthorized transitions are rejected, not interpreted permissively.

- **Missing evidence or invalid state does not silently become acceptance.**
- **The resolver cannot promote custody through the resolver itself.**

### 5.5 Immutability (Frozen)

A frozen artifact or state has been explicitly fixed and should not be changed casually.

- **P0 is frozen:** No modifications. Defects → new revision with explicit delta, not silent edit.
- **Frozen contracts govern implementations.** Implementation behavior must not silently redefine the contract.

### 5.6 Behavioral Verification vs Formal Proof

Two distinct epistemic levels that must not be conflated.

- **Behavioral verification:** Independent implementations agree on behavior across a differential test matrix. This is what P0 currently establishes.
- **Formal proof:** Mechanical, machine-checked proof that the specification itself is correct. This is a FUTURE RESEARCH OBJECTIVE, not current evidence.
- **Why the distinction matters:** In a custody model, independent implementations agreeing is not equivalent to proving the trusted specification. A flawed specification can propagate its flaw into every faithful implementation.

---

## 6. Semantic Distinctions

These are the fundamental invariants that the system enforces. They are global unless explicitly revised by a higher-order specification.

### 6.1 Observation ≠ Authority

An evaluator seeing information does not thereby acquire authority over the object being observed.

### 6.2 Admissibility ≠ Truth

Satisfying an admissibility predicate means evidence satisfies declared admission conditions. It does not independently establish truth.

### 6.3 Evidence ≠ Authority

Evidence may support a decision without possessing authority to make the decision.

### 6.4 Identity ≠ Location

A path is not an identity. A filename is not an identity. A location change does not alias a previous identity.

### 6.5 Resolution ≠ Promotion ≠ Freeze

Resolution produces an observation. Custody promotion requires independent verification. Freeze requires persistent evidence. These are distinct operations with distinct gates.

### 6.6 Implementation ≠ Specification

Implementations are downstream of frozen contracts. Implementation behavior must not silently redefine the contract.

### 6.7 Behavioral Verification ≠ Formal Proof

Independent implementations agreeing on behavior is not equivalent to proving the trusted specification. A flawed spec propagates flaws into faithful implementations.

### 6.8 Authority(FCO) = 0

The FCO is an evidence boundary, not an authority boundary. It does not establish truth, value, authorization, execution authority, or promotion authority.

### 6.9 Audit Authority = 0

The audit/identity admission plane cannot approve, authorize, execute, or promote. Identity precedes evaluation; it does not authorize action.

### 6.10 Type Systems ≠ Complete Security Boundary

Type-level guarantees do not automatically survive serialization, FFI, reflection, persistence, generated code, type erasure, or external representations.

---

## 7. Architectural Planes

The system is organized into planes with explicitly separated responsibilities and authority boundaries.

### 7.1 Custody Plane

Responsible for maintaining and constraining evidence/state custody through declared transitions.

- **Authority:** Does not inherently grant authority to evidence objects.
- **Function:** Controls what may happen to evidence as it moves through the system.

### 7.2 Evolution Plane

Concerned with system evolution/transformation rather than custody authority.

- **Function:** Separates system change from evidence custody and prevents transformation semantics from silently becoming authority semantics.

### 7.3 Audit Plane (TSCP-AUDIT-CANON)

The identity-first audit/admission plane establishing canonical identity before downstream evaluation.

- **Authority:** Zero. Cannot approve, authorize, execute, or promote.
- **Function:** Identity is established before an artifact or state can enter subsequent evaluation processes.

### 7.4 Evidence Plane

The plane in which evidence is produced, observed, and constrained.

- **FCO:** The Field Coherence Object operates here as an evidence boundary (not an authority boundary).
- **Invariant:** Authority(FCO) = 0.

### 7.5 Play Plane

The plane in which proposals, hypotheses, and conversation-generated artifacts exist before persistence and verification.

- **Critical restriction:** PLAY cannot jump directly to CUSTODY. The path requires persistence, resolution, observation, binding, independent verification, custody promotion, and receipt.

---

## 8. Two-Channel Model

The system enforces a structural separation between two channels with different epistemic properties.

### 8.1 Play Channel

Where proposals, hypotheses, and conversation-generated candidate artifacts exist.

- **Epistemic status:** Claims. Not evidence. Not custody.
- **Can produce:** Proposals for artifacts, specifications, tests.
- **Cannot produce:** Custody promotions, verified artifacts, frozen contracts, authority.

### 8.2 Epistemic Channel

Where persistent bytes are resolved, observed, verified, and promoted to custody.

- **Pipeline:**
  ```
  PERSISTENCE → RESOLVE → OBSERVE → BIND → INDEPENDENT VERIFY → CUSTODY PROMOTION → RECEIPT
  ```
- **Gate:** No independently resolvable bytes = no entry into the epistemic channel.

### 8.3 The Critical Property

PLAY cannot jump directly to CUSTODY. This is not merely documented — it is enforced as an architectural boundary. The distinction between play and epistemic is turned into a structural separation with a mandatory pipeline between them.

---

## 9. Naming Conventions for Entity Types

To prevent the ontology from becoming a flat list of acronyms, each term should be classified by what kind of thing it names.

| Entity Type | Description | Examples |
|-------------|-------------|----------|
| thing | A named object or concept | Artifact, Receipt, FCO |
| contract | A frozen specification defining behavior | P0-CANONICAL-SERIALIZATION-SPEC-001 |
| property | A characteristic an entity may possess | Identity, Integrity, Fail-Closed |
| observation_domain | A level of information exposed to an evaluator | O₀, O₁, O₂, O₃, O_SHARK |
| protocol | A defined procedure or interaction pattern | TSCP, TSCP-PL |
| artifact | A persistent byte-addressable object | Golden vectors, test files, manifests |
| test | A verification procedure | CE16, CE17, CE18 |
| architectural_plane | A structural division with separated authority | Custody Plane, Evolution Plane, Audit Plane |
| state | A condition an entity can occupy | UNVERIFIED, VERIFIED, FROZEN, STAGED |
| relation | A connection between entities | Resolution, Verification, Custody Promotion |
| agent | A system component that acts | Legio, Watchtower, Memory Core |
| label | A descriptive name without canonical semantic authority | (informal terms) |

---

## 10. Ontological Rules

1. **Every term in the lexicon should be classified by entity type.** An acronym that names a contract is different from one that names a property or an observation domain.

2. **Contracts and properties are not interchangeable.** A contract defines what must hold. A property is what can be observed to hold. A contract may require a property; a property does not by itself constitute a contract.

3. **States are orthogonal.** Custody state, transaction state, and provenance state are independent dimensions. An artifact can be FROZEN (custody) + NONE (transaction) + ESTABLISHED (provenance) simultaneously.

4. **Authority is directional.** It flows from evidence through verified state to authority — never the reverse. No entity grants itself authority by producing claims about itself.

5. **Observation is predicate-relative.** There is no universally minimal observation. The observation required depends on what question is being asked.

6. **The lexicon is normative about terminology, not authoritative about contracts.** The authority chain is: Lexicon → identifies terminology → points to governing artifact → governing artifact establishes contract → implementation realizes contract → tests/evidence establish what was observed.

---

## 11. Cross-References

| Concept | Defined in Volume | Governing Specification |
|--------|-------------------|------------------------|
| Canonical serialization | I (§5.1 Identity) | P0-CANONICAL-SERIALIZATION-SPEC-001 |
| Artifact reference resolution | I (§4.1 Resolution) | P0-ARTIFACT-REFERENCE-SPEC-001 |
| Resolver behavior | I (§4.2 Verification) | P0-RESOLVER-SPEC-001 |
| Custody state machine | I (§3.1 Custody States) | P0-RESOLVER-SPEC-001 |
| Transaction state machine | I (§3.2 Transaction States) | (Future P1 work — HOLD) |
| Provenance classification | I (§3.3 Provenance States) | Unified Provenance Framework |
| Observation lattice | I (§4.5 Observation Expansion) | SHARK/INTEGRITY audit framework |
| Authority invariant | I (§2.6 Authority, §4.6 Authority Flow) | Foundational invariant (Sean, 2026-08-13) |
| FCO authority zero | I (§6.8, §7.4) | TSCP-FCO constitutional specification |
| Two-channel model | I (§8) | v0.4 generation boundary |
| Behavioral verification vs formal proof | I (§5.6, §6.7) | Epistemic correction (Aria, 2026-08-26) |

---

## 12. Version History

| Version | Date | Changes |
|---------|------|---------|
| Draft v0.1 | 2026-08-26 | Initial ontology: entity types, states, relations, properties, semantic distinctions, architectural planes, two-channel model, naming conventions |
