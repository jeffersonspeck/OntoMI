# Specifications — OntoMI (Ontology for Multiple Intelligences)

> Version: 1.1.0 · Language: OWL (TTL) · Profile: OWL 2 (with BFO/IAO alignment)  
> Repository: https://github.com/jeffersonspeck/OntoMI

This document describes **what each part of the ontology is and does**, how the modules fit together, and how to work with classes, properties, axioms, shapes, queries, and examples.

---

## 1. Purpose & Scope

**OntoMI** formalizes the *semantic representation of Multiple Intelligences (MI) evoked by explanatory educational texts*. The ontology does **not** measure a learner’s MI profile; instead, it **structures the knowledge** needed for external heuristics/rules to infer activations from textual evidence (lexical, contextual, and discursive).

Core capability:
- Represent *explanatory fragments* and their *semantic elements* (keywords, context objects, discursive strategies).
- Link those elements to **MI types** (Intelligence).
- Reify **Intelligence Activation** events with metadata (e.g., primary/secondary), enabling traceable, time-aware reasoning.

---

## 2. Top-Level Alignment (BFO/IAO)

- **BFO** split:  
  - `IntelligenceActivation` ⟶ **Occurrent** (event/process dependent on time and context)  
  - `ExplanationFragment`, `Keyword`, `ContextObject`, `DiscursiveStrategy` ⟶ **Continuant** via **IAO** as **Information Content Entity (ICE)**
- **IAO / OBO-style metadata**: standard annotations, IRIs, authorship, versioning, and reuse conventions.

---

## 3. Namespaces

Suggested (example; adapt to your final IRIs):

```
@prefix onto: <https://w3id.org/ontomi#> .
@prefix bfo:  <http://purl.obolibrary.org/obo/BFO_> .
@prefix iao:  <http://purl.obolibrary.org/obo/IAO_> .
@prefix owl:  <http://www.w3.org/2002/07/owl#> .
@prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:  <http://www.w3.org/2001/XMLSchema#> .
```

---

## 4. Core Classes — *What they are / What they do*

| Class | What it is | What it does |
|---|---|---|
| **`onto:ExplanationFragment`** (IAO:ICE) | A unit of explanatory text (sentence/paragraph). | Anchors all evidence. Links to its semantic elements and to activation events. |
| **`onto:ExplanationElement`** (abstract, IAO:ICE) | Generic container for evidence-bearing units. | Organizes subtypes that contribute to MI evocation. Not instantiated directly. |
| **`onto:Keyword`** ⊆ `ExplanationElement` | Lexical cue (verb/noun/expression). | Points to MI types it can evoke; weakest standalone evidence. |
| **`onto:ContextObject`** ⊆ `ExplanationElement` | Physical/symbolic/situational object. | Grounds the explanation (space/time/interaction). Medium-strength evidence. |
| **`onto:DiscursiveStrategy`** ⊆ `ExplanationElement` | Rhetorical/pedagogical strategy (analogy, dramatization, simulation…). | Structural organizer of the explanation; strongest evidence. |
| **`onto:Intelligence`** | MI category (e.g., Bodily-Kinesthetic, Musical…). | Stable conceptual types used as targets of evocation/activation. |
| **`onto:IntelligenceActivation`** (BFO:Occurrent) | Reified activation event (primary/secondary). | Records that a specific MI was activated for a fragment, with metadata and time-provenance if needed. |

> **Design intent**: keep the **core vocabulary stable** while refining ontological commitments (BFO/IAO), constraints and reasoning friendliness.

---

## 5. Object Properties — *What they connect / Why*

| Property | Domain → Range | Purpose |
|---|---|---|
| **`onto:usesElement`** | `ExplanationFragment` → `ExplanationElement` | Associates a fragment to its evidence elements. |
| **`onto:evokesIntelligence`** | `ExplanationElement` → `Intelligence` | Declares potential MI evocation by a given element. |
| **`onto:hasActivation`** | `ExplanationFragment` → `IntelligenceActivation` | Links a fragment to one or more activation events. |
| **`onto:refersTo`** | `IntelligenceActivation` → `Intelligence` | Points each activation to exactly one MI type. |

**Constraints (OWL-level):**
- Domains/ranges are **minimal and explicit** (BFO/IAO-consistent).
- **Disjointness**: `Keyword` ⟂ `ContextObject` ⟂ `DiscursiveStrategy`.
- **Cardinality**: a fragment may have *multiple* `hasActivation` values (co-activation).

---

## 6. Data Properties — *How they qualify*

| Data Property | Domain → Datatype | Purpose / Notes |
|---|---|---|
| **`onto:hasType`** *(Functional)* | `IntelligenceActivation` → `xsd:string` | Qualifies activation as `primary`/`secondary` (or a controlled vocabulary). Functional for consistency. |
| *(Optional)* `onto:hasScore` | `IntelligenceActivation` → `xsd:decimal` | Store a numeric score derived from heuristics (if used). |
| *(Optional)* `rdfs:label`, `rdfs:comment` | Any entity | Human-readable naming and documentation. |

---

## 7. Axioms & Constraints (Reasoner-Friendly)

- **Subclassing**: `Keyword`, `ContextObject`, `DiscursiveStrategy` ⊆ `ExplanationElement`.
- **Disjointness**: the three subtypes are **explicitly disjoint**.
- **Domains & Ranges**: set to the minimal, correct classes for safe inference.
- **Functional**: `hasType` is `owl:FunctionalProperty`.
- **Reification**: `IntelligenceActivation` captures event-level metadata, time, and referential clarity.

