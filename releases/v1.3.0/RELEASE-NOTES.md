# Release Notes — OntoMI v1.3.0
**Date:** 2026-01-07

## Summary

This release consolidates the modeling stance that **the ExplanationDocument represents the total text** and that all competency-question reporting should be **document-first**. The main change is the **unification of the profile vector naming/attachment**: the ontology and tooling now treat it simply as a **profile vector** (`onto:hasProfileVector`), including at the **document level**, and CQ outputs now always include (1) **document-level main intelligence** and (2) the **fragment breakdown**.

## Highlights

* **Unified Profile Vector semantics (no “document vector” naming)**

  * Reframed as **vector/profile vector** (generic), instead of “document profile vector”.
  * The document total now links its aggregated MI profile using **`onto:hasProfileVector`** (instead of a document-specific vector property naming in the narrative/tooling).

## Backward Compatibility

* **Data compatibility:** existing instances remain compatible **as long as a document has an aggregated MI vector reachable via `onto:hasProfileVector`** (or migrated to it).
* **Behavioral change:** CQ reports are now **document-first**, which may change the expected output format for downstream consumers (parsers/tests that assumed fragment-only headers).

## Upgrade Guide

1. **Ensure the document total has the aggregated vector linked via `onto:hasProfileVector`.**

   * Document → `onto:hasProfileVector` → `onto:MIProfileVector` (aggregated).
2. **Keep fragments linked and still emit fragment vectors normally** (if you use them):

   * Fragment → `onto:hasProfileVector` → `onto:MIProfileVector` (fragment-level).
3. **Update any scripts/readers** that parse CQ text outputs:

   * They must handle a **document header section** before fragment sections.

## Notes for Tooling

* The S6 CQ runner was updated so the competency questions are answered **with the document as the primary scope**: document summary + fragment evidence.
* The “document total” view makes it easier to report a single **main intelligence for the full text**, without losing fragment explainability.

## Credits

* Continuation of the modeling alignment introduced in v1.2.0x (BFO/IAO alignment, SHACL constraints), now extended with a document-first reporting convention and unified vector semantics.
