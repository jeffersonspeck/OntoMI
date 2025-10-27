# OntoMI — Technical Report Aligned with SABiOx
**Version:** 1.0 • **Date:** 2025-10-27  

**Methodological basis:** SABiOx — *Extended Systematic Approach for Building Ontologies* (Aguiar & Souza, 2024).  
**Foundational alignment:** **BFO/IAO** (operationalized in TTL), with OBO-style identifiers where applicable.  
**Artifact type:** Reference & Operational Ontology Documentation (consolidated).

---

## 0. Executive Summary
This document assesses OntoMI’s current documentation and changes against the **SABiOx** methodology and consolidates a **method-compliant technical report** for the project.  
**Conclusion (fit):** OntoMI’s lifecycle and artifacts **are compatible with SABiOx**. The project has clear **Requirements**, **Setup**, **Capture**, **Design** and **Implementation** outputs; additionally, the SABiOx **supporting activities** (Knowledge Acquisition, Documentation, Configuration Management, Evaluation, Reuse, Publication) are already represented in the **SABiOx Support Activities table** and complementary docs (README, citation, release notes, change log). Minor recommendations are included as “Open items” in each phase.

---

## 1. Method Overview and Roles
**Ontology life-cycle:** Iterative cycles across the phases **Requirements → Setup → Capture → Design → Implementation**, allowing backward revisions and evolution cycles.  
**SABiOx supporting activities:** Knowledge Acquisition (KNO), Documentation (DOC), Configuration Management (MAN), Evaluation (EVA), Reuse (REU), Publication (PUB).

**Roles used in OntoMI (inspired by SABiOx/Scrum):**
- **Ontology Owner:** Jefferson Rodrigo Speck.  
- **Ontology Master / Facilitator:** (assumed) project lead overseeing SABiOx adherence.  
- **Ontology Team:** domain experts in education/MI + ontology engineers.  

---

## 2. Requirements Phase
### 2.1 Define Purpose (REQ-PURP)
- **What:** OntoMI represents **Multiple Intelligences (MI)** conceptualization for **semantic classification of educational resources** and explanation-oriented vectors.  
- **For what:** To support **explainable personalization**, **semantic tagging**, **recommendation**, and **analytics** (e.g., vector-based MI alignment between student profiles and texts).  
- **Why:** Lack of interoperable, well-founded MI representations; need for **BFO/IAO-grounded** conceptual clarity and operational TTL for downstream NLP/LLM pipelines.

**Evidence / Artifacts:** `README.md` (project overview), `CITATION.cff`, prior study protocol and design notes.

### 2.2 Identify and Size Domain (REQ-DOMN)
- **Horizontal boundary:** MI theory (Gardner) as used in **digital educational technologies**; related constructs for **textual explanation fragments**, **discursive strategies**, **context objects**.  
- **Vertical boundary:** Ontology targets **semantic description** of **textual content** (not general learner modeling, not neuropsychometrics). Focus on **operational tagging/instantiation** required by the pipeline.

### 2.3 Elicit Requirements (REQ-ELIC)
- **Functional requirements (FR):**
  - FR1. Represent MI categories and related entities (intelligences, indicators, strategies, evidence).  
  - FR2. Support **sentence/fragment-level** tagging and **explainable vectors** per resource.  
  - FR3. Allow **instantiation** from pipelines (JSON→TTL), with **traceability** of evidence.  
  - FR4. Enable **queries** answering competency questions (CQ1–CQ3; see §7).  
  - FR5. Provide **module-level reuse** and **versioning** for evolution.
- **Non-functional requirements (NFR):**
  - NFR1. **Foundational grounding** (BFO/IAO).  
  - NFR2. **TTL/OWL** encoding; human-readable labels (pt/en).  
  - NFR3. **Performance** for SPARQL queries and batch instantiation.  
  - NFR4. **Documentation/Publication** (open repo, citation, license).  
  - NFR5. **Maintainability** with **CHANGELOG** and **release notes**.

### 2.4 Identify Subdomains (REQ-SUBD)
- **Core MI:** MI categories, relationships, constraints.  
- **Evidence & Annotations:** Explanation fragments, strategies, context objects.  
- **Operationalization:** Pipelines, profiles, vectors, evaluation datasets.

### 2.5 Document & Control & Evaluate (DOC-SPEC, MAN-SPEC, EVA-SPEC)
- **Outputs:** This report + README + CQs; repository version control (Git), periodic review with Owner/Team.  
- **Open items:** Formalize a *single* “Ontology Specification” page in `docs/specification.md` (traceable to FR/NFR).

---

## 3. Setup Phase
### 3.1 Modeling Language (SET-LANG)
- **Choice:** **OntoUML-style conceptual commitments** expressed textually; diagrams optional; final commitment realized in OWL/TTL.

### 3.2 Foundational Ontology (SET-FOUN)
- **Choice:** **BFO/IAO** (OBO style). Rationale: mature commitments, reuse of upper-level categories (**continuants/occurrents**, **information content entity**, etc.).

### 3.3 Concept Criteria (SET-CRIT)
- **Inclusion:** Concepts central to MI operationalization in text; must support tagging → vectorization → query.  
- **Exclusion:** Psychometric test internals; broad pedagogical taxonomies not needed for computational instantiation.

### 3.4 Ontologies to Reuse (SET-REUS)
- **Core:** BFO, IAO.  
- **Domain:** MI domain is purpose-built in OntoMI; external vocabularies may be referenced (e.g., SKOS for labels), as needed.

### 3.5 Document/Control/Evaluate (DOC-REFE, MAN-REFE, EVA-REFE)
- **Outputs:** `docs/bfo-iao-premises.md` (optional), foundational mapping embedded directly in **TTL**.  
- **Open items:** Add a compact *BFO alignment note* inside the TTL header comments.

