# 1. Setup Phase

The Setup Phase aims to define questions that will guide the elaboration of the reference ontology, that is, decisions that have an impact on the conceptual modeling tasks to follow. Its main activities have the aid of supporting activities of the following categories:

* **Knowledge Acquisition (KNO):** to extract knowledge from resources;
* **Reuse (REU):** to reuse recognized ontological and non-ontological resources;
* **Documentation (DOC):** to register this knowledge as part of the Reference Ontology Document;
* **Configuration Management (MAN):** to control the changes, versions and deliveries of the documented information;
* **Evaluation (EVA):** to verify that the questions defined for the reference ontology meet its purpose.

The activities that compose this phase are presented in the following sections. Each activity is represented by a 4-letter acronym with a 3-letter prefix indicating if it is a main activity of this phase (**SET**) or a supporting activity, whose prefixes are indicated above.

---

## 1.1 Define Modeling Language (SET-LANG)

**Setup activity** that defines the modeling language to be used in the construction of the reference ontology, i.e., the conceptual model. The choice of language directly influences the integration and reuse of the ontology under construction, since ontologies developed in different languages may require greater adaptation efforts.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** ontology specification document prepared in the activity Document Specification (DOC-SPEC);
**What-Output:** choice of modeling language to be adopted in the reference ontology.

**Support activities in parallel**

**Adopt Modeling Language (REU-LANG)**
Reuse activity that aims to adopt existing modeling languages for building the reference ontology. There are several languages to model, communicate and negotiate ontology concepts.

**Running Example:**
For **OntoMI**, the **GRAFOO** (Graphical Framework for OWL Ontologies) notation is adopted for conceptual diagrams, with **OWL 2 DL (TTL serialization)** as the logical implementation language to ensure direct traceability between conceptual and logical artifacts.

---

## 1.2 Define Foundational Ontology (SET-FOUN)

**Setup activity** that defines the foundational ontology to be adopted, which guides the modeling process of the ontology under construction and the views of the reused ontologies. To do this, the popularity, usability, and adherence of the foundational ontology for the defined domain must be considered, as well as the expertise of the ontology engineer in the chosen ontology.

SABiO highlights the importance of concepts and relationships being previously analyzed in light of a foundational ontology. Reuse of grounding ontologies can be done by specialization or analogy, when concepts and relations are not explicitly extended but rather implicitly used to derive the ontology under construction.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** ontology domain identified in activity Identify and Size Domain (REQ-DOMN) and modeling language defined in activity Define Modeling Language (SET-LANG);
**What-Output:** choice of foundational ontology and conceptual patterns to be applied to the ontology under construction.

**Support activities in parallel**

**Adopt Foundational Ontology (REU-FOUN)**
Reuse activity that aims to adopt an existing foundational ontology for the construction of the reference ontology.

**Adopt Ontology Patterns (REU-PATT)**
Reuse activity that aims to define the ontology patterns to be adopted in the ontology construction process. Such patterns can be classified as:

* **Conceptual Pattern:** reusable fragments of grounding or domain reference ontologies;
* **Architectural Pattern:** patterns that describe how to organize the ontology in terms of subontologies or modules;
* **Design Pattern:** patterns related to reasoning and logical implementation constructs; and
* **Programming Pattern:** patterns related to the ontology implementation language.

**Running Example:**
For **OntoMI**, the **Basic Formal Ontology (BFO 2.0)** is adopted as the foundational ontology. Patterns reused include:

* **Information Content Entity** patterns (from **IAO**) to model text segments and annotations;
* **Quality/Measurement** pattern (BFO + **QUDT** for units/scales) to model **intensity** as a measurable attribute of evocation;
* **Process/Occurrence** pattern (BFO) to model **Evocation** as an event-like occurrence relating evidence and intelligence;
* **Provenance** pattern (**PROV-O**) to register creators, tools and timestamps of assertions.

---

## 1.3 Define Concept Criteria (SET-CRIT)

**Setup activity** that defines the criteria that will be adopted to identify if a concept is adherent to the domain of the ontology under construction. For this, a list of objective criteria, with quantitative information, or subjective criteria, with qualitative information, is defined. These criteria can be defined for individual analysis of each knowledge source or joint analysis over all the cataloged sources.

