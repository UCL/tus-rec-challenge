---
title: Home
layout: default
nav_order: 1
---

<!-- 1. TOC
{:toc} -->

# TUS-REC2025 Challenge

<div align=center>
  <a href="img/TUS-REC2025.pdf" target="_blank"><img style="padding: 10px;" src="img/logo.png" width=200px></a>
</div >

**Trackerless 3D Freehand Ultrasound Reconstruction (TUS-REC2025) Challenge**

Reconstructing 2D Ultrasound (US) images into a 3D volume enables 3D representations of anatomy to be generated which are beneficial to a wide range of downstream tasks such as quantitative biometric measurement, multimodal registration, and 3D visualisation. This application is challenging due to 1) inherent accumulated error - frame-to-frame transformation error will be accumulated through time when reconstructing long sequence of US frames, and 2) a lack of publicly-accessible data with synchronised spatial location, often obtained from tracking devices, for benchmarking the performance and for training learning-based methods. 

TUS-REC2025 presents a different scanning protocol, in addition to the previous TUS-REC2024 non-rotation-based protocols. The new scans include more diverse probe movement such as rotating and tilting at various angles. With 3D reconstruction as the challenge task, TUS-REC2025 aims to 1) benchmark the model performance on the new rotating data, and 2) validate the model generalisation ability among different scan protocols. The outcome of the challenge includes 1) providing in open access the new US dataset with accurate positional information; 2) establishing the first benchmark for 3D US reconstruction for rotating scans, suitable for modern learning-based data-driven approaches.

<!-- In TUS-REC2024 we observed that reconstruction performance is dependent on scan protocol although the variability of protocols within the TUS-REC2024 dataset remained limited. We believe it is thus relevant to investigate a new scan protocol with more diverse probe movement. TUS-REC2025 presents a different scanning protocol, in addition to the previous TUS-REC2024 non-rotation-based protocols. The new scans include more diverse probe movement such as rotating and tilting at various angles. The new data may further improve reconstruction
performance owing to dense sampling of the area-to-be-reconstructed. With 3D
reconstruction as the challenge task, TUS-REC2025 aims to 1) benchmark the model performance on the new rotating data, and 2) validate the model generalisation ability among different scan protocols. The outcome of the challenge includes 1) providing in open access the new US dataset with accurate positional information; 2) establishing the first benchmark for 3D US
reconstruction for rotating scans, suitable for modern learning-based data-driven approaches. -->

## Main resources
* <a href="https://zenodo.org/records/15119085" target="_blank">Full challenge description</a>
* <a href="https://zenodo.org/records/15224704" target="_blank">Training data</a>
* <a href="https://doi.org/10.5281/zenodo.15699958" target="_blank">Validation data</a>
* <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline" target="_blank">Baseline code</a>
* <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/tree/main/submission" target="_blank">Submission/Evaluation code</a>

## Timeline

The TUS-REC2025 Challenge is an open call event, accepting new submissions after conference deadline. The fixed challenge submission timeline below is associated with <a href="https://conferences.miccai.org/2025/en/" target="_blank">MICCAI 2025</a>. All times are 23:59 BST.

| Date                          | Challenge Milestone                              |
| :-----------------------------| :----------------------------------------------- |
| Apr. 01, 2025                   | Challenge Websites Opening/Registration Opens                               |
| Apr. 28, 2025                   | Training Data/Baseline Code Release                            |
| Jun. 23, 2025                  | Validation Data/Submission Code Release                          |
| Jul. 07, 2025                  | Submission Starts                               |
| Aug. 18, 2025                  | Submission Closes                               |
|  Sep. 01, 2025                 | Winners Announcement                               |
|  Sep. 23, 2025                 | TUS-REC2025 Challenge Events at MICCAI 2025     |

The Challenge will take place on Sep. 27, 2025 during the <a href="https://miccai-ultrasound.github.io/#/asmus25" target="_blank">ASMUS Workshop</a>. (Details for location, presentation, and event format: TBC.)

## The Task

This challenge aims to estimate the transformations among US frames, such that the entire US scan can be reconstructed in 3D space, both for establishing one of the first benchmarks for 3D US reconstruction on the introduced new scan protocol and paving the way from experimental volunteer studies to potential clinical applications for this challenging task.

For detailed information, please refer to [task description](task.html), [dataset](data.html), [assessment](assessment.html), and [submission process](submission.html).

## Awards

The results from all participants will be made publicly available on leaderboard unless the submitted dockers incurred errors during the evaluation process. Teams are allowed to make multiple distinct submissions (but must ensure they are not merely simple variations in hyperparameter values). The leaderboard will be accessible for public viewing [here](leaderboard.html).

- The first-place and runner-up achievers will receive additional certificates.
- Participants who successfully participated the challenge will be awarded certificates of participation.

## Organizers

[Qi Li](mailto:qi.li.21@ucl.ac.uk), University College London

Yuliang Huang, University College London

Shaheer U. Saeed, University College London

Dean C. Barratt, University College London

Matthew J. Clarkson, University College London

Tom Vercauteren, King's College London

Yipeng Hu, University College London

<!-- Challenge Contact E-Mail: [`qi.li.21@ucl.ac.uk`](mailto:qi.li.21@ucl.ac.uk) -->

## Sponsors

<div >
  <a href="http://ucl.ac.uk/hawkes-institute/" target="_blank"><img style="padding: 10px;" src="img/UCL-Hawkes-Institute-BLACK.jpg" width=140px></a>
  <a href="https://conferences.miccai.org/2025/en/" target="_blank"><img style="padding: 10px;" src="img/miccai2025-logo.png" width=130px></a>
  <a href="https://miccai-ultrasound.github.io/#/asmus25" target="_blank"><img style="padding: 10px;" src="img/asmus.png" width=115px></a>
  <a href="https://miccai.org/index.php/special-interest-groups/sig/" target="_blank"><img style="padding: 10px;" src="img/SIGMUS.png" width=220px></a>
</div>