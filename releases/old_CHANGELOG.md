# Changelog
All notable changes to this project are documented in this file.
This project adheres to [Semantic Versioning](https://semver.org/) and follows the style of [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.2.0] - 2025-10-29
### Added
- **SHACL validation layer** with three shapes:
  - `ExplanationElementAdvisoryShape` (warning severity).
  - `ExplanationFragmentShape` (requires `usesElement` **or** `hasActivation`).
  - `IntelligenceActivationShape` enforcing: `iao:is about` points to an **IntelligenceDisposition** instance **or** a subclass IRI; `hasActivationType` ∈ {`Primary`,`Secondary`}; `hasActivationScore` in **[0,1]**; and SPARQL rules for primary/secondary coherence.
- **ABox‑light validation strategy (Option B)** documented.

### Changed
- Clarified validation semantics so pipelines that link activations to **class IRIs** (e.g., `onto:SpatialIntelligence`) are valid without materializing individuals for each intelligence.

### Fixed
- Typical data issues now flagged by SHACL: missing activation type and out‑of‑range scores.

### Migration
- Populate `hasActivationType` during activation generation and normalize scores to **[0,1]**. Re‑run SHACL and fix any violations.

## [1.1.0] - 2025-09-27
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
- Declared `onto:hasType` as **owl:FunctionalProperty** (already used as such) and documented intended values (primária/ secundária).

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
