# 1. Capture Phase

The Capture Phase aims to represent in a well-founded way the domain conceptualization based on the specification elaborated in the Requirements Phase and the questions defined in the Setup Phase, which should be revised at each iteration in order to add, detail, and delete requirements and questions related to the domain needs. In this context, conceptualization is an intentional semantic framework that encodes the implicit rules that constrain the structure of a part of reality.

The main activities of this phase have the aid of supporting activities of the following categories:

* **Knowledge Acquisition (KNO):** to extract the knowledge from the domain;
* **Reuse (REU):** to reuse recognized ontological and non-ontological resources;
* **Documentation (DOC):** to register this knowledge as a conceptual model and part of the Reference Ontology Document;
* **Configuration Management (MAN):** to control the changes, versions and deliveries of the documented information;
* **Evaluation (EVA):** to verify if the ontology is being built according to the requested requirements and to validate if it meets its purpose;
* **Publication (PUB):** to make the reference ontology available.

> Note: A single ontology specification can give rise to distributed processes in the reference phase, according to the subdomains defined in **Identify Subdomains (REQ-SUBD)**.

Each activity is represented by a 4-letter acronym with a 3-letter prefix indicating if it is a main activity of this phase (**CAP**) or a supporting activity, whose prefixes are indicated above.

---

## 1.1 Identify Concepts (CAP-CONC)

Capture activity that identifies which domain concepts are part of the purpose of the ontology according to the knowledge sources. This activity treats **concept** as a conception or idea of a reality; therefore **types**, **properties** and **examples** are not identified as concepts, but as part of the description of concepts.

### 1.1.1 Catalog Concepts (CAP-CATA)

Capture activity that catalogs the concepts related to the ontology domain, according to the criteria defined in **Define Concept Criteria (SET-CRIT)**.

Concepts can be cataloged using three different knowledge sources: **data source**, **domain expert**, and **ontology owner**. Data sources include books, standards, specifications, articles, or other recognized references. The initial catalog forms a simple list of terms and meanings extracted from different sources, i.e., it may contain conflicts, overlaps and synonyms.

Although guided by criteria, this activity remains subjective and dependent on the analysis of the involved roles. Only criteria defined from **individual analysis** of knowledge sources are applied here; criteria requiring **joint analysis** are applied in **Model Ontology (CAP-MODE)**.

The results of this activity optimize **CAP-MODE**, since domain knowledge can be identified by different roles and basic domain instructions can be organized.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert and/or ontology owner as participants (can be distributed across roles);
**What-Input:** ontology specification document prepared in **Document Specification (DOC-SPEC)**;
**What-Output:** domain concepts extracted from the knowledge sources.

**Support activities in parallel**

**Capture Concepts (KNO-CONC)**
Apply brainstorming, interviews, forms and concept mapping with the ontology owner and domain experts; for data sources, search repositories and apply text analysis to extract high-evidence concepts. At this point, capture **all** potentially relevant concepts, without worrying about overlaps or relations.

**Reuse Data Source (REU-DATA)**
Adopt authoritative data sources; avoid inventing descriptions—prefer importing from recognized references.

**Running Example (OntoMI):**
For **OntoMI**, books and articles on Multiple Intelligences (MI), discourse analysis/strategies, educational text explanation, and semantic annotation were used as knowledge sources, alongside internal guidelines for MI evidence and text segmentation. A fragment of the concept catalog (simplified) is shown below.

**Table 1.1: Fragment of the Concept Catalog for OntoMI**

