# OntoMI — Traceability Matrix (CQ → Axioms / Queries / Instances)

> Version: 1.0 (aligns OntoMI with CQs; compatible with BFO/IAO; OWL DL profile)  
> Scope: CQ1–CQ3. Each row points to the **last mile**: the axioms that make the query possible, the **canonical SPARQL** that must run, and the **gold set** of instances/expected outputs.

## Conventions
- Prefixes (examples): `onto:` (OntoMI), `rdf:`, `rdfs:`, `owl:`, `xsd:`, `bfo:`, `iao:`  
- Classes: `onto:ExplanationFragment`, `onto:ExplanationElement` (abstract), `onto:Keyword`, `onto:ContextObject`, `onto:DiscursiveStrategy`, `onto:Intelligence`, `onto:IntelligenceActivation`  
- Properties:  
  - Object: `onto:usesElement`, `onto:evokesIntelligence`, `onto:hasActivation`, `onto:refersTo`  
  - Data: `onto:hasType` (functional: `primary|secondary`)

---

## Traceability table

| CQ | Competency question | OWL axioms / entities (minimum) | Query file | Canonical instances | Expected output |
|----|---------------------|----------------------------------|------------|---------------------|-----------------|
| CQ1 | *Which intelligences are evoked in a given explanation fragment?* | Classes: `onto:ExplanationFragment`, `onto:Intelligence`; Properties: `onto:hasActivation` (domain=Fragment, range=Activation), `onto:refersTo` (Activation→Intelligence) | `queries/cq1.rq` | `examples/canonical/*.ttl` | `expected/cq1.tsv` |
| CQ2 | *Which semantic elements contributed to each evocation?* | Classes: `onto:ExplanationElement` (disjoint subclasses `Keyword`/`ContextObject`/`DiscursiveStrategy`); Properties: `onto:usesElement`, `onto:evokesIntelligence` | `queries/cq2.rq` | `examples/canonical/*.ttl` | `expected/cq2.tsv` |
| CQ3 | *What is the primary vs. secondary activation per fragment?* | Data property `onto:hasType` **functional** with values `primary|secondary`; linkage via `onto:hasActivation`/`onto:refersTo` | `queries/cq3.rq` | `examples/canonical/*.ttl` | `expected/cq3.tsv` |

> **SHACL** (recommended): `shapes/ontomi.shacl.ttl` validates disjointness, functional `hasType`, and typing of elements (`Keyword`/`ContextObject`/`DiscursiveStrategy`).

---|---|---|---|---|---|
| **CQ1** | “Which **intelligences** are evoked in a **fragment**?” | (1) `usesElement` dom=Fragment, range=Element; (2) `evokesIntelligence` dom=Element, range=Intelligence; (3) explicit disjointness between `Keyword`, `ContextObject`, `DiscursiveStrategy`; (4) `hasActivation` Fragment→Activation; (5) `refersTo` Activation→Intelligence; (6) `hasType` functional. | `queries/cq1.rq` | `examples/fragment_newton_01.ttl` · `examples/fragment_newton_02.ttl` | List of tuples `(activation, intelligence [, type])` per `Fragment` |
| **CQ2** | “Which **semantic elements** contributed to the **evocation**?” | (1) Same axioms as CQ1; (2) **contribution trail**: `Fragment --usesElement--> Element --evokesIntelligence--> Intelligence`; (3) `Activation --refersTo--> Intelligence` linked to the same `Fragment`. | `queries/cq2.rq` | `examples/fragment_newton_01.ttl` | Tuples `(fragment, activation, intelligence, element, elementType)` |
| **CQ3** | “If there are **multiple activations**, which one is **primary**?” | (1) `hasActivation` and `refersTo` as in CQ1; (2) `hasType` functional with value `primary` (or tie‑break in the heuristic) | `queries/cq3.rq` | `examples/fragment_newton_01.ttl` | 1 tuple per `Fragment`: `(fragment, activation, intelligence, type=primary)` |

---

## Canonical SPARQL queries

> **Note**: prefixes omitted for brevity. Adjust according to your `.ttl` files.

### `queries/cq1.rq` — Intelligences evoked by a fragment
```sparql
SELECT ?fragment ?activation ?intelligence ?type
WHERE {
  ?fragment a onto:ExplanationFragment .
  OPTIONAL { ?fragment onto:hasActivation ?activation .
             ?activation onto:refersTo ?intelligence .
             OPTIONAL { ?activation onto:hasType ?type } }
}
ORDER BY ?fragment ?intelligence
```

### `queries/cq2.rq` — Elements that contributed to the evocation
```sparql
SELECT ?fragment ?activation ?intelligence ?element ?elementType
WHERE {
  ?fragment a onto:ExplanationFragment ;
            onto:usesElement ?element .
  ?element onto:evokesIntelligence ?intelligence .
  ?activation a onto:IntelligenceActivation ;
              onto:refersTo ?intelligence .
  # bind the activation to the same fragment
  ?fragment onto:hasActivation ?activation .

  # report the element's type (subclass)
  VALUES ?elementType { onto:Keyword onto:ContextObject onto:DiscursiveStrategy }
  ?element a ?elementType .
}
ORDER BY ?fragment ?intelligence ?elementType
```

### `queries/cq3.rq` — Primary activation of the fragment
```sparql
SELECT ?fragment ?activation ?intelligence
WHERE {
  ?fragment a onto:ExplanationFragment ;
            onto:hasActivation ?activation .
  ?activation onto:hasType "primary" ;
              onto:refersTo ?intelligence .
}
```
---

## Gold set (instances & expectations)

| File | Description | CQ1 expectation | CQ2 expectation | CQ3 expectation |
|---|---|---|---|---|
| `examples/fragment_newton_01.ttl` | Fragment “sonic ritual / constant motion / external force” | 3–5 activations; includes `Kinesthetic` (strong), `Musical`, `Logical‑mathematical`, `Interpersonal` | Elements list `Keyword` (e.g., *rhythm*, *motion*), `ContextObject` (e.g., *platform*), `DiscursiveStrategy` (e.g., *dramatization*, *simulation*) | `Kinesthetic` as primary |
| `examples/fragment_newton_02.ttl` | Variant without the sonic ritual | 2–4 activations; drop in `Musical` | Contributions without sonic elements | Primary may switch between `Kinesthetic` and `Logical‑mathematical` |

> **SHACL** recommended: `shapes/ontomi.shacl.ttl` to ensure the minimum presence of `hasActivation/refersTo/hasType` and typing of elements (`Keyword`/`ContextObject`/`DiscursiveStrategy`).

---

## Ontology coverage (traceability checklist)

- [x] Explicit disjointness between `Keyword`, `ContextObject`, `DiscursiveStrategy`  
- [x] Minimal domains/ranges of `usesElement`, `evokesIntelligence`, `hasActivation`, `refersTo`  
- [x] `hasType` as `owl:FunctionalProperty` (canonical values)  
- [x] OBO‑style annotations (IAO: label, definition, source, version)  
- [x] Modules (core, activation, heuristics/queries, results) imported into the main file

> Any axiom change that affects these CQs must **update this matrix** and the corresponding **gold sets**.
