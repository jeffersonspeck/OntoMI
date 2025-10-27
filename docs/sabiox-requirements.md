# 1. Requirements Phase

The Requirements Phase aims to identify the purpose of the ontology within a defined domain and to discover the needs that the ontology should satisfy regarding its content and characteristics. Its main activities have the aid of supporting activities of the following categories:

* **Knowledge Acquisition (KNO):** to extract knowledge through the use of brainstorming, interview, questionnaire, concept mapping and other elicitation techniques;
* **Documentation (DOC):** to register the acquired knowledge as an ontology specification;
* **Configuration Management (MAN):** to control the changes, versions and deliveries of the information recorded in the ontology specification;
* **Evaluation (EVA):** to validate whether the information extracted and registered in the ontology specification meets the expectations.

The activities that compose this phase are presented in the following sections. Each activity is represented by a 4-letter acronym with a 3-letter prefix indicating if it is a main activity of this phase (**REQ**) or a supporting activity (prefixes listed above).

---

## 1.1 Define Purpose (REQ-PURP)

**Requirements activity** that defines and describes the purpose of the ontology in order to answer: *what* is the domain that the ontology intends to represent, *for what* the ontology will be useful, and *why* the ontology should be built.

**Activity definition:**
**Who:** ontology engineer as responsible and ontology owner as participant;
**What-Input:** need to build an ontology;
**What-Output:** answers to the questions *what*, *for what*, and *why*.

**Support activities in parallel**

**Capture Ontology Purpose (KNO-PURP)**
Knowledge Acquisition activity in which the ontology engineer extracts expectations from the ontology owner in order to answer the three questions (what, for what, and why) for the ontology. This knowledge is usually acquired through brainstorming and interview techniques.

**Running Example (OntoMI):**
For **OntoMI**, the purpose of the ontology is: to represent the concepts related to the **evocation of Multiple Intelligences (MI)** in explanatory educational texts (*what*); so that MI evocations can be **consistently identified, justified by evidence, measured in intensity, queried via SPARQL, and reused by external profiling/recommendation services** (*for what*); because current educational resources and analytics lack a **standard, interoperable, and explainable semantic model** for MI attribution—leading to heterogeneity, weak traceability of evidence, and limited interoperability (*why*).

---

## 1.2 Identify and Size Domain (REQ-DOMN)

**Requirements activity** that identifies the domain that the ontology is intended to represent according to its purpose and sizes its boundaries. It should identify the knowledge as well as the level of detail that the ontology should cover of the domain. It can also explicitly indicate which details or parts should not be covered. Although the development of an ontology is primarily driven by the application-related scenarios of that ontology, the goal of this activity is not to list the application scenarios but rather to extract the **knowledge domain** embedded in those scenarios.

**Activity definition:**
**Who:** ontology engineer as responsible and ontology owner as participant;
**What-Input:** purpose of the ontology defined in the activity Define Purpose (REQ-PURP);
**What-Output:** the domain to be represented in the ontology and its boundaries.

**Support activities in parallel**

**Understanding Ontology Domain (KNO-DOMU)**
Knowledge Acquisition activity in which the ontology engineer aims to understand the domain related to the purpose of the ontology, considering the prior knowledge of the ontology owner, domain expert and sources from the literature on the domain.

**Size Ontology Domain (KNO-DOMS)**
Knowledge Acquisition activity in which the ontology engineer aims to size the domain boundaries to be represented in the ontology. This activity is challenging, because real-world domains are interconnected and it is not always possible to define a clear boundary between them. Therefore, the prior knowledge of the ontology owner about the threshold dimensions of this domain must be considered.
Boundaries should be defined for **horizontal dimension** in order to limit the external areas that are part of the domain and **vertical dimension** in order to limit the level of detail that should be delved into in the domain.

**Running Example (OntoMI):**
For **OntoMI**, the domain is defined as the **semantic representation of Multiple Intelligences evoked by explanatory educational texts**, including the **evocation event**, its **evidence** (e.g., keywords, discourse strategies, context objects), its **intensity**, and the **text segment** it refers to, along with essential **provenance/metadata** to ensure accountability and reuse.
In the **horizontal dimension**, the domain is limited to concepts related to **textual MI evocation and its justification**; it excludes general learner modeling, assessment instruments, and UI/visualization.
For the **vertical dimension**, the representation focuses on **text segments (sentence/paragraph)** and **document-level aggregation** for profiling; it does not cover psychometric validation details, classroom orchestration workflows, or non-text modalities (audio/video) at this stage.

