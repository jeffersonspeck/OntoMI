# 1. Implementation Phase

The Implementation Phase aims to implement the reference ontology produced in the Capture Phase into an operational ontology, according to the design specifications elaborated in the Design Phase. This phase transforms the reference ontology into a machine-interpretable ontology, making it available for use in applications, decision support, and domain reasoning.

---

## 1.1 Code Concepts (IMP-CONC)

**Implementation activity** that encodes the concepts of the reference ontology as elements of the formal operational ontology language, according to the assumptions defined in the Operational Ontology Document. For OWL, concepts are encoded as **classes**.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Operational Ontology Document from **DOC-OPER**;
**What-Output:** concepts encoded in the operational ontology.

**Running Example (OntoMI):**
Listing 1.1: Fragment of concepts in OntoMI’s operational ontology (TTL).

```turtle
@prefix ontomi: <https://w3id.org/ontomi#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .
@prefix iao:    <http://purl.obolibrary.org/obo/IAO_> .
@prefix owl:    <http://www.w3.org/2002/07/owl#> .

ontomi:Intelligence a owl:Class ;
  rdfs:comment "Multiple Intelligences category (e.g., Linguistic, Logical-Mathematical, Spatial...)." .

ontomi:TextSegment a owl:Class ;
  rdfs:subClassOf iao:IAO_0000030 ;  # Information Content Entity
  rdfs:comment "Bounded fragment of a document (sentence/paragraph) that may evoke MI." .

ontomi:Evocation a owl:Class ;
  rdfs:comment "Assertion that a TextSegment evokes an Intelligence with a measurable intensity." .

ontomi:Evidence a owl:Class ;
  rdfs:comment "Observable semantic element supporting an Evocation." .

ontomi:KeywordEvidence a owl:Class ;
  rdfs:subClassOf ontomi:Evidence .

ontomi:DiscourseStrategyEvidence a owl:Class ;
  rdfs:subClassOf ontomi:Evidence .

ontomi:ContextObjectEvidence a owl:Class ;
  rdfs:subClassOf ontomi:Evidence .
```

---

## 1.2 Code Relations (IMP-RELC)

**Implementation activity** that encodes the relations of the reference ontology as properties and constraints, according to the assumptions defined in the Operational Ontology Document. For OWL, relations are **object/data properties** and **restrictions**.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Operational Ontology Document from **DOC-OPER**;
**What-Output:** relations encoded in the operational ontology.

**Running Example (OntoMI):**
Listing 1.2: Fragment of relations in OntoMI (TTL).

```turtle
@prefix ontomi: <https://w3id.org/ontomi#> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .
@prefix owl:    <http://www.w3.org/2002/07/owl#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .

ontomi:evokesMI a owl:ObjectProperty , owl:FunctionalProperty ;
  rdfs:domain ontomi:Evocation ;
  rdfs:range  ontomi:Intelligence ;
  rdfs:comment "Exactly one Intelligence per Evocation." .

ontomi:isAboutSegment a owl:ObjectProperty , owl:FunctionalProperty ;
  rdfs:domain ontomi:Evocation ;
  rdfs:range  ontomi:TextSegment ;
  rdfs:comment "Exactly one TextSegment per Evocation." .

ontomi:hasEvidence a owl:ObjectProperty ;
  rdfs:domain ontomi:Evocation ;
  rdfs:range  ontomi:Evidence ;
  rdfs:comment "An Evocation must have at least one Evidence." .

ontomi:intensityValue a owl:DatatypeProperty ;
  rdfs:domain ontomi:Evocation ;
  rdfs:range  xsd:decimal ;
  rdfs:comment "Evocation strength in [0,1]." .
```

---

## 1.3 Code Axioms (IMP-AXIO)

**Implementation activity** that encodes the axioms defined in the reference ontology according to the operational language.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** Operational Ontology Document from **DOC-OPER**;
**What-Output:** axioms encoded in the operational ontology.

**Running Example (OntoMI):**
Listing 1.3: Fragment of axioms in OntoMI (TTL; disjointness and cardinalities).

```turtle
@prefix ontomi: <https://w3id.org/ontomi#> .
@prefix owl:    <http://www.w3.org/2002/07/owl#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .

# Disjoint evidence kinds
[] a owl:AllDisjointClasses ;
   owl:members ( ontomi:KeywordEvidence
                 ontomi:DiscourseStrategyEvidence
                 ontomi:ContextObjectEvidence ).

# Evocation has exactly one Intelligence and one TextSegment; at least one Evidence
ontomi:Evocation rdfs:subClassOf
  [ a owl:Restriction ; owl:onProperty ontomi:evokesMI ; owl:qualifiedCardinality "1"^^xsd:nonNegativeInteger ; owl:onClass ontomi:Intelligence ],
  [ a owl:Restriction ; owl:onProperty ontomi:isAboutSegment ; owl:qualifiedCardinality "1"^^xsd:nonNegativeInteger ; owl:onClass ontomi:TextSegment ],
  [ a owl:Restriction ; owl:onProperty ontomi:hasEvidence ; owl:minQualifiedCardinality "1"^^xsd:nonNegativeInteger ; owl:onClass ontomi:Evidence ] .
```

*(In practice, the numeric literals use `xsd:nonNegativeInteger`; the interval constraint [0,1] for `intensityValue` is enforced via SHACL in the Validation Phase.)*

---

