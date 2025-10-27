# Regression testing

1) Run reasoner over `ontology/src/ontomi.ttl` and export classification / unsat report.
2) Run SPARQL CQ queries against ontology + `examples/instances.ttl`.
3) Compare results to the previous release; record deltas in `ontology/releases/vX.Y.Z/checks/`.
4) Tag the release and update `ontology/releases/CHANGELOG.md` and `RELEASE-NOTES.md`.
