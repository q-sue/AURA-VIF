<div align="center">

<img src="assets/brand/aura-vif-logo.png" alt="AURA-VIF dataset logo" width="720" />

# AURA-VIF

### Low-Altitude UAV Infrared-Visible Video Fusion

<p>
  <a href="#dataset"><img src="https://img.shields.io/badge/71%20sequences-1d4ed8?style=flat-square" alt="71 sequences" /></a>
  <a href="#dataset"><img src="https://img.shields.io/badge/28%2C205%20frame%20pairs-0f766e?style=flat-square" alt="28,205 frame pairs" /></a>
  <a href="#mastfusion"><img src="https://img.shields.io/badge/MASTFusion-c2410c?style=flat-square" alt="MASTFusion" /></a>
</p>

<p>
  <a href="#video-demos">Video demos</a> &nbsp;|&nbsp;
  <a href="#overview">Overview</a> &nbsp;|&nbsp;
  <a href="#dataset">Dataset</a> &nbsp;|&nbsp;
  <a href="#mastfusion">MASTFusion</a>
</p>

</div>

## Video demos

These clips visualize synchronized infrared-visible frames by overlaying the two registered streams. They are registration visualizations, not fusion-algorithm outputs.

### Demo 1

https://github.com/user-attachments/assets/79e1dfef-b6e9-4ec8-86d1-fbd55783948a

### Demo 3

https://github.com/user-attachments/assets/4817d2c8-c885-4328-8ce6-bf1445f1cb84

## Overview

Low-altitude UAV sensing brings together platform motion, changing viewpoints and target scales, dynamic objects, occlusion, and difficult illumination. **AURA-VIF** keeps these effects in temporally continuous infrared-visible video rather than reducing the data to independent image pairs.

The benchmark is accompanied by **MASTFusion**, a motion-aligned spatial-temporal fusion network. Neighboring observations are aligned toward a focus frame, aggregated within each modality, and fused only during reconstruction.

<div align="center">
<table>
  <tr>
    <td align="center"><strong>71</strong><br /><sub>continuous sequences</sub></td>
    <td align="center"><strong>28,205</strong><br /><sub>registered frame pairs</sub></td>
    <td align="center"><strong>9</strong><br /><sub>scene categories</sub></td>
    <td align="center"><strong>22</strong><br /><sub>acquisition locations</sub></td>
  </tr>
</table>
</div>

## Dataset

| Item | Specification |
| --- | --- |
| Platform | DJI Matrice 4T UAV with co-mounted infrared and visible sensors |
| Native streams | Infrared `1280 x 1024`; visible `3840 x 2160` |
| Registered output | Visible frames resampled to `1280 x 1024` |
| Frame rate | Nominal `30 fps` |
| Flight altitude | Approximately `15-80 m` |
| Collection | Approximately four months, covering daytime and nighttime conditions |
| Synchronization | Mean absolute residual `5.29 ms`; median `4 ms`; 95th percentile `16 ms` |
| Calibration | RMS reprojection error `1.2868 px` (infrared) and `1.2128 px` (visible) |

### Scene coverage

The collection includes roads, campus entrances, playgrounds, crowded public areas, transportation zones, power-distribution facilities, indoor scenes, rain, small targets, and partial occlusion.

<div align="center">
  <img src="assets/figures/updated/aura-vif-collection.png" width="100%" alt="AURA-VIF infrared-visible scene coverage" />
</div>

### Splits

The split is acquisition-disjoint: sequences from the same location, recording session, or UAV flight stay in one subset.

| Split | Sequences | Frame pairs |
| --- | ---: | ---: |
| Training | 49 | 19,694 |
| Validation | 11 | 3,992 |
| Test | 11 | 4,519 |
| **Total** | **71** | **28,205** |

The benchmark reports spatial quality with **MI** and **Qabf**, and temporal consistency with **flowD**, **feaCD**, **BiSWE**, and **MS2R**.

## MASTFusion

<div align="center">
  <img src="assets/figures/updated/mastfusion-architecture.png" width="100%" alt="MASTFusion architecture" />
</div>

| Module | Purpose |
| --- | --- |
| **MDSE** | Modality-specific patch embedding and Bidirectional Spatial Mamba encoding, followed by frozen SEA-RAFT alignment. |
| **WTFA** | Independent infrared and visible aggregation over overlapping three-frame windows with multi-scale convolution and Bi-Mamba refinement. |
| **Fusion decoder** | Delayed cross-modal concatenation, Transformer reconstruction, and fused-frame output. |

During training, a five-frame clip produces three consecutive outputs from overlapping three-frame windows centered at `t-1`, `t`, and `t+1`. This keeps motion alignment, temporal aggregation, and cross-modal reconstruction as separate stages.

