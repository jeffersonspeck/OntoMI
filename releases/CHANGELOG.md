# Changelog
All notable changes to this project are documented in this file.
This project adheres to [Semantic Versioning](https://semver.org/) and follows the style of [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.3.0] - 2026-01-07
### Added
- **Document-first reporting convention** for competency questions: CQ outputs now always include **(1) document-level main intelligence** and **(2) fragment breakdown** (S6 runner updated accordingly). :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

### Changed
- **Unified profile vector semantics**: the ontology/tooling now treat it simply as a **profile vector**, including at the **document level**, linked via **`onto:hasProfileVector`** (no “document vector” naming in narrative/tooling). :contentReference[oaicite:2]{index=2}
- **CQ output format** is now **document-first**, which may affect downstream parsers/tests that assumed fragment-only sections. :contentReference[oaicite:3]{index=3} :contentReference[oaicite:4]{index=4}

### Deprecated
- “Document-specific vector” naming in documentation/tooling (prefer the generic **profile vector** phrasing everywhere). :contentReference[oaicite:5]{index=5}

### Migration
- Ensure the **document total** links its aggregated MI vector via:
  - Document → `onto:hasProfileVector` → `onto:MIProfileVector` (aggregated). :contentReference[oaicite:6]{index=6}
- Keep fragment vectors as usual (if you use them):
  - Fragment → `onto:hasProfileVector` → `onto:MIProfileVector` (fragment-level). :contentReference[oaicite:7]{index=7}
- Update any scripts/readers that parse CQ outputs to handle a **document header section** before fragment sections. :contentReference[oaicite:8]{index=8}

## [1.2.0] - 2025-10-29
### Added
- **SHACL validation layer** aligned with the project’s competency questions and modeling choices. :contentReference[oaicite:9]{index=9}
- **New SHACL shapes**
  - `onto:ExplanationElementAdvisoryShape` (**warning**): discourages instantiating `ExplanationElement` directly; prefer `Keyword`, `ContextObject`, or `DiscursiveStrategy`. :contentReference[oaicite:10]{index=10}
  - `onto:ExplanationFragmentShape`: requires at least one `onto:usesElement` **or** `onto:hasActivation`. :contentReference[oaicite:11]{index=11}
  - `onto:IntelligenceActivationShape` enforcing: `iao:0000136` targets an `IntelligenceDisposition` instance **or** a subclass IRI (Option B); `onto:hasActivationType` ∈ {`onto:Primary`, `onto:Secondary`}; `onto:hasActivationScore` in **[0,1]**; and SPARQL coherence rules for primary/secondary consistency. :contentReference[oaicite:12]{index=12}
- **ABox-light validation strategy (Option B)** documented. :contentReference[oaicite:13]{index=13}

### Changed
- Clarified validation semantics so pipelines that link activations to **class IRIs** (e.g., `onto:SpatialIntelligence`) are valid without materializing individuals for each intelligence. :contentReference[oaicite:14]{index=14}

### Fixed
- Typical data issues now flagged by SHACL: missing activation type and out-of-range scores. :contentReference[oaicite:15]{index=15}

### Migration
- Populate `onto:hasActivationType` during activation generation and normalize scores to **[0,1]**. Re-run SHACL and fix any violations. :contentReference[oaicite:16]{index=16}

## [1.1.0] - 2025-10-27
### Added
- **Foundational alignment** to **BFO 2020** (ISO/IEC 21838-2) and **IAO** (OBO Foundry) documented across the TBox.
  - Classes and properties anchored to BFO upper categories (e.g., `IntelligenceActivation` as **occurrent**; `ExplanationFragment` and explanatory elements as **information content entities** via IAO).
  - **OBO-style annotations** (`IAO:0000115` definitions, editor notes, provenance) adopted across ontology terms.
- **Data property `onto:hasActivationScore`** (functional) to register per-intelligence scores at the ABox level.
- **Data property `onto:miVector`** to store the 8-position MI vector (derived from activation scores); documented as optional output for analytics.
- **Design profiles and coding standards**: IRIs, naming conventions, OWL 2 DL profile, and release workflow.
- **Evaluation assets**: SPARQL competency question queries (CQ1–CQ3), integrity checks, and a regression test outline.
- **Documentation set**: SABiOx-oriented README, BFO alignment guide, design decisions, evaluation plan, and CQ guide.

### Changed
- Clarified **domain/range** axioms to the minimum necessary for reasoning, consistent with BFO/IAO commitments.
- Made **disjointness** between `Keyword`, `ContextObject`, and `DiscursiveStrategy` explicit in the TBox.
- Declared `onto:hasActivationType` as **owl:FunctionalProperty** (already used as such) and documented intended values (primária/ secundária).

### Deprecated
- None.

### Removed
- No structural removals. Alignment delivered via documentation and minimal axioms (no separate `alignments.ttl` file).

### Fixed
- Normalized labels and comments to avoid ambiguity; ensured consistent use of Portuguese in class labels per repository convention.

### Security
- N/A.

## [1.0.0] - 2025-06-01
### Added
- Initial OntoMI prototype built with **Ontology Development 101**:
  - Core classes: `ExplanationFragment`, `ExplanationElement` (abstract), `Keyword`, `ContextObject`, `DiscursiveStrategy`, `Intelligence`, `IntelligenceActivation`.
  - Core object properties: `usesElement`, `evokesIntelligence`, `hasActivation`, `refersTo`.
  - Core data property: `hasType` (activation type).
- Example instances for validation and reasoning.

[1.3.0]: https://example.org/ontomi/releases/1.3.0
[1.2.0]: https://example.org/ontomi/releases/1.2.0
[1.1.0]: https://example.org/ontomi/releases/1.1.0
[1.0.0]: https://example.org/ontomi/releases/1.0.0
