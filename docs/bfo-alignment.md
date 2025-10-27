# BFO/IAO alignment for OntoMI (documentation)

> Alignment axioms are **embedded** in `ontology/src/ontomi.ttl`. This document records the intended mapping and rationale.

## Class mappings (informal summary)

- **onto:IntelligenceActivation ⊑ BFO:process**  
  *Rationale*: an activation is an occurrent (happens in time), possibly with start/end and participants (evidence, fragment).

- **onto:ExplanationFragment ⊑ IAO:InformationContentEntity**  
  *Rationale*: a fragment is an informational entity (ICE), a generically dependent continuant.

- **onto:ExplanationElement ⊑ IAO:InformationContentEntity**  
  and **onto:Keyword / onto:ContextObject / onto:DiscursiveStrategy ⊑ onto:ExplanationElement** (pairwise disjoint).

- **onto:Intelligence**  
  Modeled as a reference concept (can be aligned to an ICE that is_about cognitive competences).

- **onto:MIVector ⊑ IAO:DataItem** (or **IAO:Dataset** if persisted as a collection)  
  Holds eight numeric positions corresponding to MI dimensions.

## Property patterns

- **onto:usesElement**: `ExplanationFragment → ExplanationElement`  
  Domain/range set minimally; functional constraints not imposed.

- **onto:evokesIntelligence**: `ExplanationElement → Intelligence`  
  Optionally complemented by `IAO:is_about` when appropriate.

- **onto:hasActivation**: `ExplanationFragment → IntelligenceActivation`  
  Many activations per fragment allowed.

- **onto:refersTo**: `IntelligenceActivation → Intelligence` (exactly 1).

- **onto:hasType** (functional): `IntelligenceActivation → xsd:string` (e.g., "primary", "secondary").

- **onto:hasActivationScore**: `IntelligenceActivation → xsd:decimal`.

- **onto:hasMIVector**: `ExplanationFragment → MIVector`.

- **onto:hasVectorPosition**: `MIVector → xsd:decimal` (eight assertions in fixed order).

## Aboutness pattern (IAO)

Where suitable, use **IAO:is_about** to connect ICEs to the referenced `onto:Intelligence` individuals/classes.

## Disjointness and integrity

- `Keyword ⟂ ContextObject ⟂ DiscursiveStrategy` (pairwise disjoint).  
- `IntelligenceActivation` must `refersTo` exactly one `Intelligence`.  
- Each `MIVector` must have exactly eight `hasVectorPosition` values.
