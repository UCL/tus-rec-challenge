---
title: Assessment
layout: default
nav_order: 5
---

# Assessment Criteria

## Metrics

For each scan, the submitted method is tasked to output two types of transformation-representing displacement vectors (hereinafter is also referred to as the prediction), at global and local levels.
- The "global displacement vectors" will be used to reconstruct individual frames (without the first frame), with respect to the first frame in the scan as the "global reference frame".
- The "local displacement vectors" will be used to reconstruct individual frames (without the first frame), with respect to the immediately previous frame in the scan as the "local reference frame".

For each scan, the performance of a submitted method will be evaluated using two reconstruction errors, "landmark reconstruction error" and "pixel reconstruction error".
- The "landmark reconstruction error" is defined as average Euclidean distance, between the
ground-truth-reconstructed frame and the prediction-reconstructed frame, averaged over a set of predefined anatomical landmarks in each scan.
- The "pixel reconstruction error" is defined as the same average Euclidean distance, between the
ground-truth-reconstructed frame and the prediction-reconstructed frame, averaged over all pixels of all but the first frames in each scan.

Thus, each submitted method should output four sets of displacement vectors:
- Global displacement vectors for pixel reconstruction (number of the "GP" vectors = number of pixels in the entire scan, without the first frame)
- Global displacement vectors for landmark reconstruction (number of the "GL" vectors = number of defined landmarks in the scan)
- Local displacement vectors for pixel reconstruction (number of the "LP" vectors = number of pixels in the entire scan, without the first frame)
- Local displacement vectors for landmark reconstruction (number of the "LL" vectors = number of defined landmarks in the scan)

Based on these four output vector sets, four evaluation metrics will be used in this challenge:
- Global pixel reconstruction error (GPE), the pixel reconstruction error using GP vectors.
- Global landmark reconstruction error (GLE), the landmark reconstruction error using GL vectors.
- Local pixel reconstruction error (LPE), the pixel reconstruction error using LP vectors.
- Local landmark reconstruction error (LLE), the landmark reconstruction error using LL vectors.
 
> **_NOTE:_** Runtime will be considered as additional evaluation metric which is the consumed time of predicting positions for all frames in a scan, averaged over all scans in the test set.

## Rationale in using these metrics

**Rationale in using Euclidean distance-based error metrics, as opposed to errors defined in transformation parameter space**

Direct measuring the accuracy of parameters of transformation matrix is difficult since the
contribution and weighting between rotation and translation components can be sensitive to experimental and imaging configurations, such as reference coordinates and definition of rotation axis, and dependent on application. In this challenge, metrics based on distance error is preferred, which is arguably considered a more practical type of measure to reflect the difference between ground truth and prediction in Euclidean space (<a href="https://doi.org/10.1016/j.media.2023.102810" target="_blank">Luo et al. 2023</a>).

**Justification of using displacement-based representation of transformation, as opposed to rigid- or affine matrices, as the algorithm output**

Although the ground-truth are available in the form of rigid transformation, we
argue that, from experience in developing similar numerical algorithms, enforcing the algorithm output to be homogeneous transformation is not only unnecessary, but sometimes misleadingly encourages a more
numerically challenging solution due to issues such as gimbal lock in using rotation matrix, local minima in numerical optimisation. In addition, the displacement-based representation allows flexibility for a quantitatively more accurate reconstruction <a href="https://link.springer.com/chapter/10.1007/978-3-031-72083-3_64" target="_blank">Li et al. 2024</a>, with a near-rigid transformation, which could be sufficient for clinical use. However, there is no requirement in the internal methodology adopted, for example, the submitted algorithm can convert a single estimated rigid transformation matrix to all these four types of required displacement vectors as output.

**Justification of the local and global reconstruction errors**

The reconstructed scan from either local level or global level displacement are capable of representing different types of reconstruction performance, such as frame-level reconstruction error and accumulated error of the algorithm (<a href="https://doi.org/10.1109/TBME.2023.3325551" target="_blank">Li. et al. 2023</a>, <a href="https://link.springer.com/chapter/10.1007/978-3-030-59716-0_49" target="_blank">Wein et al. 2020</a>). To streamline the evaluation, other monotonic metrics, such as final drift and Dice overlap, albeit commonly reported in literature (e.g. <a href="https://doi.org/10.1109/TBME.2023.3325551" target="_blank">Li et al 2023</a>), are not included. However, in practical applications, one might choose to reconstruct a sequence of ultrasound frames (as opposed to the entire scan or two adjacent frames, which are represented by local and global errors, respectively), using a pre-optimised sequence length that is most suitable to the downstream application. Without specifying a single target clinical application, these two adopted local and global errors shall represent the range of accuracy between the choices of the reconstruction length.



## Ranking method

For each test scan, the four evaluation metrics will be normalised to the range [0, 1] based on the "smallest reconstruction error" and "largest reconstruction error", respectively, using formulas below. The "smallest reconstruction error" is defined as the reconstruction error using the ground truth transformations, which is 0. The "largest reconstruction error" is the reconstruction error using transformations of identity matrix for all frames in a scan.

GPE<sup>* </sup> = (GPE – largest_GPE) / (smallest_GPE - largest_GPE)
GLE<sup>* </sup> = (GLE – largest_GLE) / (smallest_GLE - largest_GLE)
LPE<sup>* </sup> = (LPE – largest_LPE) / (smallest_LPE - largest_LPE)
LLE<sup>* </sup> = (LLE – largest_LLE) / (smallest_LLE - largest_LLE)

where <sup>* </sup> indicates the normalised reconstruction errors. smallest_GPE, smallest_GLE, smallest_LPE, and smallest_LLE denote the smallest reconstruction errors for each evaluation metric, and largest_GPE, largest_GLE, largest_LPE, and largest_LLE denote the largest reconstruction error for each evaluation metric.

Then, for each team, the final score for each scan will be generated using the formula below:

final score = 0.25GPE<sup>* </sup> + 0.25GLE<sup>* </sup> + 0.25LPE<sup>* </sup> + 0.25LLE<sup>* </sup>

The final score for each team will be averaged over all scans in the test set. The final score within the range of [0,1] will be used to produce the final rank for all the submitted algorithms. The final score will be reported with 3 decimal places and the higher the better. For the submissions with the same final score, the rank will be generated based on the runtime. A smaller runtime will be awarded a higher rank. All the raw values for the defined metrics will also be made available.

We also report four other categories of scores, global reconstruction score = 0.5*(1-GPE<sup>* </sup>) + 0.5*(1-GLE<sup>* </sup>), local reconstruction score = 0.5*(1-LPE<sup>* </sup>) + 0.5*(1-LLE<sup>* </sup>), landmark reconstruction score = 0.5*(1-GLE<sup>* </sup>) + 0.5*(1-LLE<sup>* </sup>) and pixel reconstruction score = 0.5*(1-GPE<sup>* </sup>) + 0.5*(1-LPE<sup>* </sup>). These are provided for reference and research interest without formal ranking.

> **_NOTE:_** The minimum score (0) will be given to any case where the code cannot run or the metric cannot be computed successfully. For the submissions with the same final score, the rank will be generated based on the runtime. A smaller runtime will be awarded a higher rank. All the raw values for the defined metrics will also be made available.

<!-- A maximum runtime will be imposed for challenge submissions, benchmarked as the speed of our baseline methods, to encourage usability in the clinical applications.  -->


