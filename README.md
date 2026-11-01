<div align="center">

# From Hand Radiographs to Standardized Joint Crops: A Modular and Automated Pipeline with Quality Assurance

</div>

> [!NOTE]
> **Under review.** This repository accompanies a paper submitted to ISBI 2027. The interface, code and model weights will be available for download here upon acceptance.

<div align="center">

<img src="docs/assets/pipeline_overview.png" alt="Automated joint crop extraction pipeline" width="100%">

</div>


## What it does

<p align="justify">A modular pipeline turns a raw hand radiograph into standardized, aligned 224 x 224 crops of the 12 DIP, PIP and MCP joints of digits 2 to 5. It works on unilateral and bilateral radiographs, with or without laterality markers.</p>

## Models

## Interface

<p align="justify">A local web application that runs on your own computer. A reviewer checks one stage at a time and can correct boxes, keypoints, rotation and bone margins. Each correction updates the later stages.</p>