| Source               | Concept                 | Definition (excerpt)                                                                                                                                                   | Instance (illustrative)                     |
| -------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| MI Theory & Pedagogy | **Intelligence**        | A cognitive capacity classifiable under MI (e.g., Linguistic, Logical-Mathematical, Spatial, Bodily-Kinesthetic, Musical, Interpersonal, Intrapersonal, Naturalistic). | `ontomi:LinguisticIntelligence`             |
| Discourse Analysis   | **DiscourseStrategy**   | A rhetorical/structural device used in explanatory text that can contribute evidence for MI evocation.                                                                 | `ontomi:AnalogicalReasoning`                |
| Text Annotation      | **TextSegment**         | A bounded fragment (sentence/paragraph) of a document that bears evocations and evidence.                                                                              | `ontomi:seg-para-003`                       |
| MI Attribution       | **Evocation**           | An assertion that a segment activates an Intelligence with a measurable intensity and associated evidence.                                                             | `ontomi:ev-00021`                           |
| Quantities/Measures  | **Intensity**           | A scalar value expressing strength of evocation on a defined scale.                                                                                                    | `ontomi:intensityValue "0.78"^^xsd:decimal` |
| Evidence Model       | **Evidence**            | An observable semantic element supporting an evocation; typed as KeywordEvidence, DiscourseStrategyEvidence, or ContextObjectEvidence.                                 | `ontomi:evd-kword-12`                       |
| Provenance           | **AttributionActivity** | The process/activity that created an Evocation assertion, with agent, tool, and time.                                                                                  | `ontomi:run-2025-10-27T14:03Z`              |
| Metadata             | **EducationalDocument** | A document (lesson, chapter, article) composed of segments, from which evocations are derived.                                                                         | `ontomi:doc-physics-101`                    |

---

## 1.1.2 Extract Ontology View (CAP-VIEW)

Capture activity that extracts the **view** of the reference ontologies to be reused in the modeling of the ontology under construction.

A modularization strategy must be used to build a view (subset/projection) from a reused ontology. As the view is built, ontological analysis ensures compatibility with the ontology under construction. Guidelines:

1. If the reused ontology **fully matches** the purpose, reuse it completely;
2. If only a **part** matches, **partition** and reuse that part;
3. If only **some concepts** match, identify them and recursively visit their relations to gather the necessary subset.

This activity focuses on **modularization and analysis**, not on reengineering.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** ontologies to be reused identified in **Define Ontologies to Reuse (SET-REUS)**;
**What-Output:** views of the ontologies to be reused.

**Support activities in parallel**

**Capture View Concepts (KNO-VIEW)**
Identify the ontology concepts that will form the view. For core ontologies, identify anchors for the new ontology’s concepts; for domain ontologies, identify concepts that help answer the CQs.

