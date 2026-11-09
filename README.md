# DEUN-LightShaper

**Stable RGB light fields from dynamically distorted beams.**

Official project repository for **[Color-resolved light field shaping via diffractive-electronic U-shape network with wavelength-aware virtual branching](https://doi.org/10.1016/j.neunet.2025.108502)**.

Yuheng Zong, Huaiping Jin, Hao Fang, Chai Hu, and Jiashuo Shi

**Accepted by Neural Networks on December 15, 2025.** Published online December 22, 2025; *Neural Networks*, **197** (May 2026), 108502.

**The model and dataset have been open-sourced and are available in the supplementary materials accompanying the published paper.**

## Overview

Dynamic distortions in Gaussian beams make it difficult to preserve both color fidelity and frame-to-frame stability. **DEUN** addresses this challenge by combining a three-layer diffractive optical front-end with an electronic U-shape decoder: the optical stage shapes the wavefront, while the electronic stage corrects residual distortions and restores image detail.

**Wavelength-aware virtual branching (WAVB)** guides the shared diffractive structure toward wavelength-specific compensation during training. **Frequency-selective skip connections (FSSC)** guide the decoder toward mid- and high-frequency detail recovery while limiting low-frequency overcompensation. A **diffractive optical flow predictor** models beam evolution between frames to support temporal coherence and predictive correction.

![DEUN framework, wavelength-aware training, and optical-electronic architecture](assets/framework.png)

*Figure 1. Optical wavefront shaping and frequency-selective electronic correction within DEUN.*

## Dataset

To ground the synthetic distortions in measured beam characteristics, we construct a hybrid experimental-synthetic dataset from beam morphology and super-Gaussian parameters extracted from 50 visible-light profiles at 532 nm and 12 terahertz profiles at 40.8 micrometers. Simulated aberrations and noise extend these characteristics into dynamic sequences; the shaping evaluation uses 500 frames at 256 x 256 pixels.

![Construction of the hybrid experimental-synthetic distorted beam dataset](assets/dataset.png)

*Figure 2. Measured beam characteristics guide distorted-beam synthesis.*

## Results

DEUN produces cleaner reconstructions with better color fidelity than the purely diffractive DON-3 and DON-5 baselines. The full model achieves **22.61 dB PSNR** and **0.874 SSIM** at **18.1 ms per frame**, supporting RGB shaping above **50 Hz** in our evaluation.

![Beam-shaping comparison between DON-3, DON-5, DEUN, and target images](assets/results.png)

*Figure 3. DEUN preserves target colors and structure across changing input distortions.*

<ins><strong><em>The demonstration targets use the album covers of <a href="https://baike.baidu.com/item/%E9%BB%91%E8%89%B2%E6%9F%B3%E4%B8%81/2266778">《黑色柳丁》</a> by David Tao (陶喆) and <a href="https://baike.baidu.com/item/%E6%A2%A6%E6%83%B3%E5%AE%B6/65008794">《梦想家》</a> by Khalil Fong (方大同), chosen as a personal tribute to two of my favorite singers.</em></strong></ins>

The ablation results show how wavelength-aware training and frequency-selective reconstruction each contribute to image quality:

| Configuration | PSNR (dB) | SSIM | Latency (ms/frame) |
| :--- | ---: | ---: | ---: |
| Without WAVB | 20.13 | 0.871 | 17.6 |
| Without FSSC | 21.93 | 0.866 | 17.9 |
| **Full DEUN** | **22.61** | **0.874** | **18.1** |

*Ablation values are from Table 1. Timing is averaged over 500 sequential frames on an RTX 5090 workstation. Evaluation combines numerical diffraction with tests using experimentally measured beam inputs.*

## Citation

If you use this work, please cite:

```bibtex
@article{zong2026deun,
  title   = {Color-resolved light field shaping via diffractive-electronic
             {U}-shape network with wavelength-aware virtual branching},
  author  = {Zong, Yuheng and Jin, Huaiping and Fang, Hao and
             Hu, Chai and Shi, Jiashuo},
  journal = {Neural Networks},
  volume  = {197},
  pages   = {108502},
  year    = {2026},
  doi     = {10.1016/j.neunet.2025.108502}
}
```

Figures are reproduced from Figures 1-3 of the paper; panel content is unchanged.
