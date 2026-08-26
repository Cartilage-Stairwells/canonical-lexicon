# Triune-Oracle Canonical Lexicon

**Status:** v0.1 — Working
**Repository:** `Cartilage-Stairwells/canonical-lexicon` (PUBLIC)
**Date:** 2026-08-26

## What This Is

The canonical terminology, acronym, and nomenclature authority for the Triune-Oracle / Continuity Engineering corpus.

This repository exists to prevent terminology drift as the project expands across specifications, implementations, tests, formal proofs, evidence artifacts, repositories, correspondence, grant materials, and external review.

## What This Is Not

This is **not** a project diary, a specification repository, or an implementation repository.

- **Implementation repositories** → how the thing works
- **Specification repositories** → what the thing must mean and do
- **Canonical Lexicon (this repo)** → what the words themselves mean

The lexicon says what a term means and where its authority comes from. The underlying P0/specification says what the contract actually is. Where a specification and this index appear to conflict, the applicable frozen specification governs — and this document should then be corrected.

## What Belongs Here

- Canonical definitions and relationships
- Acronym expansions
- Domain classifications
- Status designations (Proposed / Active / Frozen / Superseded / Deprecated)
- Cross-references between related terms

## What Does NOT Belong Here

- Private credentials or secrets
- Unpublished strategic correspondence
- Sensitive operational details
- Private research notes
- Anything whose disclosure would materially affect IP strategy
- Unstable brainstorming that hasn't earned canonical status

Public vocabulary ≠ public project diary.

## Structure

```
canonical-lexicon/
├── README.md           — this file
├── NOMENCLATURE.md     — the canonical document (all terms)
├── GOVERNANCE.md       — maintenance rules and lifecycle
├── CHANGELOG.md        — version history
├── terms/              — per-domain term files (when NOMENCLATURE.md becomes unwieldy)
└── schemas/            — term-entry schema
```

## Versioning

| Version | Status | Meaning |
|---------|--------|---------|
| v0.x | Working | Terms may be added, revised, and reclassified |
| v1.0 | Canonical | Core vocabulary frozen; changes require explicit revision process |

A term marked **Frozen** has a canonical definition. A term marked **Active** is currently operational. A term marked **Candidate** has not acquired normative status. A term marked **Superseded** remains historically valid but must not be used for new specifications.

## Maintenance Rule

Every newly introduced acronym should be added to this index at the moment it becomes operationally significant, rather than retrospectively after terminology has spread.

Before introducing a new acronym:
1. Does an existing term already describe the concept?
2. Does the proposed acronym collide with an existing term?
3. Is the term a subsystem, property, contract, artifact, observation domain, or merely a descriptive label?
4. Does the literal expansion accurately describe the canonical meaning?
5. Does the acronym accidentally imply authority, truth, certification, or another stronger semantic property than intended?
6. What artifact will be authoritative for its definition?
7. What is its lifecycle status?

The goal is not to maximize the number of acronyms. The goal is to make every acronym semantically expensive to misuse and cheap to understand.


## Authority Boundary

The lexicon is **normative about terminology, but not authoritative about the underlying technical contract.**

The authority chain:

```
Lexicon → identifies terminology
  → points to governing artifact
  → governing artifact establishes contract
  → implementation demonstrates/realizes contract
  → tests/evidence establish what was actually observed
```

The lexicon records what a name means and where authority lives. The governing specification establishes the contract. Without this distinction, the glossary could accidentally become a second, conflicting specification.

## Canonical Principle

The vocabulary is part of the architecture. As the system becomes more formally specified, terminology is no longer merely documentation — definitions determine what distinctions the system is capable of making, what claims an artifact is permitted to carry, what transitions are admissible, and where authority does or does not exist.

This lexicon is a maintained architectural artifact, not a casual glossary.
