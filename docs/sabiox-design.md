
# 1. Design Phase

The Design Phase aims to define technological issues that will guide the implementation of the operational ontology, i.e., decisions that are dependent on the technological environment. In this context, the reference ontology, elaborated in the Capture Phase, provides the initial information to specify the design that may be originated by different technological choices.

This process aims to bridge the gap between the conceptual modeling of reference ontologies and their encoding in terms of an operational ontology language. To do this, it defines a set of activities that must be performed iteratively until the expected quality standard is defined. Given the technical nature of the process, it is suggested that the non-functional requirements defined in **Elicit Requirements (REQ-ELIC)** be revisited at each iteration, in order to add, detail and delete non-functional requirements related to the technological issues of the operational ontology. The activities of these respective processes are presented in the following subsections.

---

## 1.1 Define Encoding Language (DES-LANG)

**Design activity** that defines the representation language to be applied in the construction of the operational ontology, i.e., in the codification. The choice of language directly influences the integration and reuse of the ontology under construction, since ontologies developed in different languages may require a great deal of effort to adapt.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in **Document Reference Ontology (DOC-MODE)**;
**What-Output:** coding language to be adopted in the operational ontology.

**Support activities in parallel**

**Adopt Encoding Language (REU-ELAN)**
Activity that aims to define the encoding language to be adopted in the construction of the operational ontology. There are several languages to represent ontologies (e.g., KIF, RDF(S), OWL). Given popularity, clear formal semantics and tool support, **OWL 2 DL** is suggested.

**Running Example (OntoMI):**
For **OntoMI**, **OWL 2 DL** is chosen for encoding the operational ontology, with **Turtle (TTL)** as the canonical serialization.

---

## 1.2 Identify Vocabularies (DES-VOCA)

**Design activity** that identifies the vocabularies to be adopted in the coding of the ontology under construction, both base vocabularies to assist in the construction of the ontology and vocabularies of the reused ontologies.

These vocabularies must adopt an encoding language compatible with the language adopted in the ontology under construction (DES-LANG). In this context, *vocabulary* is the set of concepts and relations of a given domain, without necessarily adopting a complex formalism such as that of an ontology.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in **DOC-MODE**;
**What-Output:** vocabularies to be reused in the operational ontology.

**Support activities in parallel**

**Understand Vocabulary (KNO-VOCA)**
Study the classes and properties of the selected vocabularies; define which elements correspond to the operational ontology.

**Adopt Base Vocabularies (REU-BVOC)**
Select base vocabularies that support encoding (e.g., `owl`, `rdf`, `rdfs`, `xsd`).

**Adopt Vocabularies from Reused Ontologies (REU-RVOC)**
Select vocabularies from reused ontologies (foundational/core/domain) required to meet the CQs and traceability.

**Running Example (OntoMI):**
For **OntoMI**, the following vocabularies are reused:

* **OWL:** `http://www.w3.org/2002/07/owl#`
* **RDF:** `http://www.w3.org/1999/02/22-rdf-syntax-ns#`
* **RDFS:** `http://www.w3.org/2000/01/rdf-schema#`
* **XSD:** `http://www.w3.org/2001/XMLSchema#`
* **DCTERMS:** `http://purl.org/dc/terms/`
* **PROV-O:** `http://www.w3.org/ns/prov#`
* **SKOS:** `http://www.w3.org/2004/02/skos/core#`
* **BFO:** `http://purl.obolibrary.org/obo/BFO_`
* **IAO:** `http://purl.obolibrary.org/obo/IAO_`
* **RO:** `http://purl.obolibrary.org/obo/RO_`
* **QUDT:** `http://qudt.org/schema/qudt/` and `http://qudt.org/vocab/unit/`
* **OA (Web Annotation):** `http://www.w3.org/ns/oa#` *(or)* **NIF 2.0:** `http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#` (for text selectors)
* **OntoMI namespace (this work):** `https://w3id.org/ontomi#`

---

## 1.3 Define Ontology Encoding (DES-CODE)

**Design activity** that defines the coding to be applied in the operational ontology, i.e., the structure of the elements that represent the reference ontology in the operational language.

This activity indicates how the architecture of the operational ontology will be derived from the reference ontology, considering the defined coding language. From the conceptual model, define which **concepts** and **relationships** will be represented as **classes** and **properties**; define taxonomies via `rdfs:subClassOf`, object/data properties, domains/ranges, and restrictions. Establish **naming conventions**, **namespaces**, and **module organization** to preserve traceability and enable distributed implementation.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Reference Ontology Document prepared in **DOC-MODE**;
**What-Output:** coding of the operational ontology.

**Support activities in parallel**

**Map Reference Ontology (KNO-MAP)**
Map concepts/relations from the reference model to OWL classes/properties. Define object vs. data properties, cardinality restrictions (`owl:Restriction`), and alignments to reused vocabularies.

**Running Example (OntoMI):**

