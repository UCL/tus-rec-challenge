---
title: Task Description
layout: home
nav_order: 2
---

# Task Description

The aim of this task is to reconstruct 2D Ultrasound (US) images into a 3D volume.
The algorithm is expected to take the entire scan as input and output two different sets of
transformation-representing displacement vectors as results, a set of displacement vectors on individual pixels and a set of displacement vectors on provided landmarks. There is no requirement on how the algorithm is designed internally, for example, whether it is learning-based method; frame-, sequence- or scan-based processing; or, rigid-, affine- or nonrigid transformation assumptions. Details are explained further in [assessment](assessment.html).

Participant teams are expected to make use of the sequential data and potentially make knowledge transfer from other domains such as computer vision and computer-assisted intervention. The participant teams are expected to take US scan as input and output two sets of pixel displacement vectors, indicating the transformation to reference frame, i.e., first frame in this task. The evaluation process will take the generated displacement vectors from their dockerized models, and produce the final accuracy score to represent the reconstruction performance, at local and global levels, representing different clinical application of the reconstruction methods.

We will provide two baseline algorithms adapted from [Prevost et al. 2018](https://doi.org/10.1016/j.media.2018.06.003) and [Li et al. 2023](https://doi.org/10.1109/TBME.2023.3325551) on the Leaderboard.

