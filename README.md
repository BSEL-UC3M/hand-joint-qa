<div align="center">

<img src="docs/assets/pipeline_overview.jpg" alt="Automated joint crop extraction pipeline on a bilateral hand radiograph" width="100%">

<br>

# hand-joint-qa

**From hand radiographs to standardized joint crops: a modular, automated pipeline with a local quality assurance interface.**

![Status](https://img.shields.io/badge/code%20and%20weights-available%20upon%20acceptance-538AE5)
![Runs locally](https://img.shields.io/badge/interface-runs%20100%25%20locally-3B6D11)
![Modality](https://img.shields.io/badge/modality-hand%20radiographs-534AB7)

[Overview](#overview) ·
[What is behind the figure](#what-is-behind-the-figure) ·
[Quality assurance interface](#quality-assurance-interface) ·
[Results](#results) ·
[Availability](#availability) ·
[Citation](#citation)

</div>

---

## Overview

Hand osteoarthritis assessment starts with locating each joint on the
radiograph. Radiographs differ in layout, orientation, number of hands and
radiographic markers, so this step is often repeated by hand and can take
several minutes per image.

**hand-joint-qa** is a modular five-stage pipeline that converts a raw hand
radiograph into standardized, aligned **224 x 224 joint crops** of the 12 DIP,
PIP and MCP joints of digits 2 to 5. It does not need prior knowledge of the
input: it handles unilateral and bilateral radiographs, with or without
laterality markers, and adapts each crop to the local bone anatomy.

A **local quality assurance (QA) interface** lets a reviewer inspect and correct
the output of every stage, and each correction regenerates all downstream
outputs.

<table>
<tr>
<td width="25%" valign="top"><b>Any layout</b><br>Unilateral and bilateral radiographs, with or without markers.</td>
<td width="25%" valign="top"><b>Standardized crops</b><br>12 joints per hand, rotated along the finger axis and resized to 224 x 224.</td>
<td width="25%" valign="top"><b>Bone-aware framing</b><br>The crop limits follow the bone margins predicted for each joint.</td>
<td width="25%" valign="top"><b>Private by design</b><br>The interface runs on your computer. Nothing is uploaded.</td>
</tr>
</table>

---

## What is behind the figure

The figure at the top follows one bilateral radiograph through the pipeline.

| # | Stage | What it does |
|---|---|---|
| 1 | **Marker detection** | Finds the radiographic markers and classifies each as left or right. |
| 2 | **Hand detection** | Finds each hand and classifies it by thumb side (thumb-left or thumb-right). |
| 3 | **Marker-to-hand assignment** | Gives each hand its anatomical side from the nearest marker. |
| 4 | **Splitting and orientation** | Splits bilateral radiographs into single hands and mirrors them so every hand has the thumb on the right. |
| 5 | **19-keypoint localization** | Predicts 19 joint centers per hand: 4 DIP, 4 PIP, the thumb IP, 5 MCP and 5 CMC. |
| 6 | **Joint alignment** | Rotates each of the 12 target joints so that its finger axis is vertical. |
| 7 | **Bone-boundary regression** | Predicts the left and right bone margins at each joint (solid lines in the figure). |
| 8 | **Final joint crop** | Builds a square crop centered on the joint, framed by the margins plus 3 mm (dashed lines), and resizes it to 224 x 224. |

**How laterality is decided.** The thumb side cannot tell left from right on its
own, because that also depends on the projection and on whether the image was
mirrored. The side is therefore taken from the nearest marker. With a single
marker in a bilateral radiograph, the other hand receives the opposite side.
Without markers, the thumb side is used under the posteroanterior convention and
the radiograph is flagged for review.

**How a crop is framed.** The half-side of each crop is the distance from the
joint center to the farther predicted bone margin, plus 3 mm. Without pixel
spacing, 0.1 mm per pixel is assumed.

---

## Quality assurance interface

The interface is a local web application. It walks a reviewer through the
pipeline one stage at a time, showing the model prediction on the image and the
controls to approve or correct it.

- **Stage-by-stage review.** Markers, hands, joints, alignment and boundaries,
  each with a short explanation of what to check.
- **Correction of every output.** Boxes and classes, any of the 19 keypoints,
  the rotation of each joint and the bone margins can be edited.
- **Changes propagate downstream.** A correction at one stage regenerates the
  outputs of all later stages.
- **Review records.** Predictions and corrections are saved per image, and the
  joint crops can be downloaded.
- **Runs on CPU.** No GPU is required.
- **Local and private.** Images stay on the computer where the interface runs.

---

## Results

Internal evaluation uses a participant-level test set of the Osteoarthritis
Initiative (OAI). External evaluation applies the OAI-trained models without
retraining to 895 radiographs of the USC Digital Hand Atlas (DHA).

| Stage | Metric | OAI test |
|---|---|---|
| Marker detection | Macro-F1 | 0.960 |
| Hand detection | Macro-F1 | 0.999 |
| Keypoint localization | Mean radial error, 19 landmarks | 0.384 mm |
| Bone-boundary regression | Mean absolute error | 0.073 mm (0.55 % of bone width) |

| External evaluation on DHA (895 radiographs) | |
|---|---|
| Keypoint error, 19 landmarks | 1.583 mm |
| Keypoint error, subjects aged 17 to 18 years | 1.068 mm |
| Visual review of the full pipeline output | 761 radiographs (85.0 %) with no flagged issue |
| CPU inference, full pipeline | 1.027 +/- 0.160 s per image |

<sub>Timing measured on an Apple M4 with 16 GB of RAM, including loading, preprocessing, all stages and crop saving. See the paper for the full protocol.</sub>

---

## Availability

> **The interface, the code and the model weights will be made available in this
> repository upon acceptance of the paper.**

This repository currently contains only this description.

---

## Citation

The accompanying paper is under review. A citation will be added here upon
acceptance.

## Acknowledgments

Universidad Carlos III de Madrid, Instituto de Investigación Sanitaria Gregorio
Marañón, UMass Chan Medical School and Brigham and Women's Hospital.
Research supported by project PID2023-149604OB-I00 funded by
MICIU/AEI/10.13039/501100011033 and by ERDF, EU.