* **Namespaces & Version IRI**

  * Base IRI: `https://w3id.org/ontomi#`
  * Ontology IRI (versioned): `https://w3id.org/ontomi/1.1.0`
  * Prefix: `ontomi:`

* **Module Architecture (operational):**

  * `ontomi-core.ttl` — `Intelligence`, `Evocation`, `Intensity` and core relations.
  * `ontomi-text.ttl` — `EducationalDocument`, `TextSegment`, OA/NIF selectors.
  * `ontomi-evidence.ttl` — `Evidence` and subclasses (`KeywordEvidence`, `DiscourseStrategyEvidence`, `ContextObjectEvidence`).
  * `ontomi-prov.ttl` — PROV-aligned `AttributionActivity`, `Agent`, links to DCTERMS metadata.
  * `ontomi-profile.ttl` — document-level MI vectors/aggregations.
  * `ontomi-align.ttl` — alignments to BFO/IAO/RO/QUDT/PROV-O/OA (via `rdfs:subClassOf`, `owl:equivalentClass`, `owl:equivalentProperty`, or `rdfs:seeAlso`).

* **Class Mapping (examples):**

  * `ontomi:Intelligence` — **class** (taxonomy enumerates MI subclasses, may be `skos:Concept`-aligned).
  * `ontomi:Evocation` — **class**; aligns to BFO processual entity (via `rdfs:subClassOf`).
  * `ontomi:TextSegment` — **class**; `rdfs:subClassOf iao:IAO_0000030` (information content entity).
  * `ontomi:Evidence` — **class**; subclasses per evidence type.
  * `ontomi:AttributionActivity` — **class**; `rdfs:subClassOf prov:Activity`.
  * `ontomi:MIProfile` — **class** for aggregated vectors.

* **Object Properties (examples):**

  * `ontomi:evokesMI (Evocation → Intelligence)` — **functional** (exactly one).
  * `ontomi:isAboutSegment (Evocation → TextSegment)` — **functional** (exactly one).
  * `ontomi:hasEvidence (Evocation → Evidence)` — **min 1**.
  * `ontomi:wasGeneratedBy (Evocation → AttributionActivity)` — subPropertyOf `prov:wasGeneratedBy`.
  * `ontomi:wasAssociatedWith (AttributionActivity → prov:Agent)` — subPropertyOf `prov:wasAssociatedWith`.

* **Datatype Properties (examples):**

  * `ontomi:intensityValue (Evocation → xsd:decimal)` with `0 ≤ value ≤ 1`.
  * `ontomi:selectorStart`, `ontomi:selectorEnd` (TextSegment → xsd:integer) when OA/NIF not used directly.
  * `dcterms:created`, `dcterms:creator`, `dcterms:source` used on documents and assertions.

* **Restrictions (illustrative):**

  * `Evocation ⊑ (=1 evokesMI.Intelligence) ⊓ (=1 isAboutSegment.TextSegment) ⊓ (≥1 hasEvidence.Evidence)`
  * `Evidence ⊑ ( =1 rdf:type.(KeywordEvidence ⊔ DiscourseStrategyEvidence ⊔ ContextObjectEvidence) )` *(operationalized via SHACL in implementation)*

* **Naming & IRI Policy:**

  * **Classes:** `PascalCase` (e.g., `TextSegment`, `AttributionActivity`).
  * **Properties:** `camelCase` (e.g., `hasEvidence`, `isAboutSegment`).
  * **Individuals:** `kebab-case` with scoped prefixes per module:

    * `doc:doc-physics-101`, `seg:physics-101-p003`, `ev:ev-00021`, `evd:evd-kword-12`.
  * **Versioning:** semantic versioning in ontology header; `owl:versionIRI` and `owl:versionInfo`.

* **Reasoning/Profiles:**

  * Target **OWL 2 DL**.
  * Ensure compatibility with standard reasoners (HermiT/ELK) and SHACL engines (shacl-js/pySHACL) in later phases.

---

## 1.4 Document Premise of Operational Ontology (DOC-OPER)

**Documentation activity** that documents the assumptions of the operational ontology through the **Operational Ontology Document**, which should include:

* **Coding Language:** identification of the coding language to be used;
* **Vocabularies:** prefix identifying the vocabulary and its definition;
* **Coding Rules:** description of the rules to be applied;
* **Architecture:** description/representation of the architecture to be adopted.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** activities performed in the Design Phase;
**What-Output:** Operational Ontology Document with its respective assumptions.

**Running Example (OntoMI):**
**Table 6.1: Operational Ontology Document**

* **Document:** Operational Ontology
* **Ontology:** OntoMI — Multiple Intelligences Evocation
* **Version:** v1.1.0
* **Date:** Oct 27, 2025

**Coding Language:**

* **OWL 2 DL**, canonical serialization **Turtle (TTL)**.

**Vocabularies:**

