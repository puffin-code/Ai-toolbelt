# Multimodal AI

Short notes from 2026-11-02. Progress describes demonstrated understanding, not mastery.

## CLIP-style alignment and zero-shot classification
Progress: **can explain**.

- **What this means:** Separate image and text encoders learn a shared embedding space through paired contrastive training. Zero-shot classification compares an image with text descriptions of classes.
- **When it can be used:** Image–text retrieval and classification without fitting a new task-specific classifier.
- **Pitfalls:** Equal embedding dimensions don't imply alignment. Replacing either encoder can break compatibility. Prompt wording matters; "normal" and "nonmalignant" define different classes. Choose prompts on validation data, then evaluate on held-out data.
- **Tools / methods using it:** [CLIP](https://github.com/openai/CLIP) is the foundational example; [OpenCLIP](https://github.com/mlfoundations/open_clip) provides implementations and pretrained models. [CONCH](https://github.com/mahmoodlab/CONCH) is a pathology vision-language model trained using image–caption pairs, supporting tasks involving images and text.

## Matching supervision to spatial scale
Progress: **can apply** to a hypothetical pathology experiment.

- **What this means:** Match the image representation's scale to the text: a slide-level report should supervise a slide-level representation.
- **When it can be used:** Aggregate tile embeddings before aligning slides with reports.
- **Pitfalls:** Pairing every tile with its slide's diagnosis creates misleading supervision. Aggregation helps match scale but doesn't guarantee that every report finding is visible or correctly localized.
- **Tools / methods using it:** MIL or whole-slide encoders combined with a CLIP-style objective. [TITAN](https://github.com/mahmoodlab/TITAN) aligns whole-slide representations with pathology reports, and also uses region–caption alignment. [mSTAR](https://github.com/Innse/mSTAR) incorporates slides, pathology reports and gene expression during pretraining, then transfers multimodal whole-slide knowledge into patch representations.

## Testing shortcuts and alignment failures
Progress: **can apply** to hypothetical experiments.

- **What this means:** Report matching, stain robustness and malignancy prediction test different properties.
- **When it can be used:** Test cases that break centre–diagnosis associations. Compare linear probes before and after image projection, then compare with zero-shot predictions on the same held-out samples, using consistent splits and comparable probe fitting.
- **Pitfalls:** Patient splits can preserve centre confounding. Plausible stain changes test only the variations examined. A weaker probe after projection suggests less linearly accessible signal, not necessarily complete information loss. Strong probes at both stages with weak zero-shot performance suggest that text-derived decision directions aren't accessing available signal effectively; this doesn't isolate the text encoder as the cause.
- **Tools / methods using it:** Linear probes; subgroup evaluation; controlled stain perturbations. CLIP's reference implementation includes zero-shot and linear-probe examples.

CONCH, TITAN and mSTAR are examples identified during this discussion; their detailed mechanisms have not yet been studied.

## References

- [CLIP reference implementation and evaluation examples](https://github.com/openai/CLIP)
- [CONCH: A visual-language foundation model for computational pathology](https://www.nature.com/articles/s41591-024-02856-4)
- [TITAN: Multimodal Whole Slide Foundation Model for Pathology](https://arxiv.org/abs/2411.19666)
- [mSTAR: A multimodal knowledge-enhanced whole-slide pathology foundation model](https://www.nature.com/articles/s41467-025-66220-x)
