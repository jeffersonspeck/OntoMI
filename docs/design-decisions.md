# Design decisions (OntoMI)

- **Foundational choice**: BFO as top-level ontology (ISO/IEC 21838-2) and IAO for information artifacts (OBO).  
  Motivations: rigor (continuant/occurrent), interoperability, reuse.
- **Core pattern**: fragment → elements → activations → MI vector.  
- **Reification**: `IntelligenceActivation` as a first-class occurrent with `hasType` (functional) and `hasActivationScore`.
- **Evidence modeling**: `ExplanationElement` specialized in `Keyword`, `ContextObject`, `DiscursiveStrategy`; disjointness declared.
- **Vector artifact**: `MIVector` holds eight positions derived from activation scores; linked via `hasMIVector`.
- **Minimal domains/ranges**: declare only what is necessary to support reasoning and validation; avoid overspecification.
- **Annotations**: OBO-style labels, definitions, synonyms, provenance notes.
- **Naming**: PascalCase for classes; camelCase for properties; lowercase-with-dashes for individuals if needed.
