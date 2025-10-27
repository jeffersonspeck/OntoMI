# Release Notes — OntoMI v1.1.0
**Date:** 2025-10-27

## Summary
This release elevates OntoMI from an Ontology Development 101 prototype to a **SABiOx-compliant** artifact with an explicit life cycle, **BFO 2020** + **IAO** foundational alignment, OBO-style annotations, and an evaluation pipeline (CQs, integrity checks, regression outline). The **ABox remains compatible**; the alignment occurs in the TBox with minimal axiomatization.

## Highlights
- **BFO/IAO alignment (TBox):** clear classification of continuants vs. occurrents; information content entities for textual artifacts.
- **Scoring and vectorization:** `onto:hasActivationScore` (functional) + derived `onto:miVector` (8 positions) to report normalized MI activation results.
- **Quality-by-design:** explicit disjointness among explanatory elements; minimal domain/range axioms; functional `onto:hasType`.
- **SABiOx documentation set:** requirements, setup (foundational choice), capture (axioms, modularization), design (profiles/IRIs), and implementation (workflow, evaluation).

## Backward Compatibility
- **No breaking changes** in the core class/property structure from v1.0.0.
- Instances created for v1.0.0 remain valid. New data properties are **optional**.

## Upgrade Guide
1. Replace your ontology file with the v1.1.0 `.ttl` version (keeps class/property IRIs stable).
2. If you compute MI totals, populate `onto:hasActivationScore` per intelligence on the relevant individuals; optionally materialize `onto:miVector` as a comma-separated 8-length literal (or as a datatype supporting vectors, if your stack provides one).
3. Run the provided **SPARQL CQs** and **integrity checks** to verify consistency.
4. Follow the **release workflow** and update `CHANGELOG.md` and `RELEASE-NOTES.md` for subsequent releases.

## Documentation
- SABiOx README, BFO alignment guide, design decisions, evaluation plan, and CQ guide are included under `docs/`.
- Profiles and naming rules are under `ontology/profiles/`.

## Credits and References
- BFO 2020 (ISO/IEC 21838-2), IAO (OBO Foundry), Ontology Development 101, SABiOx guide (NEMO/Ufes), and related literature cited in `citations/references.bib`.
