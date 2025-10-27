# Competency Questions (CQ1–CQ3) and SPARQL Examples

This document lists the core competency questions defined for OntoMI and provides **ready-to-run SPARQL** examples. Adjust prefixes and graph IRIs as needed for your triplestore / Protégé setup.

---

## Prefixes (adjust as needed)

```sparql
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl:  <http://www.w3.org/2002/07/owl#>
PREFIX xsd:  <http://www.w3.org/2001/XMLSchema#>

# Top-level & OBO-style
PREFIX bfo:  <http://purl.obolibrary.org/obo/BFO_>
PREFIX iao:  <http://purl.obolibrary.org/obo/IAO_>

# OntoMI (change to your base IRI)
PREFIX onto: <http://purl.org/ontomi#>
```

Key classes/properties used below:

- `onto:ExplanationFragment`
- `onto:ExplanationElement` (abstract), with subclasses `onto:Keyword`, `onto:ContextObject`, `onto:DiscursiveStrategy`
- `onto:Intelligence`
- `onto:IntelligenceActivation`
- `onto:usesElement` (fragment → element)
- `onto:evokesIntelligence` (element → intelligence)
- `onto:hasActivation` (fragment → activation)
- `onto:refersTo` (activation → intelligence)
- `onto:hasType` (activation → string; e.g., "primary" / "secondary")
- `onto:hasActivationScore` (activation → xsd:decimal; functional)
- `onto:miVector` (fragment → literal; 8-position vector; optional, derived)

> **Note**: Depending on your file, some annotations (labels, comments) may be at `rdfs:label` or `iao:IAO_0000115` (definition). Replace as needed in the examples.

---

## CQ1 — Which multiple intelligences are evoked in a given explanatory fragment?

### Variant A — Using reified activations (recommended if ABox materializes activations)
Returns all activations for a fragment, with intelligence, type, and score (if present).

```sparql
SELECT ?fragment ?fragmentLabel ?activation ?intelligence ?intLabel ?type ?score
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }  # ← set your fragment URI
  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }

  ?fragment onto:hasActivation ?activation .
  ?activation onto:refersTo ?intelligence .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }
  OPTIONAL { ?activation onto:hasType ?type . }
  OPTIONAL { ?activation onto:hasActivationScore ?score . }
}
ORDER BY DESC(?score) ?intLabel
```

### Variant B — Deriving activations via elements (if no activations are materialized)
Lists intelligences *evoked* by elements used in the fragment.

```sparql
SELECT DISTINCT ?fragment ?fragmentLabel ?intelligence ?intLabel
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }  # ← set your fragment URI
  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }

  ?fragment onto:usesElement ?el .
  ?el onto:evokesIntelligence ?intelligence .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }
}
ORDER BY ?intLabel
```

---

## CQ2 — Which semantic elements contributed to the evocation?

Lists **elements** (keyword / context object / discursive strategy) that contributed to each evoked intelligence in the fragment.

```sparql
SELECT ?fragment ?fragmentLabel ?el ?elLabel ?elType ?intelligence ?intLabel
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }  # ← set your fragment URI
  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }

  ?fragment onto:usesElement ?el .
  OPTIONAL { ?el rdfs:label ?elLabel . }

  # classify element type by rdf:type
  VALUES ?elClass { onto:Keyword onto:ContextObject onto:DiscursiveStrategy }
  ?el rdf:type ?elClass .
  BIND(STRAFTER(STR(?elClass), "#") AS ?elType)

  ?el onto:evokesIntelligence ?intelligence .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }
}
ORDER BY ?elType ?elLabel ?intLabel
```

If you materialize **activations** and **scores**, you can cross-walk elements to activations of the **same intelligence**:

```sparql
SELECT ?el ?elLabel ?elType ?intelligence ?intLabel ?activation ?score
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }

  ?fragment onto:usesElement ?el .
  OPTIONAL { ?el rdfs:label ?elLabel . }
  VALUES ?elClass { onto:Keyword onto:ContextObject onto:DiscursiveStrategy }
  ?el rdf:type ?elClass .
  BIND(STRAFTER(STR(?elClass), "#") AS ?elType)

  ?el onto:evokesIntelligence ?intelligence .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }

  # link to activation(s) for the same fragment & intelligence
  ?fragment onto:hasActivation ?activation .
  ?activation onto:refersTo ?intelligence .
  OPTIONAL { ?activation onto:hasActivationScore ?score . }
}
ORDER BY ?intLabel DESC(?score) ?elType ?elLabel
```

---

## CQ3 — In cases of multiple activations, which intelligence manifests with greater intensity?

### Variant A — Using `onto:hasActivationScore` to compute primary vs. secondary
Returns the **top-scoring intelligence** (primary) and lists the rest (secondary).

```sparql
# Primary intelligence (highest score) for a given fragment
SELECT ?fragment ?fragmentLabel ?intelligence ?intLabel ?score
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }

  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }
  ?fragment onto:hasActivation ?a .
  ?a onto:refersTo ?intelligence ;
     onto:hasActivationScore ?score .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }
}
ORDER BY DESC(?score)
LIMIT 1
```

```sparql
# All intelligences ranked by score (primary + secondary)
SELECT ?fragment ?fragmentLabel ?intelligence ?intLabel (MAX(?score) AS ?rankScore)
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }

  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }
  ?fragment onto:hasActivation ?a .
  ?a onto:refersTo ?intelligence ;
     onto:hasActivationScore ?score .
  OPTIONAL { ?intelligence rdfs:label ?intLabel . }
}
GROUP BY ?fragment ?fragmentLabel ?intelligence ?intLabel
ORDER BY DESC(?rankScore) ?intLabel
```

### Variant B — Reading the derived 8-slot MI vector (if materialized)
If `onto:miVector` is materialized on the fragment (e.g., "[0.72,0.14, ...]"), this query retrieves it.

```sparql
SELECT ?fragment ?fragmentLabel ?vector
WHERE {
  VALUES ?fragment { <http://purl.org/ontomi#fragment_exemplo_1> }
  OPTIONAL { ?fragment rdfs:label ?fragmentLabel . }
  ?fragment onto:miVector ?vector .
}
```

> **Tip**: If the vector is stored as a string literal, consider a convention such as JSON array or comma-separated values and parse it in your consuming application.

---

## Sanity/Integrity checks (optional)

Ensure modeling consistency for core constraints used by OntoMI.

```sparql
# Elements must be one of the three specializations (disjointness not shown here)
SELECT ?el ?elLabel ?typeFound
WHERE {
  ?el rdf:type onto:ExplanationElement .
  OPTIONAL { ?el rdfs:label ?elLabel . }
  FILTER NOT EXISTS { ?el rdf:type onto:Keyword }
  FILTER NOT EXISTS { ?el rdf:type onto:ContextObject }
  FILTER NOT EXISTS { ?el rdf:type onto:DiscursiveStrategy }
  BIND("Missing specific subclass" AS ?typeFound)
}
```

```sparql
# Functional property: each activation should have at most one hasActivationScore
SELECT ?a (COUNT(?s) AS ?scores)
WHERE {
  ?a rdf:type onto:IntelligenceActivation ;
     onto:hasActivationScore ?s .
}
GROUP BY ?a
HAVING (COUNT(?s) > 1)
```

---

## Notes

- Replace fragment URIs (`onto:fragment_exemplo_1`) with your local instances.
- If you prefer `iao:IAO_0000115` (definition) instead of `rdfs:label`, update the OPTIONAL label clauses.
- Aggregation semantics can be adapted (e.g., sum of scores per intelligence) if your inference pipeline generates multiple activations per intelligence per fragment.
