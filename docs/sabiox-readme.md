# OntoMI — SABiOx Readme

This repository packages **OntoMI** following the **SABiOx** (Extended Systematic Approach for Building Ontologies) life-cycle.  
It preserves the 101-built operational core and documents the evolution to a mature, interoperable artifact grounded on **BFO** and **IAO**, with OBO-style annotations.

> Key refs: Noy & McGuinness (101), ISO/IEC 21838-2 (BFO), BFO-2020 site, IAO (OBO Foundry), Arp–Smith–Spear, Aguiar & Souza (SABiOx). See `citations/references.bib`.

---

## 1) Repository layout

```
.
├── ontology/
│   ├── src/
│   │   └── ontomi.ttl                 # operational ontology (main, in Turtle)
│   ├── profiles/
│   │   └── profiles.md                # OWL profile, IRIs, naming, annotation policy (OBO-style)
│   └── releases/
│       ├── vX.Y.Z/
│       │   ├── ontomi.ttl
│       │   ├── checks/                # reasoner reports, SPARQL validation
│       │   └── RELEASE-NOTES.md
│       └── CHANGELOG.md
├── docs/
│   ├── bfo-alignment.md               # mapping OntoMI ↔ BFO/IAO (classes & properties)
│   ├── design-decisions.md            # rationale for modeling choices
│   ├── cq-guide.md                    # CQ1–CQ3 queries + how to run them
│   ├── evaluation-plan.md             # metrics, datasets, acceptance criteria
│   └── sabiox-readme.md               # (this document; duplicate kept in /docs for GitHub Pages)
├── evaluation/
│   ├── cq/
│   │   ├── cq1.rq                     # “which intelligences are evoked in a fragment?”
│   │   ├── cq2.rq                     # “which elements contributed to each evocation?”
│   │   └── cq3.rq                     # “which intelligence is most intense (primary)?”
│   ├── consistency/
│   │   └── integrity-queries.rq       # domain/range/functional/disjointness checks
│   └── tests/
│       └── regression.md              # how to run repeatable checks per release
├── examples/
│   ├── instances.ttl                  # canonical instances (e.g., Newton’s First Law example)
│   └── shapes/                        # optional SHACL/SHEXC shapes (if adopted; create if needed)
├── datasets/
│   └── demo/                          # small corpora for demonstration & evaluation
├── citations/
│   └── references.bib                 # BibTeX (BFO/IAO/101/SABiOx/etc.)
└── README.md                          # short project overview for newcomers
```

> **Note**: Per your decision, there is **no** separate `alignments.ttl`. The BFO/IAO alignment is *embedded in the main ontology* (`ontology/src/ontomi.ttl`). The mapping is documented in `docs/bfo-alignment.md`.

---

## 2) SABiOx life-cycle traceability

### Requirements
- **Artifacts**: `docs/cq-guide.md`, `docs/evaluation-plan.md`
- **Content**: domain/scope, **CQ1–CQ3** as functional requirements, non-functional goals (interoperability, quality metrics), traceability CQ → SPARQL → instances.

### Setup
- **Artifacts**: `docs/bfo-alignment.md`, `ontology/profiles/profiles.md`, `docs/design-decisions.md`
- **Content**: foundational ontology = **BFO** (ISO/IEC 21838-2) + **IAO** for information artifacts; IRIs & naming; acceptance criteria for concepts & properties; reuse policy.

### Capture
- **Artifacts**: `ontology/src/ontomi.ttl` (maintained by you), `docs/design-decisions.md`
- **Content**: classes, hierarchies, properties, axioms; disjointness; domain/range minimality; BFO-guided analysis (continuant/occurrent; ICE; dispositions).

### Design
- **Artifacts**: `ontology/profiles/profiles.md`, `docs/evaluation-plan.md`
- **Content**: OWL 2 DL profile; OBO-style annotations; versioning policy; design for heuristics queries and **MI vector** result artifact (8-position vector from `hasActivationScore`).

### Implementation
- **Artifacts**: `ontology/releases/`, `evaluation/` (CQ SPARQLs, consistency checks), `examples/instances.ttl`
- **Content**: operational TTL; canonical instances; automated checks (reasoners + SPARQL); changelog; release notes; publication instructions.

### Supporting activities (consolidated)
Knowledge acquisition; documentation; configuration management; evaluation; reuse; publication. See `docs/` and `ontology/releases/`.

---

## 3) BFO/IAO alignment (summary)

- **Top-level**: BFO distinguishes **continuants** vs **occurrents**.  
- **Information**: explanatory artifacts (fragments/elements) as **IAO:Information Content Entity** (ICE; generically dependent continuant).  
- **Events**: `IntelligenceActivation` as **BFO:process** (occurrence).  
- **Results**: `MIVector` as **IAO:Data item/Data set** (8-position vector from activation scores).  
- **Aboutness**: evidence/activations use **IAO:is_about** to connect content to `Intelligence` (concept).  
Full mapping in `docs/bfo-alignment.md`.

---

## 4) Validation

- **Reasoner**: HermiT/Pellet/ELK on `ontology/src/ontomi.ttl`.
- **CQs**: run SPARQL in `evaluation/cq/*.rq` against ontology + `examples/instances.ttl`.
- **Integrity**: `evaluation/consistency/integrity-queries.rq`.

---

## 5) MI vector artifact

- Class: `MIVector` (IAO data item).
- Link: `hasMIVector(ExplanationFragment, MIVector)`.
- Data: eight decimals via `hasVectorPosition` (fixed order documented in `docs/cq-guide.md`).
- Source: aggregated from `hasActivationScore` on each `IntelligenceActivation`.

---

## 6) Versioning & releases

- Semantic versioning `vMAJOR.MINOR.PATCH`.
- Each release: `ontomi.ttl`, reasoner report, CQ results, `RELEASE-NOTES.md`.
- Summaries in `ontology/releases/CHANGELOG.md`.

---

## 7) How to cite

Citations are prepacked in `citations/references.bib` (BFO/IAO/101/SABiOx/etc.).

---

## 8) Contributing

1. Fork and create a feature branch.
2. Edit `ontology/src/ontomi.ttl` (BFO/IAO alignment lives inside the file).
3. Adjust CQ queries or tests in `evaluation/`.
4. Run reasoner + SPARQL checks; attach a brief report in PR.
5. Follow naming/annotation rules in `ontology/profiles/profiles.md`.

---

© OntoMI contributors. See `LICENSE` for terms.
