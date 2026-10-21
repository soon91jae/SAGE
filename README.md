<div align="center">

# SAGE
### Sense-Aligned Multimodal Grounding Evaluation with Gloss-Augmented Reasoning

**Beyond image–text matching: does a model actually ground the intended word sense?**

[![Status](https://img.shields.io/badge/status-research%20preview-6366f1)](https://github.com/soon91jae/SAGE)
[![Code](https://img.shields.io/badge/code-coming%20soon-64748b)](#release-status)
[![Data](https://img.shields.io/badge/data-coming%20soon-64748b)](#release-status)

</div>

> **Research preview.** This README describes the SAGE benchmark and the Gloss-Augmented Reasoning (GAR) framework based on the October 2026 manuscript. **Code, processed benchmark data, and evaluation scripts are not yet available in this repository.**

## Why SAGE?

High image–text similarity does not necessarily mean a model recognizes the *intended sense* of an ambiguous expression. In SAGE, image choice must distinguish subtle meanings of **nouns**, **verbs**, and **named entities** even when alternative candidates look semantically plausible.

SAGE unifies three established datasets under a **10-candidate image-selection** setting with one correct candidate:

| Setting | Source dataset | Grounding target | Test examples |
|:--|:--|:--|--:|
| Noun senses | **VWSD** | Contextual word sense | 463 |
| Verb senses | **VerSe** | OntoNotes verb sense | 1,264 |
| Named entities | **WikiDiverse** | Contextual entity referent | 1,243 |

*Numbers correspond to Table 1 of the October 2026 manuscript.*

### 1. Beyond the original image–caption pairing: SPIS

In VerSe, the original correct image may share many unrelated cues with its caption. **Sense-Preserving Image Swap (SPIS)** substitutes another image labeled with the **same verb sense**, while allowing objects, participants, and scene context to change. **Target-verb neutralization (NEU)** then tests how much image selection depends on the verb itself.

| Diagnostic | Gold image | Target verb |
|:--|:--|:--|
| Original | Original caption-paired image | Preserved |
| Original + NEU | Original caption-paired image | Neutralized |
| SPIS | Different image with the same annotated verb sense | Preserved |
| SPIS + NEU | Swapped image | Neutralized |

In the reported diagnostic, three models clustered around **91–92 Hits@1** in the original paired setting, but diverged to **43.7–74.3 Hits@1** after SPIS. Neutralizing the verb in SPIS produced drops of **3.4–33.0 points**, revealing different dependencies on the target verb.

## GAR: Gloss-Augmented Reasoning

### 2. Gloss-Augmented Reasoning (GAR)

GAR examines **which linguistic evidence helps distinguish visually confusable candidates**. It uses external lexical glosses to synthesize and expand an intended-sense definition, then tests that definition in two ways:

- **Definition-based ranking:** Score candidate images using an expanded, sense-specific description.
- **Constraint-Guided Reasoning (CGR):** Break a definition into **object**, **attribute**, and **state** evidence; ask visual verification questions and aggregate their scores.

The manuscript reports that lexical-resource-grounded definition augmentation is beneficial across all three settings, while CGR's benefits vary: stronger on VWSD and VerSe, but less reliable for fine-grained entity distinctions in WikiDiverse.

## Main findings

- **Performance does not transfer uniformly between grounding settings.** Model ranking agreement across dataset pairs is only partial (Kendall's τb **0.46–0.74**).
- **Original image–caption pairs can mask verb-insensitive behavior.** SPIS and NEU expose differences that ordinary paired-image evaluation can conceal.
- **Explicit lexical evidence matters.** Grounded definitions help image ranking, but constraints must be discriminative among the *actual alternatives* rather than merely plausible.

## Paper figures

The October 2026 manuscript includes:

- **Figure 1:** Original task formulations of VWSD, VerSe, and WikiDiverse.
- **Figure 2:** The sense-preserving image swap diagnostic.
- **Figure 3:** GAR's definition synthesis, expansion, semantic decomposition, and visual verification.

**Figures 1–3 from the manuscript are not yet hosted in this repository.** Previous placeholder graphics were removed. The actual manuscript figures will be added after extraction and verification; we do not substitute generated illustrations for original results.

## Release status

| Resource | Status |
|:--|:--|
| Research overview | Available |
| Original manuscript figures | Prepared for upload; not yet hosted |
| Benchmark construction and splits | Planned |
| SPIS / NEU diagnostic code | Planned |
| GAR / CGR inference pipeline | Planned |
| Evaluation and reproducibility scripts | Planned |
| Data access / licenses | To be documented |

We intend to make the research code and shareable data available here. Third-party source datasets and images may remain subject to their original terms; release will respect those restrictions.

## Citation

A BibTeX entry will be added after public bibliographic details are finalized.

## Questions

Please use [GitHub Issues](https://github.com/soon91jae/SAGE/issues) for questions or release-related requests.