---

## 8. SHACL Shapes

File: `shapes/ontomi.shacl.ttl`

Validate at least:
- Disjointness (`Keyword` vs `ContextObject` vs `DiscursiveStrategy`).
- Functionality of `hasType` (maxCount = 1).
- Minimal domains/ranges for `usesElement`, `evokesIntelligence`, `hasActivation`, `refersTo`.
- Allowed values for `hasType` (e.g., `primary|secondary`).

---

## 9. Competency Questions (CQs) & SPARQL

CQs (examples):
- **CQ1**: Which intelligences are evoked in a given fragment?
- **CQ2**: Which elements (keyword / context / strategy) contributed to each evocation?
- **CQ3**: In multi-activation cases, which intelligence is primary / has stronger evidence?

Place queries in: `queries/cq1.rq`, `queries/cq2.rq`, `queries/cq3.rq`.  
Expected results in TSV: `expected/cq1.tsv`, `expected/cq2.tsv`, `expected/cq3.tsv`.

**Tip**: run a reasoner before executing SPARQL if your queries rely on inferred types/links.

---

## 10. Canonical Examples

Folder: `examples/canonical/*.ttl` — each file **imports** the core ontology and instantiates one explanatory fragment with its elements and activations.

**Minimal pattern (illustrative)**:

```turtle
@prefix onto: <https://w3id.org/ontomi#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:  <http://www.w3.org/2001/XMLSchema#> .

onto:fragment_palmas a onto:ExplanationFragment ;
  rdfs:label "Using claps to mimic constant motion"@en ;
  onto:usesElement onto:kw_ritmo, onto:ctx_ritual, onto:ds_ritual_sonoro ;
  onto:hasActivation onto:act_cin_primary, onto:act_mus_secondary .

onto:kw_ritmo a onto:Keyword ;
  rdfs:label "rhythm"@en ;
  onto:evokesIntelligence onto:Intelligence_Musical .

onto:ctx_ritual a onto:ContextObject ;
  rdfs:label "movement ritual"@en ;
  onto:evokesIntelligence onto:Intelligence_BodilyKinesthetic .

onto:ds_ritual_sonoro a onto:DiscursiveStrategy ;
  rdfs:label "sonic ritual with claps"@en ;
  onto:evokesIntelligence onto:Intelligence_Musical, onto:Intelligence_BodilyKinesthetic .

onto:act_cin_primary a onto:IntelligenceActivation ;
  onto:refersTo onto:Intelligence_BodilyKinesthetic ;
  onto:hasType "primary"^^xsd:string .

onto:act_mus_secondary a onto:IntelligenceActivation ;
  onto:refersTo onto:Intelligence_Musical ;
  onto:hasType "secondary"^^xsd:string .
```

---

## 11. Modules & Project Layout

Recommended structure:

```
ontomi.ttl                      # core ontology (OWL TTL)
queries/
  cq1.rq, cq2.rq, cq3.rq        # SPARQL queries for CQs
expected/
  cq1.tsv, cq2.tsv, cq3.tsv     # expected results (golden files)
examples/
  canonical/
    fragment1.ttl, ...          # canonical instances
shapes/
  ontomi.shacl.ttl              # SHACL shapes (validation)
docs/
  Specifications.md             # this file (or copied into repo)
  traceability.md               # CQ → axioms/queries/instances matrix
CHANGELOG.md                    # SABiOx-aligned release notes
```

---

## 12. Reasoning & Profile

- Works with standard OWL 2 reasoners (HermiT, ELK, FaCT++).  
- Keep axioms conservative to preserve **performance and maintainability**.  
- Use SHACL as complementary **data validation** for instances and editorial rules.

---

## 13. Versioning, Interoperability & Citation

- **Versioning**: semantic versioning; record changes in `CHANGELOG.md`.
- **Interoperability**: BFO/IAO alignment eases mapping and reuse with other OBO/BFO-based ontologies.
- **How to cite** (example BibTeX entry to adapt):

```
@misc{OntoMI,
  title        = {OntoMI: Ontology for Multiple Intelligences},
  author       = {Jefferson Rodrigo Speck and collaborators},
  year         = {2025},
  howpublished = {\url{https://github.com/jeffersonspeck/OntoMI}},
  note         = {Version 1.1.0, OWL (TTL), BFO/IAO aligned}
}
```

---

## 14. Design Rationale (short)

- Reification of activation events (`IntelligenceActivation`) provides **traceability**, **temporal reasoning**, and **metadata hooks**.
- Separation of *content* (IAO:ICE) vs *occurrence* (BFO:Occurrent) clarifies identity/dependencies and supports robust inference.
- Disjoint, typed evidence (`Keyword`, `ContextObject`, `DiscursiveStrategy`) reflects different **strengths of indication** used by heuristic rules.

---

## 15. Quick Start (Protégé)

1. Open `ontomi.ttl` in Protégé.  
2. Import `examples/canonical/*.ttl`.  
3. Run a reasoner (HermiT/ELK).  
4. Execute SPARQL queries in `queries/` and compare with `expected/*.tsv`.  
5. Validate instances with SHACL (`shapes/ontomi.shacl.ttl`).

---

*Footnote:* The full ontology body, tests, canonical instances, and SABiOx artifacts are available at the repository above.