Given the depth of domain knowledge at this point, defining criteria can be challenging. Thus, as knowledge is enriched and decisions about the domain are made, one should return to this activity to update these criteria.

**Activity definition:**
**Who:** ontology engineer as responsible and domain expert as participant. Alternatively, to optimize the process, this activity can be conducted unilaterally by the domain expert;
**What-Input:** ontology specification document prepared in the activity Document Specification (DOC-SPEC);
**What-Output:** criteria defined for the domain concepts.

**Running Example:**
For **OntoMI**, a concept is adherent to the domain if it satisfies **all** mandatory criteria and at least **one** optional criterion:

**Mandatory criteria:**

* The concept represents **Multiple Intelligence**, **Evocation**, **Evidence** (keyword, discourse strategy, context object), **Text Segment**, **Intensity**, or **Provenance** elements directly related to **textual MI evocation**;
* The concept is **operationalizable** in OWL 2 DL with SHACL constraints (i.e., identifiable in instances and queryable to answer CQ1–CQ3);
* The concept is **foundationally alignable** to BFO/IAO categories.

**Optional criteria:**

* The concept appears (or its role is observed) in **≥ 30%** of the sampled explanatory corpus or in **≥ 2** evidence types;
* The concept is **language-agnostic** (not specific to a single natural language or pedagogy) and supports cross-corpus reuse;
* The concept increases **traceability** (e.g., improves links between evocation and evidence).

---

## 1.4 Define Ontologies to Reuse (SET-REUS)

**Setup activity** that defines the reference ontologies to be reused, i.e., ontologies or ontology fragments that match the purpose of the ontology under construction.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** ontology specification document prepared in the activity Document Specification (DOC-SPEC);
**What-Output:** ontologies to be reused in the ontology under construction.

**Support activities in parallel**

**Adopt Reused Ontology (REU-ONTO)**
Reuse activity that aims to adopt core and domain ontologies related to the purpose of the ontology under construction, regardless of its ontology grounding level. The reuse of ontologies is a challenge, since it involves heterogeneity of formalism, diversity of languages, lexical and semantic problems, implicit representation assumptions, loss of consensus knowledge, lack of documentation, and others.
The reuse of a **core ontology** will position the ontology under construction within a broader domain, while that of a **domain ontology** will provide concepts already formalized for its domain. To do this, one must search for candidate ontologies in search engines, repositories, and known ontologies.
To select core ontologies, one must analyze whether the candidate ontology represents appropriate concepts to anchor the ontology under construction. To select domain ontologies, one should analyze the coverage of the candidate ontology with respect to the requirements of the ontology under construction.
Further, one must consider: (i) if any ontology analysis was applied to the candidate ontologies; (ii) if the foundational ontology adopted by the candidate ontology is adherent to the ontology under construction; and (iii) if the domain perspective represented in the candidate ontology corresponds to that of the ontology under construction. The candidate ontology may refer to an individual ontology or to a network of ontologies.

**Running Example:**
For **OntoMI**, candidate ontologies/vocabularies are surveyed and evaluated for adherence to BFO and coverage of requirements:

* **BFO 2.0** (foundational grounding; mandatory);
* **IAO** (Information Artifact Ontology) for documents, text, and annotations;
* **PROV-O** for provenance of assertions and processing steps;
* **DCMI Terms (dcterms)** for basic metadata (title, creator, source, created);
* **SKOS** for controlled labels and examples when needed;
* **QUDT** (or OM) for **intensity** value/scale modeling;
* **Web Annotation (OA)** and/or **NIF 2.0** for addressing **text segments** with selectors/offsets;
* **OBO RO** (Relations Ontology) for standardized object properties (e.g., part-of, about).

Selected for reuse in OntoMI: **BFO, IAO, PROV-O, DCTERMS, SKOS, QUDT, OA/NIF, RO**. Other candidates are documented but not adopted if they diverge from BFO grounding or fail to cover CQ1–CQ3 needs.

---

## 1.5 Document Premise of Reference Ontology (DOC-REFE)

**Documentation activity** that documents the assumptions of the reference ontology in the **Reference Ontology Document**, which must include the questions previously defined in this phase, namely:

