# OntoMI — An Ontology for Multiple Intelligences in Texts
[![versão](https://img.shields.io/badge/vers%C3%A3o-1.3.0-blue?style=flat-square)](#)
[![formato](https://img.shields.io/badge/formato-OWL%20%2F%20TTL-0B7285?style=flat-square)](https://www.w3.org/TR/owl2-overview/)
[![base](https://img.shields.io/badge/base-BFO%20%2B%20IAO-6C757D?style=flat-square)](https://basic-formal-ontology.org/)

**OntoMI** is a domain ontology (OWL 2, Turtle) developed in a Master’s dissertation to represent how explanatory fragments of educational texts evoke **Multiple Intelligences (MI)**.  
The project began as a prototypical artifact built with **Ontology Development 101** and was **evolved under SABiOx** to a mature, documented, and interoperable ontology **grounded on BFO 2020** and **IAO (OBO Foundry)**.

---

## What is OntoMI?

OntoMI models:
- **ExplanationFragment**: the textual unit of analysis (sentence/paragraph).
- **ExplanationElement** *(abstract)* with three specializations used as evidence:
  - **Keyword**, **ContextObject**, **DiscursiveStrategy**.
- **Intelligence**: the MI categories.
- **IntelligenceActivation**: the reified activation event inferred for a fragment.

The ABox may store **per-intelligence scores** and a derived **MI vector**:
- `onto:hasActivationScore`: (functional) score per intelligence activation.
- `onto:miVector`: 8-position vector (percentages), derived from scores.

---

## Why BFO/IAO?

OntoMI is **founded on BFO 2020** (ISO/IEC 21838-2) and reuses **IAO**:
- Clear separation of **occurrents** (e.g., `IntelligenceActivation`) and **information content entities** (e.g., `ExplanationFragment`).
- OBO-style annotations for definitions, provenance, and editor notes.
- Interoperability and reuse across the OBO/BFO ecosystem.

References are listed in [`citations/references.bib`](citations/references.bib).

---

## Where it comes from (Master’s)

The ontology, rationale, and evaluation (competency questions, instances, and queries) were produced as part of a Master’s dissertation in Informatics in Education, focusing on **heuristic inference** of MI from explanatory discourse.

---

## How it works (in brief)

1. **Model (TBox)**  
   Classes and properties represent fragments, evidence elements, MI categories, and activations; axioms are aligned to BFO/IAO.

2. **Population (ABox)**  
   Text fragments are instantiated with evidence elements. Heuristic rules (external to the OWL TBox) or analytics compute activations and **scores**; the optional **`onto:miVector`** materializes the 8 MI percentages.

3. **Query/Validation**  
   SPARQL queries cover competency questions CQ1–CQ3; integrity checks verify disjointness, domains/ranges, and functional properties.

---

## Repository Structure

```
.
├── ontology/
│ ├── src/
│ │ ├── ontomi.ttl                # operational ontology (main)
│ │ ├── alignments.ttl            # BFO/IAO alignment axioms (subClassOf/subPropertyOf)
│ │ ├── modules/                  # optional modules (e.g., elements/, activations/, vector/)
│ │ └── patterns/                 # reusable fragments (annotation patterns, aboutness, data-vec)
│ ├── profiles/
│ │ └── profiles.md               # OWL profile, IRIs, naming, annotation policy (OBO-style)
│ └── releases/
│   ├── vX.X.X/
│   │ ├── ontomi.ttl
│   │ └── RELEASE-NOTES.md
│   └── CHANGELOG.md
├── docs/
│ ├── bfo-alignment.md            # mapping OntoMI ↔ BFO/IAO (classes & properties)
│ ├── design-decisions.md         # rationale for modeling choices
│ ├── cq-guide.md                 # CQ1–CQ3 queries + how to run them
│ ├── evaluation-plan.md          # metrics, datasets, acceptance criteria
│ └── sabiox-readme.md            # sabiox documentation
├── evaluation/
│ ├── cq/
│ │ ├── cq1.rq                    # “which intelligences are evoked in a fragment?”
│ │ ├── cq2.rq                    # “which elements contributed to each evocation?”
│ │ └── cq3.rq                    # “which intelligence is most intense (primary)?”
│ ├── consistency/
│ │ └── integrity-queries.rq      # domain/range/functional/disjointness checks
│ └── tests/
│ └── regression.md               # how to run repeatable checks per release
├── examples/
│ ├── instances.ttl               # canonical instances (e.g., Newton’s First Law example)
│ └── shapes/                     # optional SHACL/SHEXC shapes (if adopted)
├── datasets/
│ └── demo/                       # small corpora for demonstration & evaluation
├── citations/
│ └── references.bib              # BibTeX (BFO/IAO/101/SABiOx/etc.)
└── README.md                     # short project overview for newcomers
```

---

## Quick start

1. **Open in Protégé**  
   Load `ontology/src/OntoMI.ttl`. Verify consistency with HermiT/ELK.

2. **Explore core CQs**  
   See `docs/competency-questions.md` and run queries from `examples/queries/`.

3. **Inspect BFO/IAO alignment**  
   See `docs/bfo-alignment.md` for the anchoring of OntoMI classes and properties.

4. **Use the scoring & vector**  
   Populate `onto:hasActivationScore` for each activation; optionally emit the 8-slot `onto:miVector` as a derived summary.

---

## Documentation

- **SABiOx overview** → [`docs/sabiox-readme.md`](docs/sabiox-readme.md)  
- **BFO/IAO alignment** → [`docs/bfo-alignment.md`](docs/bfo-alignment.md)  
- **Design decisions** → [`docs/design-decisions.md`](docs/design-decisions.md)  
- **Evaluation plan** → [`docs/evaluation-plan.md`](docs/evaluation-plan.md)  
- **Competency questions guide** → [`docs/cq-guide.md`](docs/cq-guide.md)
- **Competency questions (CQ1–CQ3)** → [`docs/competency-questions.md`](docs/competency-questions.md)

**History & releases**
- **Changelog** → [`releases/CHANGELOG.md`](releases/CHANGELOG.md)  
- **Release notes** → [`releases/v1.1.0/RELEASE-NOTES.md`](releases/v1.1.0/RELEASE-NOTES.md)

---

## How to cite

If you use OntoMI, please cite the repository and the preferred paper.

**Software (this repository):**
- OntoMI — Ontology for Multiple Intelligences. CC-BY-4.0.  
  Repository: https://github.com/jeffersonspeck/OntoMI

**Preferred citation:**
- Speck, Jefferson Rodrigo. *OntoMI: A Ontology for Multiple Intelligences. 2025*.

> We maintain a machine-readable citation file: [`CITATION.cff`](./CITATION.cff).

---

## License

Specify your preferred license (e.g., CC BY 4.0 or BSD-3-Clause) in a `LICENSE` file at the root.
