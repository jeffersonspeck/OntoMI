# From “101” to SABiOx — Evolution at a Glance

OntoMI started as a **101-style** ontology (Noy & McGuinness): lightweight scoping, informal **competency questions (CQs)**, quick concept listing, and direct OWL encoding for fast iteration and demos.

It has since evolved into a **SABiOx**-guided artifact with:

* **Process structure** across phases (Requirements → Setup → Capture → Design → Implementation → Publication), with explicit **supporting activities** (KNO, REU, DOC, MAN, EVA, PUB).
* **Foundational grounding** (BFO/IAO) and OBO-style annotations.
* **Traceability**: CQ → model elements → SPARQL queries → instances → evaluation.
* **Configuration management** (versioning, changelog, releases) and **quality gates** (reasoner checks + SPARQL integrity).

Below you will find a concise menu for each SABiOx phase. Each page briefly recaps the **101 baseline** and documents the **SABiOx extensions** you are using now.

---

## SABiOx Documentation Menu

> All documents live in `docs/` unless noted. Relative links assume repository root.

### 1) Requirements

perfeito — segue o mesmo trecho com **links clicáveis** (relativos ao repo). É só colar no README:

---

### 1) Requirements

* **File:** [`docs/sabiox-requirements.md`](docs/sabiox-requirements.md)
* **What changed vs. 101:** 101 CQs são mantidas, e o SABiOx adiciona **non-functional requirements**, **interoperability goals** e **CQ→Query→Instance** traceability.
* **Includes:** domain & scope; CQ1–CQ3; NFRs; initial evaluation criteria; traceability matrix.

### 2) Setup

* **File:** [`docs/sabiox-setup.md`](docs/sabiox-setup.md)
* **What changed vs. 101:** de escolhas ad-hoc para **seleções explícitas**: **modeling language**, **foundational ontology (BFO/IAO)**, **reuse policy** e **concept inclusion criteria**.
* **Includes:** chosen language (conceptual), foundational patterns, reuse candidates, acceptance criteria.

### 3) Capture (Reference Ontology)

* **File:** [`docs/sabiox-capture.md`](docs/sabiox-capture.md)
* **What changed vs. 101:** além de lista de classes/propriedades, o SABiOx pede **concept cataloging**, **views de ontologias reutilizadas**, **axioms**, **modularization** e um **Reference Ontology Document**.
* **Includes:** concept catalog, ontology views, axioms (informal/formal), modularization diagram, model dictionary.

### 4) Design (Operational Decisions)

* **File:** [`docs/sabiox-design.md`](docs/sabiox-design.md)
* **What changed vs. 101:** explicita **OWL 2 DL profile** e **encoding rules**; define **vocabularies**, **naming/IRI policy** e **module architecture**.
* **Includes:** encoding language, vocabularies (BFO/IAO/…), coding rules, file/module architecture.

### 5) Implementation (Operational Ontology)

* **File:** [`docs/sabiox-implementation.md`](docs/sabiox-implementation.md)
* **What changed vs. 101:** codificação guiada pelo Design; **classes/relations/axioms** com **releases versionadas** e **automação de checks**.
* **Includes:** como o [`ontology/src/ontomi.ttl`](ontology/src/ontomi.ttl) é estruturado; release pipeline; metadata (`owl:versionIRI`, `dct:*`).

### 6) Evaluation & Validation

* **File:** [`docs/sabiox-evaluation.md`](docs/sabiox-evaluation.md)
* **What changed vs. 101:** formaliza **subontology/integration/ontology tests**, **reasoner checks**, **SPARQL para CQ1–CQ3** e (opcional) **SHACL**.
* **Includes:** how to run reasoner; queries em `evaluation/cq/` — [`cq1.rq`](evaluation/cq/cq1.rq), [`cq2.rq`](evaluation/cq/cq2.rq), [`cq3.rq`](evaluation/cq/cq3.rq); integrity queries; acceptance thresholds.

### 7) Publication & Releases

* **File:** [`docs/sabiox-publication.md`](docs/sabiox-publication.md)
* **What changed vs. 101:** padroniza **SemVer**, **CHANGELOG**, **release notes** e artefatos de distribuição.
* **Includes:** layout de [`ontology/releases/`](ontology/releases/); o que incluir (TTL, reports, CQ results); citação & licensing — veja também [`ontology/releases/CHANGELOG.md`](ontology/releases/CHANGELOG.md).

---

## Quick Links (Artifacts & Helpers)

* **Ontology (operational):** `ontology/src/ontomi.ttl`
* **Profiles & policy:** `ontology/profiles/profiles.md`
* **BFO/IAO alignment (summary):** `docs/bfo-alignment.md`
* **Design decisions:** `docs/design-decisions.md`
* **CQ queries:** `evaluation/cq/` (`cq1.rq`, `cq2.rq`, `cq3.rq`)
* **Integrity checks:** `evaluation/consistency/integrity-queries.rq`
* **Examples:** `examples/instances.ttl`
* **Releases:** `ontology/releases/` (`CHANGELOG.md`, per-version `checks/` & `RELEASE-NOTES.md`)
* **Citations:** `citations/references.bib`

---

## How to Read This Repository

1. **Start** with `sabiox-requirements.md` to understand scope, CQs, and NFRs.
2. **Check** `sabiox-setup.md` for foundational choices (BFO/IAO) and reuse policy.
3. **Review** `sabiox-capture.md` to see the reference model decisions and modularization.
4. **Follow** `sabiox-design.md` for encoding rules and OWL profile.
5. **Implement/inspect** `ontology/src/ontomi.ttl` with guidance from `sabiox-implementation.md`.
6. **Validate** with `sabiox-evaluation.md`, running the reasoner and SPARQL (CQ1–CQ3).
7. **Publish** per `sabiox-publication.md`, updating releases and changelog.