| Prefix | Definition                                                                                                                         |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| owl    | [http://www.w3.org/2002/07/owl#](http://www.w3.org/2002/07/owl#)                                                                   |
| rdf    | [http://www.w3.org/1999/02/22-rdf-syntax-ns#](http://www.w3.org/1999/02/22-rdf-syntax-ns#)                                         |
| rdfs   | [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)                                                     |
| xsd    | [http://www.w3.org/2001/XMLSchema#](http://www.w3.org/2001/XMLSchema#)                                                             |
| dct    | [http://purl.org/dc/terms/](http://purl.org/dc/terms/)                                                                             |
| prov   | [http://www.w3.org/ns/prov#](http://www.w3.org/ns/prov#)                                                                           |
| skos   | [http://www.w3.org/2004/02/skos/core#](http://www.w3.org/2004/02/skos/core#)                                                       |
| bfo    | [http://purl.obolibrary.org/obo/BFO](http://purl.obolibrary.org/obo/BFO)_                                                          |
| iao    | [http://purl.obolibrary.org/obo/IAO](http://purl.obolibrary.org/obo/IAO)_                                                          |
| ro     | [http://purl.obolibrary.org/obo/RO](http://purl.obolibrary.org/obo/RO)_                                                            |
| qudt   | [http://qudt.org/schema/qudt/](http://qudt.org/schema/qudt/)                                                                       |
| unit   | [http://qudt.org/vocab/unit/](http://qudt.org/vocab/unit/)                                                                         |
| oa     | [http://www.w3.org/ns/oa#](http://www.w3.org/ns/oa#)                                                                               |
| nif    | [http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#](http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#) |
| ontomi | [https://w3id.org/ontomi#](https://w3id.org/ontomi#)                                                                               |

**Coding Rules:**

| Rule              | Definition                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------ |
| Class Name        | `PascalCase` from reference concepts (no spaces/hyphen/underscore).                              |
| Property Name     | `camelCase`; if ambiguous, suffix with target (e.g., `hasEvidenceItem`).                         |
| Individual IRI    | Scoped prefix + `kebab-case` ID (e.g., `ev:ev-00021`, `seg:physics-101-p003`).                   |
| Class Description | Use `rdfs:comment` (en) and optional `skos:definition`.                                          |
| Specialization    | Use `rdfs:subClassOf`.                                                                           |
| Disjointness      | Use `owl:disjointWith` for parallel siblings where applicable.                                   |
| Datatypes         | Prefer `xsd:decimal` (intensity), `xsd:integer` (offsets), `xsd:string` (labels).                |
| Alignment         | Use `rdfs:subClassOf`/`owl:equivalentClass`/`owl:equivalentProperty` to BFO/IAO/RO/QUDT/PROV/OA. |
| Versioning        | Provide `owl:versionIRI` and `owl:versionInfo` with SemVer.                                      |
| Annotations       | `dct:creator`, `dct:created`, `dct:source`, `prov:wasGeneratedBy` on assertion graphs.           |

**Architecture (Modules):**

| Ontology (file)       | Description                                                |
| --------------------- | ---------------------------------------------------------- |
| `ontomi-core.ttl`     | Core MI, Evocation, Intensity classes and core properties. |
| `ontomi-text.ttl`     | Documents, TextSegment, OA/NIF selectors.                  |
| `ontomi-evidence.ttl` | Evidence and its subtypes; relations to Evocation.         |
| `ontomi-prov.ttl`     | AttributionActivity, Agent; provenance links.              |
| `ontomi-profile.ttl`  | Aggregations and MI profiles/vectors.                      |
| `ontomi-align.ttl`    | External alignments (BFO/IAO/RO/QUDT/PROV/OA).             |

---

## 1.5 Control Premise of Operational Ontology (MAN-OPER)

**Configuration Management activity** that controls the changes, versions and deliveries of the information registered in the Operational Ontology Document (DOC-OPER).

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Operational Ontology Document prepared in **DOC-OPER**;
**What-Output:** control of the Operational Ontology Document.

**Running Example (OntoMI):**
Headers include version/date; repository control via Git tags (e.g., `ontomi-opspec-v1.1.0`) and `CHANGELOG.md` entries synchronized with releases of TTL modules.

---

## 1.6 Evaluate Premise of Operational Ontology (EVA-OPER)

**Evaluation activity** that assesses whether the information registered in the Operational Ontology Document meets the expectations of the ontology owner and is in accordance with the ontology and quality requirements defined in the Requirements Phase. Validation is performed by technical review with the ontology owner; iterate when necessary.

**Activity definition:**
**Who:** ontology engineer and ontology owner as responsible;
**What-Input:** the Ontology Specification Document and the Reference Ontology Document prepared in the Requirements and Capture Phases;
**What-Output:** evaluation of the Operational Ontology Document.

**Running Example (OntoMI):**
Review meetings verify: (i) the chosen encoding (OWL 2 DL) supports CQ1–CQ3; (ii) vocabularies cover text anchoring, provenance and measurement; (iii) coding rules ensure traceability from conceptual to operational elements; (iv) module architecture reflects the reference modularization and NFRs (performance, interoperability, maintainability).
