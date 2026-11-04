# Ai-toolbelt
Notes on my learning journey of methods for deep learning science tasks. 

## Curriculum

Populate topic files gradually through lessons.

1. 01-Foundations.md — planned
2. [02-Representation-Learning.md](02-Representation-Learning.md)
3. 03-Transformers.md — planned
4. 04-Foundation-Models.md — planned
5. [05-Multimodal-AI.md](05-Multimodal-AI.md)
6. 06-Generative-AI.md — planned
7. 07-Graph-Neural-Networks.md — planned
8. 08-Applications.md — planned

## Current checkpoint — 2026-11-04

- **Can explain:** contrastive-learning intuition and false negatives; augmentation choices; frozen encoders and linear probes; CLIP-style image–text alignment, zero-shot classification and encoder compatibility; MAE's core intuition of reconstructing hidden content from visible context.
- **Introduced:** BYOL's student, momentum teacher, stop-gradient and predictor; DINO's output distributions, centering and sharpening. Consolidation still needed.
- **Can apply (hypothetical experiments):** matching slide-level reports with slide representations; testing centre shortcuts and stain dependence; using linear probes before and after projection to investigate weak zero-shot performance.
- **Next session:** compare pixel reconstruction with predicting learned representations, connecting MAE to iBOT. Move forward from the already-covered linear-probe versus zero-shot distinction.
- **Retrieval question:** Why does heavy random masking reduce local reconstruction shortcuts, and what goes wrong if too much context is hidden?
- **Still unclear:** independently explaining how DINO's centering and sharpening complement each other; how BYOL's components work together to avoid collapse. Detailed mechanisms of CONCH, TITAN and mSTAR have not yet been studied.
- **Latest session:** introduced MAE's encoder–decoder setup, random masking, reconstruction ambiguity and the distinction between reconstruction quality and encoder usefulness. Identified PLUTO, Prov-GigaPath and scFoundation/xTrimoGene as examples with different reconstruction targets; detailed mechanisms remain unstudied. See [Representation learning](02-Representation-Learning.md#masked-autoencoders-mae).
- **Format:** short notes per topic: meaning, uses, pitfalls and tools/methods. Aim for focused 15-minute sessions: at most one brief retrieval question, one new mechanism and one application, followed by short notes. Avoid repeatedly testing demonstrated understanding. Use equations only when they aid reasoning.

Public notes only: exclude private data, institutional paths and unpublished results. Review session notes before committing unless an explicit request authorizes the update.
