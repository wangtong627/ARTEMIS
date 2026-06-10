<div align="center">

# ARTEMIS

### Agent-guided Reliability-aware Temporal Mask Evolution for Imperfectly Supervised Video Polyp Segmentation

Tong Wang<sup>1,2</sup>, Siwen Wang<sup>2</sup>, Yaolei Qi<sup>1</sup>, Jinxing Zhou<sup>2</sup>, Guanyu Yang<sup>1</sup>, Yutong Xie<sup>2</sup>

<sup>1</sup> Southeast University, China  
<sup>2</sup> Mohamed bin Zayed University of Artificial Intelligence, UAE

Guanyu Yang and Yutong Xie are corresponding authors.

<p>
  <a href="#"><img src="https://img.shields.io/badge/Paper-Submission_Stage-lightgrey" alt="Paper"></a>
  <a href="#code-and-resources"><img src="https://img.shields.io/badge/Code-Coming_Soon-blue" alt="Code"></a>
  <a href="#citation"><img src="https://img.shields.io/badge/BibTeX-Available-green" alt="BibTeX"></a>
  <a href="#"><img src="https://img.shields.io/badge/Task-Video_Polyp_Segmentation-purple" alt="Task"></a>
</p>

</div>

## News

- **[2026/06]** ARTEMIS repository page is initialized for the submission-stage manuscript.
- **[2026/06]** Code, checkpoints, and prediction maps will be released after acceptance.

## Abstract

Imperfectly supervised video polyp segmentation (VPS) aims to learn dense and temporally consistent masks from inexpensive supervision, including weak annotations such as points and scribbles, as well as semi-supervision with only a small subset of densely labeled frames. Although SAM2 can convert sparse or partial annotations into dense masks, direct pseudo labeling remains limited by geometry-degraded masks, underused temporal propagation, and reliability-blind supervision.

We propose **ARTEMIS**, a unified framework for imperfectly supervised VPS driven by **agent-guided reliability-aware temporal mask evolution**. ARTEMIS first initializes coarse masks from available supervision, then uses a debate-and-judge vision-language agent to select reliable temporal anchors under weak supervision. These anchors are propagated bidirectionally with SAM2 to refine unreliable or unlabeled frames. Finally, ARTEMIS trains the segmenter with temporal reliability-aware robust learning, including reliability-guided reference selection, a Reference Prototype Transport Module, and reliability-aware robust loss. Experiments on SUN-SEG and CVC-ClinicDB-612 under scribble, point, and limited-label settings demonstrate state-of-the-art performance.

## Highlights

- **Unified imperfect supervision.** ARTEMIS handles weakly supervised and semi-supervised VPS in one complete-then-learn framework.
- **Agent-guided anchor selection.** A debate-and-judge vision-language agent identifies reliable temporal anchors from noisy SAM2-generated masks.
- **Bidirectional temporal mask evolution.** Reliable anchors are propagated forward and backward with SAM2 to complete sparse or missing annotations.
- **Reliability-aware robust learning.** Reliability-guided reference selection, RPTM, and robust loss suppress residual pseudo-label noise while preserving difficult samples.

## Framework Overview

<p align="center">
  <img src="figure/figure_introduction_2.png" alt="ARTEMIS paradigm" width="92%">
</p>

ARTEMIS follows a two-stage pipeline.

- **Stage 1: Agent-guided bidirectional mask evolution.** Available point, scribble, or sparse dense labels are converted into temporally consistent pseudo masks through reliable anchor selection and SAM2-based propagation.
- **Stage 2: Temporal reliability-aware robust learning.** The final segmenter is trained with reliability-guided reference selection, reference prototype transport, and reliability-aware robust supervision.

<p align="center">
  <img src="figure/figure_method_stage_1.png" alt="Stage 1: Agent-guided bidirectional mask evolution" width="96%">
</p>

<p align="center"><em>Stage 1: Reliable temporal anchors are selected and propagated bidirectionally to evolve pseudo masks.</em></p>

<p align="center">
  <img src="figure/figure_method_stage_2.png" alt="Stage 2: Temporal reliability-aware robust learning" width="96%">
</p>

<p align="center"><em>Stage 2: Reliable reference identity is transported across frames and noisy supervision is down-weighted.</em></p>

## Main Results

We evaluate ARTEMIS on **SUN-SEG** and **CVC-ClinicDB-612** under weakly supervised and semi-supervised settings. The table below reports representative Dice scores. Full quantitative comparisons and ablation studies are provided in the paper.

### SUN-SEG Dice Results

| Supervision Setting | Easy-Seen | Easy-Unseen | Hard-Seen | Hard-Unseen |
| :--- | ---: | ---: | ---: | ---: |
| Scribble supervision | **85.2** | **66.7** | **78.8** | **68.7** |
| Point supervision | **81.2** | **62.8** | **74.8** | **64.4** |
| 1/8 labeled training data | **86.5** | **68.2** | **80.0** | **70.9** |
| 1/16 labeled training data | **85.5** | **66.9** | **79.1** | **68.2** |

<small>All values are Dice scores in percentage (%). Higher is better.</small>

### CVC-ClinicDB-612 Results

| Supervision Setting | S_alpha | E_phi | F_beta | Dice | IoU | MAE |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| Scribble supervision | **91.7** | **94.8** | **86.5** | **88.7** | **80.2** | **1.1** |
| Point supervision | **88.7** | **90.7** | **79.4** | **83.1** | **72.3** | **1.7** |
| 1/8 labeled training data | **92.8** | **95.2** | **88.2** | **89.6** | **81.7** | **0.8** |
| 1/16 labeled training data | **90.9** | **92.9** | **85.2** | **84.8** | **76.1** | **1.2** |

<small>All values are percentages (%). Higher is better except MAE.</small>

## Qualitative Results

<p align="center">
  <img src="figure/figure_qualitative_compairson_scribble.png" alt="Qualitative comparison under scribble supervision" width="96%">
</p>

<p align="center"><em>Qualitative comparison under scribble supervision. ARTEMIS better preserves blurry, drifting, and small polyp regions.</em></p>

<p align="center">
  <img src="figure/figure_qualitative_compairson_semi.png" alt="Qualitative comparison under semi-supervision" width="96%">
</p>

<p align="center"><em>Qualitative comparison under the 1/8 labeled training data setting. ARTEMIS reduces over-segmentation and under-segmentation for background-like polyps.</em></p>

## Code and Resources

This repository is currently maintained for the submission-stage manuscript. Source code, training and testing scripts, checkpoints, and prediction maps are not released during peer review.

The full code and additional resources will be made available after acceptance.

## Citation

If you find ARTEMIS useful, please consider citing our work. The BibTeX entry will be updated with the official venue or preprint information when it becomes available.

```bibtex
@article{wang2026artemis,
  title={ARTEMIS: Agent-guided Reliability-aware Temporal Mask Evolution for Imperfectly Supervised Video Polyp Segmentation},
  author={Wang, Tong and Wang, Siwen and Qi, Yaolei and Zhou, Jinxing and Yang, Guanyu and Xie, Yutong},
  journal={Under review},
  year={2026}
}
```

## Acknowledgement

Tong Wang, Yaolei Qi, and Guanyu Yang are supported by the National Natural Science Foundation of China (T2541064, 82441021) and the Jiangsu Province Cutting-edge Technology R&D Program (BF2025628). This work is also supported by the Big Data Computing Center of Southeast University.

## Contact

For questions about the paper or future code release, please contact [tongwangnj@qq.com](mailto:tongwangnj@qq.com).
