# Evaluation plan

- **Consistency**: reasoner runs (HermiT/Pellet/ELK) must classify without unsatisfiable classes or property conflicts.
- **CQ coverage**: CQ1–CQ3 return expected answers over canonical instances.
- **Integrity** (SPARQL): domain/range violations, functional violations (`hasType`), disjointness, vector completeness (eight positions).
- **Quality metrics**: coverage and precision of activations over labeled examples; track over releases.
- **Regression**: fix baseline results and compare on each release; publish deltas in `releases/vX.Y.Z/checks/`.
