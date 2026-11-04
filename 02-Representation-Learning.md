# Representation learning

Short notes from 2026-11-01. Progress describes demonstrated understanding, not mastery.

## Contrastive learning and InfoNCE
Status: **can explain** the core intuition.

- **What this means:** Learn embeddings by making augmented views of the same input similar relative to competing examples. InfoNCE treats this as finding the matching view among candidates; a high positive similarity alone is insufficient.
- **When it can be used:** Pretraining an encoder on unlabelled data, such as histology tiles, before training a downstream predictor.
- **Pitfalls:** Matching positives alone permits constant embeddings (collapse). Different tiles can share biology, so treating them as negatives can push useful similarities apart. Avoiding collapse does not establish biological usefulness.
- **Tools / methods using it:** [SimCLR](https://github.com/google-research/simclr), [MoCo](https://github.com/facebookresearch/moco). These are training methods with reference implementations, not encoder architectures.

## BYOL and momentum teachers
Status: **introduced**; components recalled, mechanism needs consolidation.

- **What this means:** A student predicts a teacher's representation of another augmented view without explicit negatives. The teacher receives no gradient updates and follows a moving average of student weights. The student has an additional predictor; both networks can start from identical random weights.
- **When it can be used:** Learning representations from unlabelled images for downstream tasks.
- **Pitfalls:** A slowly changing teacher alone does not guarantee avoidance of collapse; the full training design matters. Usually use encoder embeddings downstream and discard pretraining projection/prediction heads.
- **Tools / methods using it:** [BYOL reference implementation](https://github.com/google-deepmind/deepmind-research/tree/master/byol). DINO is related through teacher–student training; see the introductory notes below.

## Augmentation and invariance
Status: **can explain**; applied to a hypothetical stain example.

- **What this means:** Agreement across augmented views encourages representations to tolerate the differences introduced between them.
- **When it can be used:** Independently varying plausible staining between histology views can encourage reliance on morphology.
- **Pitfalls:** Shared stain changes can leave a matching shortcut. Excessive augmentation can destroy relevant features. Stain invariance is task-dependent and encouraged rather than guaranteed; embeddings may retain both stain and biology.
- **Tools / methods using it:** SimCLR and BYOL both learn across augmented image views; see their implementations above.

## Frozen encoders and linear probes
Status: **can explain** the evaluation distinction.

- **What this means:** Freeze the encoder and train only a linear classifier on its embeddings. This tests whether task signal is linearly accessible. An MLP or transformer can instead learn more flexible relationships.
- **When it can be used:** Assessing pretrained representations with a simple downstream model before adding complexity.
- **Pitfalls:** Weak linear performance does not prove information is absent. Keep data splits and evaluation comparable. A slide transformer seeing many tiles has different information from a classifier seeing one tile.
- **Tools / methods using it:** SimCLR and BYOL use linear evaluation of pretrained representations; see their reference implementations above.

## DINO
Status: **introduced**; centering versus sharpening needs retrieval practice.

- **What this means:** A student matches a momentum teacher's output distributions across augmented views, without explicit negatives. Centering counteracts dominant output categories; sharpening discourages flat predictions. These learned categories are not supplied tumour labels.
- **When it can be used:** Pretraining image encoders on unlabelled images for downstream grouping or prediction, such as learning histology tile embeddings.
- **Pitfalls:** Confident predictions can still collapse. Noncollapsed embeddings may encode technical variation. Test biological usefulness with relevant labels, linear probes and suitable held-out data. Labels, biological pairings and augmentation choices can guide learning toward biology; avoiding collapse alone cannot.
- **Tools / methods using it:** [Original DINO](https://github.com/facebookresearch/dino); [DINOv2](https://github.com/facebookresearch/dinov2) builds on this approach with additional objectives and training changes.

Source: [Original DINO paper](https://arxiv.org/abs/2104.14294), especially Sections 3.1 and 5.3. DINOv2's differences have not yet been studied in our sessions.

## Masked autoencoders (MAE)
Session: 2026-11-04. Status: **introduced; can explain the core intuition**.

- **What this means:** Hide random image patches and train an encoder–decoder to reconstruct their pixels. The encoder processes only visible patches with positional information; the decoder receives their representations and placeholders for missing positions. Reconstruction loss is measured on hidden patches. Afterwards, use the encoder for downstream tasks and usually discard the decoder.
- **When it can be used:** Pretraining image encoders without manual labels, including histology tile encoders. Missing content is predicted from visible context; original pixels supply the training targets.
- **Pitfalls:** Random masking does not select the strongest signals. Too little masking permits local shortcuts; too much makes reconstruction ambiguous. Squared pixel error can favour averaging plausible completions, producing blur. Good reconstruction does not guarantee useful biological embeddings. Decoder capacity can affect what the encoder learns; knowledge in decoder weights is different from information accessible in an individual encoder embedding.
- **Tools / methods using it:** [Original MAE](https://arxiv.org/abs/2111.06377); [PLUTO](https://arxiv.org/abs/2405.07905) combines MAE image reconstruction with DINO/iBOT and Fourier losses; [Prov-GigaPath](https://www.nature.com/articles/s41586-024-07441-w) uses masked autoencoding for its slide encoder over tile representations, while its tile encoder uses DINOv2; [scFoundation](https://www.nature.com/articles/s41592-024-02305-7), based on [xTrimoGene](https://arxiv.org/abs/2311.15156), adapts asymmetric masked reconstruction to gene-expression values.

These examples reconstruct different targets: image pixels, tile representations or expression values. Standard image MAE does not automatically encode an entire whole slide. Model examples were identified, not studied in detail.

**Retrieval question:** Why can hiding most patches encourage broader contextual learning, and why can excessive masking make reconstruction ambiguous?

**Resume:** Compare reconstructing pixels with predicting learned representations, connecting MAE to iBOT. Decoder capacity versus downstream embedding usefulness remains a hypothesis to test, not a rule that smaller decoders are always better.