---

## 1.3 Elicit Requirements (REQ-ELIC)

**Requirements activity** that elicits functional and non-functional requirements for the ontology.

For the **functional requirements**, competency questions (informal) are used. Such questions are represented by interrogative sentences and should be defined in a stratified manner, with higher-level questions requiring the solution of lower-level questions. The questions serve as constraints on what the ontology can be, i.e., they restrict what is or is not relevant to the ontology. Furthermore, these questions are used in the future to evaluate the ontology’s ontological commitment to check whether the ontology meets the requirements.

For the **non-functional requirements**, we consider ontology quality requirements (e.g., reasoning performance, availability, usability, maintainability); design requirements (e.g., implementation language definition, adherence to process model, foundational grounding); and intended use requirements (e.g., data source selection, ontology grouping), i.e., requirements not directly related to the contents of the ontology.

**Activity definition:**
**Who:** ontology engineer as responsible and ontology owner as participant;
**What-Input:** ontology domain identified in the activity Identify and Size Domain (REQ-DOMN);
**What-Output:** functional and non-functional requirements that the ontology must answer/satisfy.

**Support activities in parallel**

**Capture Ontology Requirements (KNO-REQI)**
Knowledge Acquisition activity in which the ontology engineer aims to discover the needs or knowledge that should be represented in the ontology. One should consider that the needs will hardly be exhausted and, therefore, the requirements must be discovered, analyzed, negotiated and updated continuously, that is, one must return to this activity whenever necessary. This knowledge is usually acquired through brainstorming, interview and concept mapping techniques.

**Negotiate Ontology Requirements (KNO-REQN)**
Knowledge Acquisition activity in which the ontology engineer aims to negotiate with the ontology owner which requirements should be considered for building the ontology. It should be considered that not all initial needs of the ontology owner are relevant to the ontology domain.

**Running Example (OntoMI):**
For **OntoMI**, the following **functional requirements (competency questions)** are defined:

* **CQ1.** Which Multiple Intelligences are evoked in a given explanatory text segment?
* **CQ2.** Which semantic elements (e.g., keywords, discourse strategies, context objects) contributed to each evocation?
* **CQ3.** In cases of multiple activations, which intelligence manifests with greater intensity?

Derived/auxiliary questions include:

* What text segments compose a document?
* What evocations are associated with a document and how are they aggregated into an MI vector?
* Which evidence items are linked to an evocation and of which evidence type are they?
* What is the intensity value, its scale, and unit/constraint?

Further, the following **non-functional requirements** are elicited:

* Be **modular** to facilitate reuse by other ontologies;
* Be **grounded** on a **foundational ontology** and reuse community vocabularies (BFO/OBO, DCTERMS, PROV, SKOS);
* Be **OWL 2 DL** compliant and provide **SHACL** shapes for validation;
* Ensure **traceability** between CQ ↔ query templates ↔ shapes ↔ instances;
* Provide **clear documentation**, stable **namespaces**, and **semantic versioning**;
* Offer **interoperability** for external services via SPARQL queries and resolvable IRIs;
* Maintain **reasoning performance** acceptable for the demo corpus and typical research datasets.

---

## 1.4 Identify Subdomains (REQ-SUBD)

**Requirements activity** that identifies subdomains related to the competency questions defined for the domain, in order to facilitate the identification of parts of the domain present in the ontology purpose and modularize the ontology requirements. Modularization in subdomains allows the targeted or distributed construction of the ontology; subdomains can be treated in parallel in later phases. To identify the subdomains, it is suggested to use pre-established categories in the domain or to create categories that reflect the high frequency terms present in the competency questions.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** functional requirements identified in the activity Elicit Requirements (REQ-ELIC);
**What-Output:** subdomains of the domain to be represented in the ontology.

**Running Example (OntoMI):**
For **OntoMI**, five subdomains are defined:

1. **Core** — MI, Evocation, Intensity;
2. **Text & Segment** — documents, segments, identifiers, containment;
3. **Evidence** — keywords, discourse strategies, context objects, evidence grouping;
4. **Profiling & Aggregation** — document/corpus-level MI vectors and summaries;
5. **Provenance & Metadata** — creators, tools, timestamps, sources.

---

## 1.5 Document Specification (DOC-SPEC)

**Documentation activity** that documents the specification of the ontology in an **Ontology Specification Document**, which should include the requirements raised for the ontology, as well as the following considerations:

