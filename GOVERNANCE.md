# Governance

## Lexicon Governance Rules

### Authority Hierarchy

1. **Frozen specifications** (P0-CANONICAL-SERIALIZATION-SPEC-001, P0-ARTIFACT-REFERENCE-SPEC-001, etc.) — primary authority for contract terms
2. **This lexicon** — terminology authority; must reflect specifications, not override them
3. **Implementations** — downstream of both; cannot redefine contracts or terminology

### When Specifications and Lexicon Conflict

The applicable frozen specification governs. The lexicon must then be corrected to reflect the authoritative definition.


### Normative vs Authoritative (Aria, 2026-08-26)

The lexicon is **normative about terminology**, but **not authoritative about the underlying technical contract**.

The lexicon establishes the meaning of a name and its relationship to the authoritative artifact. It does not establish the contract itself.

The authority chain:

```
Lexicon → identifies terminology
  → points to governing artifact
  → governing artifact establishes contract
  → implementation demonstrates/realizes contract
  → tests/evidence establish what was actually observed
```

Without this rule, someone could read:

> "FCO means X"

and mistakenly conclude:

> "Therefore the lexicon itself establishes the FCO contract."

It doesn't. The FCO contract is established by its governing specification. The lexicon records what the name means and where authority lives.

**Formal rule:** The lexicon may normatively define terminology. It may not authoritatively define contracts, invariants, properties, or behavioral specifications. Those belong to the governing specifications the lexicon points to.

### Adding a New Term

1. Check whether an existing term already describes the concept
2. Verify no acronym collision
3. Classify: subsystem, property, contract, artifact, observation domain, or descriptive label
4. Verify the literal expansion accurately describes the canonical meaning
5. Verify the acronym does not accidentally imply authority, truth, certification, or a stronger semantic property than intended
6. Identify the authoritative artifact for the definition
7. Assign lifecycle status (Proposed / Candidate / Active / Frozen / Superseded / Deprecated)

### Changing a Term's Status

- **Proposed → Candidate:** Initial review complete, concept is under active consideration
- **Candidate → Active:** Concept is operationally used; definition is stable
- **Active → Frozen:** Definition is explicitly fixed; changes require a revision process
- **Frozen → Superseded:** A later artifact replaces the definition; old term remains historically valid but must not be used for new specifications

### What Does NOT Belong in This Repository

- Private credentials or secrets
- Unpublished strategic correspondence
- Sensitive operational details
- Private research notes
- Anything whose disclosure would materially affect IP strategy
- Unstable brainstorming that hasn't earned canonical status

### Boundary Rule

Public vocabulary ≠ public project diary. The lexicon contains definitions and relationships. It does not contain implementation details, strategic plans, or private context.

### Encyclopedia Architecture

This lexicon (NOMENCLATURE.md) serves as Volume 0 / Index Layer. Future volumes may be added as the terminology grows, but the index should remain the canonical entry point.
