# Changelog

## v0.3 — 2026-09-15

### Changed — Terminology Reconciliation Event (auditable)
- TSCP Literal corrected: "Telemetry Sign-Off and Concurrency Protocol" → "Triune Structured Codex Protocol"
- Authority determination: tscp-anchor README + v2.1.x paper series govern (GOVERNANCE.md: frozen specification governs; lexicon corrects)
- Historical literals preserved for audit: "Telemetry Sign-Off and Concurrency Protocol" (lexicon v0.1, superseded); "Transparent Succinct Computational Proof" (tscp-zkptp phase3 continuity attestation 2026-08-26, conversational, never canonical)
- Rejected/floated (never admitted; recorded here only to close the event): "Traceability / Security / Continuity / Provenance"
- Added "Authority" field to the TSCP entry
- NOMENCLATURE header version reconciled (v0.1 → v0.3)
- Supersession is an explicit state transition, not an erasure; the superseded literal remains historically valid and must not be used in new specifications

### Added — Governance rules
- Terminology State Transitions: transitions between terminology states are explicit; recency alone does not establish supersession; if evidence does not establish the transition, the state remains unresolved and the boundary is reported
- Property rule (general principle; asserts no property as established): "A property is not granted by aspiration, naming, or declaration. It is granted only when the applicable evidence and verification contract justify the transition."

## v0.2 — 2026-08-26

### Added
- Volume I — Ontology (volumes/VOLUME-I-ONTOLOGY.md)
  - Entity types: Artifact, Artifact Reference, Evidence, Receipt, Contract, Authority, Observation, Agent
  - States: Custody (UNVERIFIED→OBSERVED→VERIFIED→FAILED/FROZEN), Transaction (NONE→STAGED→COMMITTING→COMMITTED/ABORTED), Provenance (ESTABLISHED/UNESTABLISHED/CONTRADICTED), Term Lifecycle
  - Relations: Resolution, Verification, Custody Promotion, Admission, Observation Expansion, Authority Flow
  - Properties: Identity, Integrity, Admissibility, Fail-Closed, Immutability, Behavioral Verification vs Formal Proof
  - Semantic distinctions: 10 canonical rules (Observation≠Authority, Admissibility≠Truth, etc.)
  - Architectural planes: Custody, Evolution, Audit, Evidence, Play
  - Two-channel model: Play → Persistence → Resolve → Observe → Bind → Independent Verify → Custody Promotion → Receipt
  - Naming conventions for entity types (12 categories)
  - Term-entry JSON schema (schemas/term-entry.schema.json)

## v0.1.1 — 2026-08-26

### Changed
- Added explicit governance rule: lexicon is normative about terminology, not authoritative about contracts (Aria)
- Added authority chain to README and GOVERNANCE: Lexicon → governing artifact → contract → implementation → tests/evidence
- Prevents the glossary from becoming a second, conflicting specification

## v0.1 — 2026-08-26

Initial canonical lexicon established.

### Added
- Core system terms: TO, TSH, TCER
- Continuity and protocol terms: TSCP, TSCP-FCO, FCO, TSCP-AUDIT-CANON, TSCP-PL
- Evidence and admissibility terms: REO, AdmittedEvidence, Admissibility Contract (AC), SNIG
- Observation and integrity terms: INTEGRITY, SHARK, O_SHARK, MinObs, ObsDepth, O₀–O₃, O₂.₁, O₂.₂
- Observation lattice: 𝒪, Eᵢ→ⱼ
- Counterexample terms: CE16, CE17, CE18
- Kernel/mathematical terms: NTT, DIT, DIF, SIMD, AVX-512, NEON, Montgomery Reduction, R, SimdField<16>
- Proof/formalization terms: Lean, P0, P0-CANONICAL-SERIALIZATION-SPEC-001, P0-ARTIFACT-REFERENCE-SPEC-001
- Custody/state terms: Custody Plane, Evolution Plane, Fail-Closed
- Artifact/evidence terms: TSCP-CANON-001, SHA256SUMS, Receipt, Evidence Boundary
- Architectural semantics: Authority, Observation, Semantic Laundering, Type-Level Enforcement
- Agent/system components: Legio, Watchtower, Memory Core, Vaultfire, Codex
- Status vocabulary: Proposed, Candidate, Active, Frozen, Superseded, Deprecated, Informal
- Canonical semantic rules (16.1–16.10)
- Naming convention
- Encyclopedia architecture (10 planned volumes)
- Maintenance rule
- Master index table