* **Purpose of the Ontology:** natural language text following the standard convention: *The purpose of the ontology is to represent ⟨what⟩ ⟨what for⟩ ⟨why⟩*;
* **Ontology Domain:** natural language descriptive text describing the domain to be represented in the ontology;
* **Ontology Dimension:** natural language descriptive text clearly highlighting the horizontal and vertical boundaries of the ontology;
* **Subdomains:** name of the subdomains identified in the domain from the competency questions;
* **Functional Requirements:** list of competency questions with a unique identifier for each requirement, grouped by subdomains;
* **Non-Functional Requirements:** descriptive text in natural language with a unique identifier for each item.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** results from the main activities of this phase;
**What-Output:** ontology specification document.

**Running Example (OntoMI) — Fragment of the Ontology Specification Document**

**Document:** Ontology Specification
**Version:** v0.1
**Ontology:** OntoMI — Multiple Intelligences Evocation
**Date:** Oct 27, 2025

**Purpose of the Ontology:**
The purpose of the ontology is to represent the evocation of Multiple Intelligences in explanatory educational texts so that such evocations can be identified, justified by evidence, measured in intensity, queried in a standard way, and reused by external systems. This is motivated by the current lack of a standardized, interoperable, and explainable semantic model for MI attribution, which hampers comparison, traceability, and integration with learning technologies.

**Ontology Domain:**
The domain covers the semantic description of MI evocations in text segments (sentences/paragraphs), including evocation instances, their targeted intelligence, their intensity values, and their evidence (keywords, discourse strategies, context objects), as well as essential provenance and metadata for reuse and accountability.

**Ontology Dimension:**
Horizontally, the domain is limited to text-based MI evocation and justification; it excludes general learner modeling, psychometric instruments, and UI layers.
Vertically, the representation covers segment and document aggregation levels; it does not include non-text modalities or classroom orchestration workflows at this stage.

**Functional Requirements (Competency Questions):**

*Subdomain: Core*

* **RF01 (CQ1):** Which Multiple Intelligences are evoked in a given text segment?
* **RF02 (CQ3):** Which intelligence manifests with greater intensity for a given segment?

*Subdomain: Evidence*

* **RF03 (CQ2):** Which semantic elements contributed to an evocation, and of which evidence type are they?

*Subdomain: Text & Segment*

* **RF04:** Which segments compose a document and what evocations do they bear?

*Subdomain: Profiling & Aggregation*

* **RF05:** What is the aggregated MI vector of a document based on its evocations?

**Non-Functional Requirements:**

* **RNF01:** Modular design to facilitate reuse by other ontologies;
* **RNF02:** Grounding in a foundational ontology and reuse of community vocabularies;
* **RNF03:** OWL 2 DL compliance and SHACL validation coverage;
* **RNF04:** Traceability between CQ, queries, shapes, and instances;
* **RNF05:** Documentation, stable namespaces, and semantic versioning;
* **RNF06:** Interoperability via SPARQL and resolvable IRIs;
* **RNF07:** Reasoning and query performance acceptable for demo corpus.

---

## 1.6 Control Specification (MAN-SPEC)

**Configuration Management activity** that controls the changes, versions and deliveries of the information present in the Ontology Specification Document, described in the activity Document Specification (DOC-SPEC). Version control may range from simple headers with version/date and a change log, to the use of **Git** for branching, pull requests, and releases.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** ontology specification produced in DOC-SPEC;
**What-Output:** controlled versions, change history, and release tags of the specification.

**Running Example (OntoMI):**
For **OntoMI**, version and date information are included in the Ontology Specification header; additionally, the repository uses Git tags (e.g., `ontomi-spec-v0.1`) and a `CHANGELOG.md` to control versions and releases of the document and related artifacts.

---

## 1.7 Evaluate Specification (EVA-SPEC)

**Evaluation activity** that assesses whether the information extracted and registered in the Ontology Specification Document meets the expectations of the ontology owner. To do so, it is necessary to validate the registered information with the ontology owner and repeat the phase life cycle if necessary.

**Activity definition:**
**Who:** ontology owner as responsible;
**What-Input:** ontology specification document prepared in the activity Document Specification (DOC-SPEC);
**What-Output:** evaluation of the ontology specification document and identified revisions.

**Running Example (OntoMI):**
For **OntoMI**, review meetings are held with the ontology owner to validate the specification document. Feedback items are logged as issues labeled `requirements` and, when necessary, the phase cycle is repeated to incorporate negotiated changes.
