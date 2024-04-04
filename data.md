---
title: Data Set
layout: home
nav_order: 3
---

# The Data set

The data in this challenge is acquired from both left and right forearms of 100 volunteers, acquired at University College London, London, U.K, with a racial-, gender-, age-diverse subject cohort. No specific exclusion criteria as long as the participants do not have allergies or skin conditions which may be exacerbated by US gel. All scanned forearms are in good health. 

## Images

The US images were acquired on an Ultrasonix machine (BK, Europe) with a curvilinear probe (4DC7-3/40). The acquired US frames were recorded at 20 fps, with an image size of 480×640, without speckle reduction. The frequency was set at 6MHz with a dynamic range of 83 dB, an overall gain of 48% and a depth of 9 cm. For each forearm, the US probe moves in three different trajectories (straight line shape, "C" shape, and "S" shape), in a distal-to-proximal direction followed by a proximal-to-distal direction, with the US plane perpendicular of and parallel to the scanning direction. The dataset contains 1200 scans in total, 12 scans associated with each subject.

## Labels / Transformations

The position information recorded by the optical tracker (NDI Polaris Vicra, Northern Digital Inc., Canada) will be provided along with the images, which indicates the position of the US probe for each frame in the camera coordinate system, described as homogeneous transformation matrix. A calibration matrix will also be provided, denoting the transformation between US image coordinate system and US probe coordinate system while these data were acquired.

## Data set structure 

TBA

The data is randomly split into training, validation, and test sets of 60, 8, and 32 subjects (720, 96, 384 scans), respectively. The data can be found [here](TBD).