**Running Example (OntoMI):**
For **OntoMI**, **BFO**/**IAO** are viewed to anchor **TextSegment** as an **Information Content Entity**; **QUDT** is viewed to reuse quantity/scale for **Intensity**; **PROV-O** is viewed to model **AttributionActivity/Agent**; **Web Annotation/NIF** are viewed to address **selectors/offsets** for segments. These views are limited to the minimal concept/property sets needed to satisfy CQ1–CQ3.

---

## 1.2 Identify Axioms (CAP-AXIM)

Capture activity that identifies the **constraint** and **inference** axioms that the conceptual model must consider. Identify constraints that cannot be fully represented graphically and register them as **informal axioms** (natural language) or in a **formalism** (e.g., FOL, OCL). As the model evolves, return to this activity for completeness and disambiguation.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert as participant;
**What-Input:** concepts identified in **Catalog Concepts (CAP-CATA)**;
**What-Output:** informal (and optional formal) axioms of the ontology.

**Running Example (OntoMI):**

* **AX1 (Cardinality):** Every `Evocation` **must** evoke exactly **one** `Intelligence` and refer to exactly **one** `TextSegment`.
* **AX2 (Evidence Requirement):** Every `Evocation` **must have at least one** `Evidence`.
* **AX3 (Typed Evidence):** Every `Evidence` instance **must** be typed as **KeywordEvidence** or **DiscourseStrategyEvidence** or **ContextObjectEvidence**.
* **AX4 (Intensity Domain):** `intensityValue` is **xsd:decimal** within **[0,1]** (inclusive).
* **AX5 (Provenance):** Every `Evocation` **must** be generated by **some** `AttributionActivity` (`prov:wasGeneratedBy`), with `prov:wasAssociatedWith` an Agent and `prov:endedAtTime`.

*(FOL sketch for AX1)*
∀e:Evocation. ∃! i:Intelligence (evokesMI(e,i)) ∧ ∃! s:TextSegment (isAboutSegment(e,s))

---

## 1.3 Model Ontology (CAP-MODE)

Capture activity that models concepts and relationships covered by the purpose of the ontology in a **technology-independent** representation language, applying **ontological analysis** (foundational categories) and **conceptual ontology patterns**.

Modeling can follow **top-down**, **bottom-up**, or **middle-out** approaches; **middle-out** is recommended for balance and reduced rework.

Concepts/relations should be modeled in the language defined in **SET-LANG**; each concept should be categorized according to the foundational ontology defined in **SET-FOUN**. For each relation, define **name, direction, type, cardinality**. Apply conceptual patterns to ensure model quality. Modeling is **evolutionary**.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert as participant;
**What-Input:** concepts identified in **CAP-CONC** (knowledge sources and reused ontologies);
**What-Output:** conceptual model of the ontology under construction.

**Support activities in parallel**

**Concepts Consensus (KNO-CONS)**
Establish semantic consensus on cataloged concepts, applying the **SET-CRIT** criteria across sources and resolving ambiguities/conflicts to form a shared conceptualization.

**Concepts Terminology (KNO-TERM)**
Define representative terms for consensus concepts. If terms are consensual across sources, adopt them; otherwise, select the term with greatest domain relevance and clarity.

**Running Example (OntoMI):**
The conceptual model introduces:

* `Intelligence` (MI types) — **BFO:category/class** aligned;
* `Evocation` — **BFO:processual entity** relating a `TextSegment` to an `Intelligence` with an `Intensity`;
* `Evidence` (with subclasses) — **IAO/annotation-like** entities linked to `Evocation`;
* `TextSegment` — **IAO:information content entity** with selectors;
* `AttributionActivity` — **prov:Activity** with Agent/time;
* Relations: `evokesMI`, `isAboutSegment`, `hasEvidence`, `hasIntensity`, `wasGeneratedBy`, `wasAssociatedWith`, etc., with explicit cardinalities.

---

## 1.4 Integrate Ontology (CAP-INTE)

Capture activity that integrates both the views of the ontology under construction and the views of reused ontologies. If built in a distributed fashion by subdomains, each subdomain yields a view to be integrated iteratively with **CAP-MODE**.

Integration with foundational ontologies may occur via **specialization** or **analogy**; integration with core/domain ontologies may use **composition** (join), establishing association/extension/specialization as needed.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert as participant;
**What-Input:** views from **CAP-MODE** and **CAP-VIEW**;
**What-Output:** integrated conceptual model.

**Running Example (OntoMI):**
Views from **BFO/IAO/QUDT/PROV-O/OA-NIF** are integrated: `TextSegment` specializes **IAO:InformationContentEntity**; `AttributionActivity` specializes **prov:Activity**; `Intensity` uses **QUDT** quantity/scale; segment selectors reuse **OA/NIF** patterns. Domain subviews (Core, Evidence, Text & Segment, Provenance/Aggregation) are merged via consistent identifiers and mapped relations.

---

## 1.5 Modularize Ontology (CAP-MODU)

Capture activity that identifies modules into which the ontology can be decomposed and considered separately while interconnected.

Goals include improved performance, easier development/maintenance, and facilitated reuse. Execute iteratively to increase cohesion and reduce coupling. Choose an appropriate modularization strategy.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert as participant;
**What-Input:** conceptual model from **CAP-MODE** and **CAP-INTE**;
**What-Output:** modularized conceptual model.

**Support activities in parallel**

**Adopt Modularization Strategy (REU-MODU)**
Consider two main strategies:

1. **Partitioning** by subdomain with completeness preserved;
2. **Transversal extraction** from key concepts, recursively collecting required neighborhoods.

**Running Example (OntoMI):**
Partitioning is adopted into the following modules:

* **Core:** Intelligence, Evocation, Intensity, main relations;
* **Text & Segment:** EducationalDocument, TextSegment, selectors;
* **Evidence:** Evidence and its subtypes;
* **Provenance & Metadata:** AttributionActivity, Agent, timestamps, dcterms;
* **Profiling & Aggregation:** document-level MI vectors, summaries.

---

## 1.6 Document Reference Ontology (DOC-MODE)

Documentation activity that records the conceptual model in the **Reference Ontology Document**, complementing **DOC-REFE**, with:

* **Modularization:** UML package diagram (or equivalent), standardized by colors;
* **Conceptual Model:** the ontology conceptual diagram;
* **Model Axioms:** constraints as informal axioms (and optional FOL/OCL);
* **Model Description:** natural language narrative of concepts and relations;
* **Model Dictionary:** glossary of concepts and meanings.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document from **DOC-REFE** and results from this phase;
**What-Output:** a complete Reference Ontology Document.

**Running Example (OntoMI) — Fragment of the Reference Ontology Document**

* **Document:** Reference Ontology
* **Ontology:** OntoMI — Multiple Intelligences Evocation
* **Version:** v0.1
* **Date:** Oct 27, 2025

**Modeling Language:** GRAFOO (conceptual), OWL 2 DL (TTL)
**Foundational Ontology:** BFO (with IAO/PROV-O/QUDT/OA/NIF views)
**Modularization:** Core; Text & Segment; Evidence; Provenance & Metadata; Profiling & Aggregation

**Axioms (excerpt):** AX1–AX5 as listed in **CAP-AXIM**.

**Dictionary (excerpt):**

* **Evocation:** Assertion that a `TextSegment` activates an `Intelligence` with an `Intensity`, justified by `Evidence`.
* **Evidence:** Observable semantic element supporting an evocation; typed as KeywordEvidence, DiscourseStrategyEvidence, or ContextObjectEvidence.
* **Intensity:** Scalar in [0,1] quantifying activation strength.
* **TextSegment:** Bounded fragment (sentence/paragraph) bearing evocations and evidence.

---

## 1.7 Control Reference Ontology (MAN-MODE)

Configuration Management activity that controls the changes, versions and deliveries of the information registered in the Reference Ontology Document (complementing **MAN-REFE**).

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in **DOC-MODE**;
**What-Output:** controlled versions, change history and release records.

**Running Example (OntoMI):**
Headers with version/date are maintained; **Git tags** (e.g., `ontomi-ref-v0.1`) and **CHANGELOG** entries track evolution and releases.

---

## 1.8 Evaluate Reference Ontology (EVA-MODE)

Evaluation activity that assesses whether the information recorded in the Reference Ontology Document meets expectations, applying **static evaluation** over requirements and purpose. Validate information and iterate as needed.

For **verification**, assess via technical reviews whether **functional requirements** are answered by the conceptual model’s concepts/relations. Competency questions from **REQ-ELIC** should be answerable exclusively by the conceptual model, forming reasoning paths.

The pattern **c1 > r > c2** transcribes a relation where **c1** is the source concept, **c2** the target concept, and **r** the relation. Use:

* association → relation name;
* composition → `componentOf`;
* specialization → `subtypeOf`;
* generalization → `specializedBy`.

For **validation**, evaluate whether the ontology meets real situations by **instantiating** its concepts (mapping cataloged examples to ontology instances).

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document from **DOC-MODE**;
**What-Output:** evaluation of the Reference Ontology Document.

**Running Example (OntoMI):**
**Verification via CQs:**

* **CQ1:** `Evocation > evokesMI > Intelligence` and `Evocation > isAboutSegment > TextSegment`
* **CQ2:** `Evocation > hasEvidence > Evidence` and `Evidence > a > (KeywordEvidence | DiscourseStrategyEvidence | ContextObjectEvidence)`
* **CQ3:** `Evocation > intensityValue > xsd:decimal` with ordering over values per segment

**Validation via instantiation:**
Given a physics paragraph (document `doc-physics-101`, segment `seg-para-003`), instantiate:
`seg-para-003 instanceOf TextSegment; ev-00021 instanceOf Evocation; LinguisticIntelligence instanceOf Intelligence; ev-00021 evokesMI LinguisticIntelligence; ev-00021 isAboutSegment seg-para-003; ev-00021 hasEvidence evd-kword-12; evd-kword-12 instanceOf KeywordEvidence; ev-00021 intensityValue "0.78"^^xsd:decimal; ev-00021 wasGeneratedBy run-2025-10-27T14:03Z; run-2025-10-27T14:03Z wasAssociatedWith agent-OntoMI.`

---

## 1.9 Publish Reference Ontology (PUB-REFE)

Publication activity that publishes the Reference Ontology defined in **DOC-MODE**.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in **DOC-MODE**;
**What-Output:** reference ontology made available.

**Running Example (OntoMI):**
The Reference Ontology Document and conceptual diagrams are published in the project repository under `docs/reference-ontology/`, with a versioned release and public read access.