---

## 4. Capture Phase
### 4.1 Identify Concepts & Axioms (CAP-CONC, CAP-AXIM)
- **Concepts:** MI categories; Evidence fragment; Discursive strategy; Context object; Vector; Profile; Activation; Justification.  
- **Axioms (informal):** e.g., “Every **Activation** is **about** exactly one **ExplanationFragment** and **denotes** one or two **MI** categories.”

### 4.2 Model / Integrate / Modularize (CAP-MODE, CAP-INTE, CAP-MODU)
- **Modules (suggested):**
  - `ontomi-core.ttl` — upper commitments and shared relations.  
  - `ontomi-mi.ttl` — MI categories and structure.  
  - `ontomi-evidence.ttl` — fragments, strategies, context objects.  
  - `ontomi-ops.ttl` — vectors, profiles, pipeline artifacts.
- **Integration:** Anchors to BFO/IAO classes for ICE and related entities.
- **Open items:** Provide a figure or PlantUML for module relations (optional).

### 4.3 Reference Ontology Documentation (DOC-MODE, MAN-MODE, EVA-MODE, PUB-REFE)
- **Outputs:** Concept dictionary in README/docs; competency questions; reference diagrams (optional).  
- **Open items:** Maintain a **Model Dictionary** (`docs/model-dictionary.md`).

---

## 5. Design Phase
### 5.1 Encoding Language & Vocabularies (DES-LANG, DES-VOCA)
- **Encoding:** **TTL/OWL**.  
- **Vocabularies:** `rdf`, `rdfs`, `owl`, `xsd`, plus `bfo`, `iao` (OBO-style).

### 5.2 Ontology Encoding (DES-CODE)
- **Conventions:** CamelCase for classes; lowerCamelCase for properties; `@en`/`@pt` labels; `owl:versionInfo`; `rdfs:isDefinedBy`.  
- **Architecture:** Multi-module TTL; imports with `owl:imports` where needed.

### 5.3 Document/Control/Evaluate (DOC-OPER, MAN-OPER, EVA-OPER)
- **Outputs:** TTL headers with metadata; coding rules in `docs/coding-rules.md`.  
- **Open items:** Add explicit *disjointness* and *cardinality* where safe; create **SPARQL** query examples per CQ.

---

## 6. Implementation Phase
### 6.1 Code Concepts/Relations/Axioms (IMP-CONC/RELC/AXIO)
- **Status:** TTL modules with BFO/IAO anchors; MI classes, evidence, and operations encoded.  
- **Examples:** Instance templates for sentence-level tagging and evidence traces.

### 6.2 Documentation/Control/Evaluation/Publication (DOC-OPER, MAN-OPER, EVA-OPER, PUB-OPER)
- **Publication:** Repo with `CITATION.cff`, **CHANGELOG**, **Release Notes**, and **docs/**.  
- **Tests:** SPARQL answering CQs on synthetic canonic instances (gold set).  
- **Open items:** Provide minimal **demo dataset** + `queries/` folder.

---

## 7. Competency Questions (CQs)
> The CQs constrain the ontology’s scope and are later used for verification via queries.
- **CQ1 (Coverage):** Which **MI** categories are **activated** by a given **text** (or **explanation fragment**)?  
- **CQ2 (Evidence):** For a given **activation**, which **evidence fragments** and **discursive strategies** justify it?  
- **CQ3 (Profiles/Vectors):** What **MI vector** is computed for a **resource** or **corpus**, and how does it **match** a given **student profile**?
- **CQ4 (Granularity):** Which **sentences** in a text contribute most to **MI=Linguistic/Logical/...**?  
- **CQ5 (Traceability):** For a **recommendation decision**, which **ontology individuals/relations** justify the outcome?

**Planned files:** `docs/competency-questions.md`, `queries/cq-examples.sparql` (one query per CQ).

---

## 8. Traceability Matrix (SABiOx ⇄ OntoMI Artifacts)
| SABiOx Activity | OntoMI Artifact / Evidence |
|---|---|
| REQ-PURP | README project purpose; §2.1 of this report |
| REQ-DOMN | Domain boundaries in README/docs; §2.2 |
| REQ-ELIC | FR/NFR in §2.3 |
| REQ-SUBD | Modules listed in §4.2 |
| DOC-SPEC / MAN-SPEC / EVA-SPEC | This report, Git history, review meetings |
| SET-LANG / SET-FOUN | TTL + BFO/IAO; §3.1–3.2 |
| SET-CRIT | Inclusion/exclusion criteria §3.3 |
| SET-REUS | BFO/IAO reuse §3.4 |
| DOC-REFE / MAN-REFE / EVA-REFE | Foundational premises in TTL headers |
| CAP-CONC / CAP-AXIM | Concept list + axioms §4.1 |
| CAP-MODE / CAP-INTE / CAP-MODU | Module plan §4.2 |
| DOC-MODE / MAN-MODE / EVA-MODE / PUB-REFE | Docs + publication (repo) |
| DES-* | Encoding rules and vocabularies §5 |
| IMP-* | TTL implementation & tests §6 |

---

## 9. Acceptance & Quality Checklist (per SABiOx)
- [x] Purpose and domain boundaries recorded (**REQ-PURP/DOMN**).  
- [x] FR/NFR and subdomains (**REQ-ELIC/SUBD**).  
- [x] Foundational choices, vocabularies, criteria (**SET-***).  
- [x] Concept list, axioms, modules (**CAP-***).  
- [x] Encoding language and rules (**DES-***).  
- [x] TTL implementation with metadata and tests (**IMP-***).  
- [x] Documentation, citation, changelog, releases (**DOC/MAN/EVA/PUB**).

---
