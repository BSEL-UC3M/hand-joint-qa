<div align="center">

# From Hand Radiographs to Standardized Joint Crops: A Modular and Automated Pipeline with Quality Assurance

</div>

> [!NOTE]
> **Under review.** This repository accompanies a paper submitted to ISBI 2027. The interface, code and model weights will be available for download here upon acceptance.

<div align="center">

<img src="docs/assets/pipeline_overview.png?v=2" alt="Automated joint crop extraction pipeline" width="100%">

</div>


## What it does

<p align="justify">A modular pipeline turns a raw hand radiograph into standardized, aligned 224 x 224 crops of the 12 DIP, PIP and MCP joints of digits 2 to 5. It works on unilateral and bilateral radiographs, with or without laterality markers.</p>


## Interface

<p align="justify">A local web application that runs on your own computer. A reviewer checks one stage at a time and can correct boxes, keypoints, rotation and bone margins. Each correction updates the later stages.</p>

### 1. Markers

<p align="justify">In this stage the model detects laterality X-ray markers (<code>bounding box</code>) and predicts the class of each one (<code>left</code> or <code>right</code>), based on whether it reads R/right or L/left. Check that each box encloses a real marker and that its class matches what is printed on it.</p>

<p align="center"><img src="docs/assets/interface/markers_1.png?v=2" alt="1. Markers stage" width="48%">&nbsp;<img src="docs/assets/interface/markers_2.png?v=2" alt="1. Markers stage, detail" width="48%"></p>

### 2. Hands

<p align="justify">In this stage the model detects hands (<code>bounding box</code>) and predicts the class of each one (<code>left</code> or <code>right</code>), based on which side of the hand the thumb is on. Check that each box encloses a whole hand and that its class matches the side the thumb is on.</p>

<p align="center"><img src="docs/assets/interface/hands_1.png?v=2" alt="2. Hands stage" width="48%">&nbsp;<img src="docs/assets/interface/hands_2.png?v=2" alt="2. Hands stage, detail" width="48%"></p>

### 3. Joints

<p align="justify">In this stage the model detects 19 joint locations (<code>keypoints</code>), one on each joint of the hand: 4 DIP, 4 PIP and 1 thumb IP, 5 MCP and 5 CMC. Check that each keypoint sits on the center of its joint, and correct any that are off by clicking the right location on the full hand image.</p>

<p align="center"><img src="docs/assets/interface/joints_1.png?v=2" alt="3. Joints stage" width="48%">&nbsp;<img src="docs/assets/interface/joints_2.png?v=2" alt="3. Joints stage, detail" width="48%"></p>

### 4. Alignment

<p align="justify">In this stage we align each joint's crop by <code>rotating</code> it using the other joints of the same finger, so the joint sits <code>centered</code> and <code>level</code>. Check that each joint's rotation looks right, correct any that are off using the sliders.</p>

<p align="center"><img src="docs/assets/interface/alignment_1.png?v=2" alt="4. Alignment stage" width="48%">&nbsp;<img src="docs/assets/interface/alignment_2.png?v=2" alt="4. Alignment stage, detail" width="48%"></p>

### 5. Boundaries

<p align="justify">In this stage the model detects the bone boundaries for each joint (<code>solid lines</code>) and adds some padding around them (<code>dashed lines</code>). Check that each joint's predicted boundary fully captures the bone, correct any that look wrong by dragging the left/right boundary sliders.</p>

<p align="center"><img src="docs/assets/interface/boundaries_1.png?v=2" alt="5. Boundaries stage" width="48%">&nbsp;<img src="docs/assets/interface/boundaries_2.png?v=2" alt="5. Boundaries stage, detail" width="48%"></p>

### 6. Download

<p align="justify">Download the final joint crops of the left hand, the right hand or both, then go to the next image or continue to OARSI classification.</p>

<p align="center"><img src="docs/assets/interface/download.png?v=2" alt="6. Download stage" width="60%"></p>
