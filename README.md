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


## Interface

<p align="justify">A local web application that runs on your own computer. A reviewer checks one stage at a time and can correct boxes, keypoints, rotation and bone margins. Each correction updates the later stages.</p>


### 1. Markers

<table>
<tr>
<td width="50%"><img src="docs/assets/interface/markers_1.png" alt="1. Markers stage"></td>
<td width="50%"><img src="docs/assets/interface/markers_2.png" alt="1. Markers stage, detail"></td>
</tr>
</table>

### 2. Hands

<table>
<tr>
<td width="50%"><img src="docs/assets/interface/hands_1.png" alt="2. Hands stage"></td>
<td width="50%"><img src="docs/assets/interface/hands_2.png" alt="2. Hands stage, detail"></td>
</tr>
</table>

### 3. Joints

<table>
<tr>
<td width="50%"><img src="docs/assets/interface/joints_1.png" alt="3. Joints stage"></td>
<td width="50%"><img src="docs/assets/interface/joints_2.png" alt="3. Joints stage, detail"></td>
</tr>
</table>

### 4. Alignment

<table>
<tr>
<td width="50%"><img src="docs/assets/interface/alignment_1.png" alt="4. Alignment stage"></td>
<td width="50%"><img src="docs/assets/interface/alignment_2.png" alt="4. Alignment stage, detail"></td>
</tr>
</table>

### 5. Boundaries

<table>
<tr>
<td width="50%"><img src="docs/assets/interface/boundaries_1.png" alt="5. Boundaries stage"></td>
<td width="50%"><img src="docs/assets/interface/boundaries_2.png" alt="5. Boundaries stage, detail"></td>
</tr>
</table>

### 6. Download

<p align="center">
<img src="docs/assets/interface/download.png" alt="Download the final joint crops" width="60%">
</p>
