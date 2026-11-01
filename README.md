<div align="center">

# From Hand Radiographs to Standardized Joint Crops: A Modular and Automated Pipeline with Quality Assurance

<img src="docs/assets/pipeline_overview.png" alt="Automated joint crop extraction pipeline" width="100%">

</div>

---

<p align="justify"><b>Under review.</b> This repository accompanies a 4-page short paper submitted to ISBI 2027. The interface, code and model weights will be available for download here upon acceptance.</p>

## What it does

<p align="justify">A modular pipeline turns a raw hand radiograph into standardized, aligned 224 x 224 crops of the 12 DIP, PIP and MCP joints of digits 2 to 5. It works on unilateral and bilateral radiographs, with or without laterality markers.</p>

## Models

| Stage | Model | Output |
|---|---|---|
| Markers | YOLOv8n | Left and right marker boxes |
| Hands | YOLOv8n | Hand boxes with thumb side |
| Keypoints | HRNet-W32 | 19 joint centers per hand |
| Alignment | Geometry | Joints rotated along the finger axis |
| Boundaries | Small CNN | Left and right bone margins per joint |

## Interface

<p align="justify">A local web application that runs on your own computer. A reviewer checks one stage at a time and can correct boxes, keypoints, rotation and bone margins. Each correction updates the later stages.</p>
