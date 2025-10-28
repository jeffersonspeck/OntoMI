# OntoMI — Acceptance Criteria and Measurement Plan (SABiOx)

> Version: 1.0 · Scope: logical quality, CQ coverage, interoperability (BFO/IAO), reuse and sustainability.

## 1. Acceptance criteria

### 1.1 Logical consistency (mandatory)
- **AC-01** Reasoner (HermiT/ELK) reports **no unsatisfiable classes** and **no inconsistencies**.
- **Metric**: *Pass/Fail* (build fails if it fails).

### 1.2 Competency Questions (CQs) coverage
- **AC-02** Canonical queries **CQ1–CQ3** return **non‑empty** results for the gold sets.
- **AC-03** For CQ1 and CQ3, the set of activations returned **matches** the expected set per fragment.
- **Metrics**:
  - **Precision** = (# correct activations / # returned activations)
  - **Recall** = (# correct activations / # expected activations)
  - **F1** = 2·(Precision·Recall)/(Precision+Recall)

### 1.3 Annotation quality (OBO‑style)
- **AC-04** ≥ **95%** of **classes** with `rdfs:label`, `IAO:0000115` (definition), `dcterms:source` (when applicable).
- **AC-05** ≥ **95%** of **properties** with `rdfs:label`, `rdfs:comment` (operational definition), explicit domain/range.
- **Metrics**: % coverage per entity type.

### 1.4 BFO/IAO conformance (interoperability)
- **AC-06** Explicit mappings:  
  - `ExplanationFragment` and elements **subClassOf** IAO:Information Content Entity;  
  - `IntelligenceActivation` **subClassOf** BFO:Occurrent;  
  - `Intelligence` modeled as a stable conceptual type (generically dependent continuant), per reference doc.
- **Metric**: *Pass/Fail* + minimal‑axioms checklist.

### 1.5 Essential axioms
- **AC-07** Disjointness among `Keyword`, `ContextObject`, `DiscursiveStrategy`.  
- **AC-08** `hasType` as an `owl:FunctionalProperty`.  
- **AC-09** Minimal domain/range: `usesElement`, `evokesIntelligence`, `hasActivation`, `refersTo`.  
- **Metric**: *Pass/Fail* via ROBOT/SPARQL report.

### 1.6 Data validation (SHACL)
- **AC-10** 100% of gold sets **pass** `shapes/ontomi.shacl.ttl` (presence of types, links and expected literals).
- **Metric**: *Pass/Fail* + % conformance.

### 1.7 Sustainability / engineering
- **AC-11** Release includes: OWL/TTL + `queries/` + `shapes/` + `examples/` + `docs/` (user guide & traceability) + `CITATION.cff` + `LICENSE`.
- **AC-12** Semantic `CHANGELOG.md` (semver) and CI badges (“Build/Reasoner/Queries”).  
- **Metric**: *Pass/Fail* via release checklist.

---

## 2. Measurement plan

### 2.1 Test artifacts
- **Gold sets** in `examples/`:
  - `fragment_newton_01.ttl`: includes `Keyword`, `ContextObject`, `DiscursiveStrategy`; activations **Kinesthetic (primary)**, `Musical`, `Logical‑mathematical`, `Interpersonal`.
  - `fragment_newton_02.ttl`: variant without sonic elements; expected drop in `Musical`.
- **SHACL shapes**: `shapes/ontomi.shacl.ttl` — ensures minimal shape of instances.
- **Queries**: `queries/cq1.rq`, `queries/cq2.rq`, `queries/cq3.rq`.

### 2.2 Procedure (recommended CI)
1. **Build**: load OntoMI + imports (BFO/IAO).  
2. **Reasoner**: classify and check consistency (HermiT/ELK).  
3. **ROBOT report**: minimal policies (domain/range, disjointness, functionality).  
4. **SHACL**: validate `examples/*.ttl`.  
5. **SPARQL (CQs)**: run `queries/*` over the gold sets.  
6. **Scoring**: compare results with *expected outputs*:
   - `expected/cq1_fragment_newton_01.tsv`
   - `expected/cq2_fragment_newton_01.tsv`
   - `expected/cq3_fragment_newton_01.tsv`
7. **Publish** reports under `reports/` and **badges** in README.

### 2.3 Target metrics (thresholds)
- **Consistency**: Pass.  
- **CQs**: Precision ≥ **0.95**, Recall ≥ **0.95**, F1 ≥ **0.95** on gold sets.  
- **OBO‑style**: label/definition/source coverage ≥ **0.95** for classes and ≥ **0.95** for properties.  
- **SHACL**: 100% conformant.  
- **Release**: all **AC‑11** items present.

### 2.4 Outputs & audit
- **`reports/`**:  
  - `reports/reasoner.txt`, `reports/robot-report.txt`  
  - `reports/shacl/*.ttl`  
  - `reports/queries/cq*.tsv` + comparison with `expected/*.tsv`  
- **README badges**: *Build*, *Reasoner OK*, *CQs OK*, *SHACL OK*.

---

## 3. Roles & cadence
- **Technical owner**: maintains ontology/axioms, reviews CQs and gold sets.  
- **Quality reviewer**: checks OBO‑style, BFO/IAO, SHACL and release.  
- **Cadence**: on every relevant commit and **before each release** (at least monthly).
