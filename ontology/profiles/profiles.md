# Ontology profiles & policies

- **OWL profile**: OWL 2 DL (Turtle `.ttl` serialization).
- **IRIs**: base IRI `http://purl.org/ontomi/onto#` (example—adjust to your PURL).
- **Naming**: Classes (PascalCase), Object/Data properties (camelCase), individuals (lower-hyphen).
- **Annotations**: OBO-style (`rdfs:label`, `IAO:0000115` definition, synonyms, editor notes).
- **Imports**: BFO, IAO via PURLs (declared inside `ontology/src/ontomi.ttl`).
- **Version IRI**: use semantic versioning and release tags.
