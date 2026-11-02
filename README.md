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

## Current checkpoint — 2026-11-02

- **Can explain:** contrastive-learning intuition and false negatives; augmentation choices; frozen encoders and linear probes; CLIP-style image–text alignment, zero-shot classification and encoder compatibility.
- **Introduced:** BYOL's student, momentum teacher, stop-gradient and predictor; DINO's output distributions, centering and sharpening. Consolidation still needed.
- **Can apply (hypothetical experiments):** matching slide-level reports with slide representations; testing centre shortcuts and stain dependence; using linear probes before and after projection to investigate weak zero-shot performance.
- **Next session:** briefly retrieve linear probes versus zero-shot prediction, then consolidate multimodal alignment through one concrete model example.
- **Retrieval question:** If linear probes work before and after image projection but zero-shot malignancy prediction fails, what does that suggest—and what does it not prove?
- **Still unclear:** independently explaining how DINO's centering and sharpening complement each other; how BYOL's components work together to avoid collapse. Detailed mechanisms of CONCH, TITAN and mSTAR have not yet been studied.
- **Latest session:** first dedicated multimodal discussion. Distinguished report matching, stain robustness and malignancy prediction; designed comparisons to investigate shortcut learning and projection bottlenecks. See [Multimodal AI](05-Multimodal-AI.md).
- **Format:** short notes per topic: meaning, uses, pitfalls and tools/methods. Keep sessions focused, with fewer questions and an earlier stopping point; use equations only when they aid reasoning.

Public notes only: exclude private data, institutional paths and unpublished results. Review session notes before committing unless an explicit request authorizes the update.
