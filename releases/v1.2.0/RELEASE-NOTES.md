# Release Notes — OntoMI v1.2.0
**Date:** 2025-10-29

## Summary
This release introduces a **SHACL validation layer** aligned with the project’s competency questions and modeling choices. We adopted an **ABox‑light strategy** (“Option B”) that validates `iao:is about` for activations against either **instances of** `onto:IntelligenceDisposition` **or** **class IRIs** that are subclasses of it. The update also adds coherence checks for primary/secondary activations and caps activation scores to \[0,1]. **No breaking changes** to class/property IRIs; existing data remain compatible after minor fixes.

## Highlights
- **New SHACL shapes**
  - `onto:ExplanationElementAdvisoryShape` (**warning**): discourages instantiating `ExplanationElement` directly; prefer `Keyword`, `ContextObject`, or `DiscursiveStrategy`.
  - `onto:ExplanationFragmentShape`: requires at least one `onto:usesElement` **or** `onto:hasActivation`.
  - `onto:IntelligenceActivationShape`:
    - `iao:0000136` (**is about**) must target **≥1** `onto:IntelligenceDisposition` (instance) **or** an IRI whose class is a **subclass** of `onto:IntelligenceDisposition` (ABox‑light validation).
    - `onto:hasActivationType` is **mandatory** with values in `{onto:Primary, onto:Secondary}`.
    - `onto:hasActivationScore` must be an `xsd:decimal` in **\[0,1]**.
    - **SPARQL coherence rules**: any activation linked by `onto:hasPrimaryActivation` must be `onto:Primary`; any linked by `onto:hasSecondaryActivation` must be `onto:Secondary`.
- **Rationale & approach**
  - Keeps the ABox minimal while supporting your pipeline that links activations to **class IRIs** for intelligences.
  - Preserves reasoning friendliness and keeps CQ implementations straightforward.

## Backward Compatibility
- **No breaking changes** to TBox identifiers.
- ABox created with v1.1.0 is compatible; instances missing `onto:hasActivationType` or with scores outside \[0,1] will now be flagged by SHACL.

## Upgrade Guide
1. Import the new SHACL shapes into your ontology module (or keep them in a dedicated `shapes.ttl` and load alongside the ontology).
2. Ensure your activation generation step sets `onto:hasActivationType` for primaries/secondaries and writes `onto:hasActivationScore` in \[0,1].
3. If you link activations via `iao:0000136` to **class IRIs** (e.g., `onto:SpatialIntelligence`), you’re covered by Option B.
4. Run the SHACL validator and address any findings (typically missing types or out‑of‑range scores).

## Notes for Tooling
- The shapes are compatible with common SHACL engines used with RDFLib/TopBraid/Protege SHACL plugins.
- Keep `onto:isAboutFragment` as an auxiliary assertion (optional), but rely on `iao:is about` for compliance checks.

## Credits
- Based on the alignment and documentation introduced in v1.1.0 (BFO/IAO, OBO‑style annotations) and extended with integrity constraints in this release.