* **Modeling Language:** description of the modeling language;
* **Foundational Ontology:** description of the foundational ontology and its ontology patterns;
* **Ontologies to Reuse:** presentation of the core and/or domain ontologies to be reused in the ontology under construction.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** results from the activities performed earlier in this phase;
**What-Output:** Reference Ontology Document with its respective premises.

**Running Example:**
In **OntoMI**, the Reference Ontology Document is prepared with the premises established for the MI-evocation reference ontology, as presented in **Table 4.1**.

**Table 1.1: Ontology Reference Document**

* **Document:** Reference Ontology
* **Ontology:** OntoMI — Multiple Intelligences Evocation
* **Version:** v0.1
* **Date:** Oct 27, 2025

**Modeling Language:**

* **Conceptual:** **GRAFOO** diagrams for OWL artifacts;
* **Logical:** **OWL 2 DL** (TTL), aligned 1–1 with conceptual elements.

**Foundational Ontology:**

* **BFO 2.0** as foundational grounding; domain aligned via:

  * **IAO** for information content entities (documents, text segments, annotations);
  * **QUDT** for quantitative **intensity** (datatype values, scales, units);
  * **PROV-O** for provenance (agents, activities, times).

**Criteria (excerpt):**

* **CR01** Concept is directly related to textual MI evocation (Evocation, Intelligence, Evidence, Segment, Intensity, Provenance);
* **CR02** Concept is operationalizable in OWL 2 DL with SHACL constraints and supports CQ1–CQ3;
* **CR03** Concept is alignable to BFO/IAO;
* **CR04 (opt.)** Concept observed in ≥ 30% of sampled corpus or in ≥ 2 evidence types;
* **CR05 (opt.)** Concept improves traceability and explainability.

**Ontologies to Reuse (selected):**

| Prefix     | Name / Role                   | Foundation   | Adoption Note                        |
| ---------- | ----------------------------- | ------------ | ------------------------------------ |
| bfo:       | Basic Formal Ontology         | Foundational | Grounding of upper-level categories  |
| iao:       | Information Artifact Ontology | OBO          | Documents, text, annotations         |
| prov:      | PROV-O                        | W3C          | Provenance of assertions/processes   |
| dct:       | DCMI Terms                    | —            | Metadata (creator, date, source)     |
| skos:      | SKOS                          | —            | Labels, notes, examples              |
| qudt:      | QUDT                          | —            | Units/scales for intensity           |
| oa: / nif: | Web Annotation / NIF 2.0      | —            | Text segment anchoring and selectors |
| ro:        | OBO Relations Ontology        | OBO          | Standard relations (e.g., part-of)   |

---

## 1.6 Control Premise of Reference Ontology (MAN-REFE)

**Configuration Management activity** that controls the changes, versions and deliveries of the information registered in the Reference Ontology Document, described in the activity Document Premise of Reference Ontology (DOC-REFE). It is suggested that the same version control mechanism adopted in activity Control Specification (MAN-SPEC) continues to be used here.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in activity Document Premise of Reference Ontology (DOC-REFE);
**What-Output:** control of the Reference Ontology Document.

**Running Example:**
For **OntoMI**, version and date headers in the Reference Ontology Document are adopted to control its versions, complemented by **Git tags** (e.g., `ontomi-ref-v0.1`) and **CHANGELOG** entries mirroring the specification’s control choices.

---

## 1.7 Evaluate Premise of Reference Ontology (EVA-REFE)

**Evaluation activity** that assesses whether the information registered in the Reference Ontology Document meets the expectations of the ontology owner and is in accordance with the domain expert. This is done by validating the registered information with the ontology owner and returning to the beginning of the phase whenever necessary.

**Activity definition:**
**Who:** ontology owner and domain expert as responsible;
**What-Input:** Reference Ontology Document prepared in activity Document Premise of Reference Ontology (DOC-REFE);
**What-Output:** evaluation of the Reference Ontology Document.

**Running Example:**
In **OntoMI**, meetings are held with the ontology owner and the domain expert to validate the Reference Ontology Document (Table 4.1). Review outcomes are logged as issues labeled `setup`, and the phase is iterated when criteria or reuse choices need refinement.
