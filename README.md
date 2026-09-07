<div align="center">

<img src="assets/brand/aura-vif-logo.png" alt="AURA-VIF dataset logo" width="100%" />

# AURA-VIF

### Low-Altitude UAV Infrared-Visible Video Fusion

<p>
  <a href="#dataset"><img src="https://img.shields.io/badge/71%20sequences-1d4ed8?style=flat-square" alt="71 sequences" /></a>
  <a href="#dataset"><img src="https://img.shields.io/badge/28%2C205%20frame%20pairs-0f766e?style=flat-square" alt="28,205 frame pairs" /></a>
  <a href="#mastfusion"><img src="https://img.shields.io/badge/MASTFusion-c2410c?style=flat-square" alt="MASTFusion" /></a>
</p>

<p>
  <a href="#mastfusion">MASTFusion</a> &nbsp;|&nbsp;
  <a href="#video-demos">Video demos</a> &nbsp;|&nbsp;
  <a href="#scene-coverage">Scene coverage</a> &nbsp;|&nbsp;
</p>

</div>

## MASTFusion

<div align="center">
  <img src="assets/figures/updated/mastfusion-architecture.png" width="100%" alt="MASTFusion architecture" />
</div>

| Module | Purpose |
| --- | --- |
| **MDSE** | Modality-specific patch embedding and Bidirectional Spatial Mamba encoding, followed by frozen SEA-RAFT alignment. |
| **WTFA** | Independent infrared and visible aggregation over overlapping three-frame windows with multi-scale convolution and Bi-Mamba refinement. |
| **Fusion decoder** | Delayed cross-modal concatenation, Transformer reconstruction, and fused-frame output. |

During training, a five-frame clip produces three consecutive outputs from overlapping three-frame windows centered at `t-1`, `t`, and `t+1`.

## Video demos

These clips visualize synchronized infrared-visible frames by overlaying the two registered streams. They are registration visualizations, not fusion-algorithm outputs.

### Demo 1

https://github.com/user-attachments/assets/79e1dfef-b6e9-4ec8-86d1-fbd55783948a

### Demo 3

https://github.com/user-attachments/assets/4817d2c8-c885-4328-8ce6-bf1445f1cb84

## Scene coverage

The collection includes roads, campus entrances, playgrounds, crowded public areas, transportation zones, power-distribution facilities, indoor scenes, rain, small targets, and partial occlusion.

<div align="center">
  <img src="assets/figures/updated/aura-vif-collection.png" width="100%" alt="AURA-VIF infrared-visible scene coverage" />
</div>