## 1.4 Document Operational Ontology (DOC-OPER)

**Documentation activity** that documents the operational ontology in the coding language defined in **DES-LANG**, following the results of the previous activities and the assumptions defined in **DOC-OPER**.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** results from previous Implementation activities;
**What-Output:** operational ontology in the defined language.

**Running Example (OntoMI):**
Listing 1.4: Ontology header and a sample class (TTL).

```turtle
@prefix ontomi: <https://w3id.org/ontomi#> .
@prefix owl:    <http://www.w3.org/2002/07/owl#> .
@prefix dct:    <http://purl.org/dc/terms/> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .

<https://w3id.org/ontomi/1.1.0> a owl:Ontology ;
  owl:versionIRI <https://w3id.org/ontomi/1.1.0> ;
  owl:versionInfo "1.1.0" ;
  dct:title "OntoMI — Multiple Intelligences Evocation Ontology" ;
  dct:created "2025-10-27"^^xsd:date ;
  dct:creator "OntoMI Team" ;
  dct:license <https://creativecommons.org/licenses/by/4.0/> .

ontomi:Intelligence a owl:Class .
```

---

## 1.5 Control Operational Ontology (MAN-OPER)

**Configuration Management activity** that controls the changes, versions and deliveries of the information registered in the operational ontology, described in **DOC-OPER**. Use ontology metadata (e.g., `owl:versionIRI`, `owl:versionInfo`) and repository tooling (e.g., Git tags/releases) to track evolution.

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** operational ontology from **DOC-OPER**;
**What-Output:** controlled versions and delivery records.

**Running Example (OntoMI):**
The ontology uses `owl:versionInfo "1.1.0"`, `owl:versionIRI <.../1.1.0>`, and repository tags `v1.1.0` with a `CHANGELOG.md` aligned to SemVer.

---

## 1.6 Evaluate Operational Ontology (EVA-OPER)

**Evaluation activity** that assesses whether the information recorded in the operational ontology meets the expectations of the ontology owner and is in accordance with the ontology and quality requirements defined in the Requirements Phase.

* **Validation:** instantiate real scenarios as individuals.
* **Verification:** translate competency questions (CQs) into queries and check answers on the instantiated ontology (SPARQL for OWL).
* **Testing levels:** Subontology Test, Integration Test, Ontology Test (including stress, performance, inference).

**Activity definition:**
**Who:** ontology engineer and ontology owner as responsible;
**What-Input:** Ontology Specification Document (Requirements) and the operational ontology (DOC-OPER);
**What-Output:** evaluation results of the operational ontology.

**Running Example (OntoMI):**
Listing 1.5: Fragment of instances representing an explanatory paragraph and one evocation.

```turtle
@prefix ontomi: <https://w3id.org/ontomi#> .
@prefix dct:    <http://purl.org/dc/terms/> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .

ontomi:doc-physics-101 a ontomi:EducationalDocument ;
  dct:title "Physics 101: Newton's First Law" .

ontomi:seg-para-003 a ontomi:TextSegment ;
  dct:isPartOf ontomi:doc-physics-101 .

ontomi:LinguisticIntelligence a ontomi:Intelligence .

ontomi:ev-00021 a ontomi:Evocation ;
  ontomi:evokesMI ontomi:LinguisticIntelligence ;
  ontomi:isAboutSegment ontomi:seg-para-003 ;
  ontomi:intensityValue "0.78"^^xsd:decimal ;
  ontomi:hasEvidence ontomi:evd-kword-12 .

ontomi:evd-kword-12 a ontomi:KeywordEvidence ;
  dct:description "Recurrent lexical cues and cohesive markers" .
```

Listing 1.6: SPARQL queries that answer CQs.

* **CQ1 (Which MI are evoked in a given segment?):**

```sparql
SELECT ?mi WHERE {
  ?e a ontomi:Evocation ;
     ontomi:isAboutSegment ontomi:seg-para-003 ;
     ontomi:evokesMI ?mi .
}
```

* **CQ2 (Which evidence supports a given evocation?):**

```sparql
SELECT ?evidence ?etype WHERE {
  ontomi:ev-00021 ontomi:hasEvidence ?evidence .
  ?evidence a ?etype .
}
```

* **CQ3 (Which intelligence manifests with highest intensity per segment?):**

```sparql
SELECT ?segment ?mi (MAX(?score) AS ?topScore)
WHERE {
  ?e a ontomi:Evocation ;
     ontomi:isAboutSegment ?segment ;
     ontomi:evokesMI ?mi ;
     ontomi:intensityValue ?score .
}
GROUP BY ?segment ?mi
ORDER BY DESC(?topScore)
```

---

## 1.7 Publish Operational Ontology (PUB-OPER)

**Publication activity** that publishes the Operational Ontology produced in **DOC-OPER** (e.g., in versioned `TTL` files, with documentation and SHACL shapes).

**Activity definition:**
**Who:** ontology engineer as responsible;
**What-Input:** operational ontology from **DOC-OPER**;
**What-Output:** operational ontology made available.

**Running Example (OntoMI):**
The operational ontology is published in the project repository under `ontomi/` with modules: `ontomi-core.ttl`, `ontomi-text.ttl`, `ontomi-evidence.ttl`, `ontomi-prov.ttl`, `ontomi-profile.ttl`, and `ontomi-align.ttl`, plus `README.md`, `CHANGELOG.md`, and example SPARQL queries.
