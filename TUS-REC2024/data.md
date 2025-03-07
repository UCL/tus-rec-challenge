---
title: Data Set
# layout: home
parent: Past Challenges
nav_order: 4
---

# The Data set

The data in this challenge is acquired from both left and right forearms of 100 volunteers, acquired at University College London, London, U.K, with a racial-, gender-, age-diverse subject cohort. No specific exclusion criteria as long as the participants do not have allergies or skin conditions which may be exacerbated by US gel. All scanned forearms are in good health. The data is randomly split into training, validation, and test sets of 50, 10, and 40 subjects (1200, 240, 960 scans), respectively.

**The train data is split into three parts: [Part 1](https://zenodo.org/doi/10.5281/zenodo.11178508), [Part 2](https://zenodo.org/doi/10.5281/zenodo.11180794), and [Part 3](https://zenodo.org/doi/10.5281/zenodo.11355499).**

## Images

The US images were acquired on an Ultrasonix machine (BK, Europe) with a curvilinear probe (4DC7-3/40). The acquired US frames were recorded at 20 fps, with an image size of 480×640, without speckle reduction. The frequency was set at 6MHz with a dynamic range of 83 dB, an overall gain of 48% and a depth of 9 cm. For each forearm, the US probe moves in three different trajectories (straight line shape, "C" shape, and "S" shape), in a distal-to-proximal direction followed by a proximal-to-distal direction, with the US plane perpendicular of and parallel to the scanning direction. The dataset contains 2400 scans in total, 24 scans associated with each subject.

## Labels / Transformations

The position information recorded by the optical tracker (NDI Polaris Vicra, Northern Digital Inc., Canada) will be provided along with the images, which indicates the position of the US probe for each frame in the camera coordinate system, described as homogeneous transformation matrix. A calibration matrix will also be provided, denoting the transformation between US image coordinate system and US probe coordinate system while these data were acquired.

## Training Data Structure 

* The training data contains 50 folders (one subject per folder), each with 24 scans. Each .h5 file corresponds to one scan, storing image and transformation of each frame within this scan. Key-value pairs in each .h5 file are explained below.

    * `frames`  - All frames in the scan; with a shape of [N,H,W], where N refers to the number of frames in the scan, H and W denote the height and width of a frame. 

    * `tforms` - All transformations in the scan; with a shape of [N,4,4], where N is the number of frames in the scan, and the transformation matrix denotes the transformation from tracker tool space to camera space. 

    * Notations in the name of each .h5 file: “RH”: right arm; “LH”: “left arm”; “Per”: perpendicular; “Par”: parallel; “L”: straight line shape; “C”: C shape; “S”: S shape; “DtP”: distal-to-proximal direction; “PtD”: proximal-to-distal direction; For example, “RH_Ver_L_DtP.h5” denotes a scan on the right forearm, with ultrasound probe perpendicular of the forearm sweeping along straight line, in distal-to-proximal direction.

* Calibration matrix: The calibration matrix was obtained using a pinhead-based method. The `scaling_from_pixel_to_mm` and `spatial_calibration_from_image_coordinate_system_to_tracking_tool_coordinate_system` are provided in the “calib_matrix.csv”. 
