# CQ Guide

**CQ1** — Which intelligences are evoked in a given explanatory fragment?  
Run `evaluation/cq/cq1.rq` with your fragment IRI bound (or use FILTER by label).

**CQ2** — Which elements contributed to each evocation?  
Run `evaluation/cq/cq2.rq` and inspect element–intelligence links.

**CQ3** — In cases of multiple activations, which intelligence is primary?  
Run `evaluation/cq/cq3.rq`, which orders activations by `hasActivationScore` and filters `hasType = "primary"` when available.

## MI vector (8 positions)

Order (document your canonical order here and keep it stable across releases), e.g.:  
1. Bodily-kinesthetic  
2. Interpersonal  
3. Intrapersonal  
4. Linguistic  
5. Logical-mathematical  
6. Musical  
7. Spatial-visual  
8. Naturalistic (if modeled) or another agreed dimension

`MIVector` stores these eight values via repeated `hasVectorPosition` assertions.
