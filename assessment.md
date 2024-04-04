---
title: Assessment
layout: home
nav_order: 4
---

# Assessment Criteria

## Metrics

For each scan, the submitted method is tasked to output two types of transformation-representing displacement vectors (hereinafter is also referred to as the prediction), at global and local levels.

- The "global displacement vectors" will be used to reconstruct individual frames (without the first frame), with respect to the first frame in the scan as the "global reference frame".
- The "local displacement vectors" will be used to reconstruct individual frames (without the first frame), with respect to the immediately previous frame in the scan as the "local reference frame".

For each scan, the performance of a submitted method will be evaluated using two reconstruction errors,
"landmark reconstruction error" and "pixel reconstruction error".
- The "landmark reconstruction error" is defined as average Euclidean distance, between the
ground-truth-reconstructed frame and the prediction-reconstructed frame, averaged over a set of predefined anatomical landmarks in each scan.
- The "pixel reconstruction error" is defined as the same average Euclidean distance, between the
ground-truth-reconstructed frame and the prediction-reconstructed frame, averaged over all pixels of all but the first frames in each scan.

Thus, each submitted method should output four sets of displacement vectors:
- Global displacement vectors for pixel reconstruction (number of the "GP" vectors = number of pixels in the entire scan)
- Global displacement vectors for landmark reconstruction (number of the "GL" vectors = number of defined landmarks in the scan)
- Local displacement vectors for pixel reconstruction (number of the "LP" vectors = number of pixels in the entire scan)
- Local displacement vectors for landmark reconstruction (number of the "LL" vectors = number of defined
landmarks in the scan)

Based on these four output vector sets, four evaluation metrics will be used in this challenge:
- Global pixel reconstruction error (GPE), the pixel reconstruction error using GP vectors.
- Global landmark reconstruction error (GLE), the landmark reconstruction error using GL vectors.
- Local pixel reconstruction error (LPE), the pixel reconstruction error using LP vectors.
- Local landmark reconstruction error (LLE), the landmark reconstruction error using LL vectors.

<!-- {: .Note}  -->
<!-- The landmark is defined based on anatomical structures, such as vessel branches, bony structures and other ad hoc landmarks. It is estimated that between 10-20 landmarks will be available for each scan, but this is subject to further verification. Further details and summary statistics of the landmarks will be made available by the challenge commence. The final score on the four evaluation metrics will be averaged over all scans in the test set. -->
> **_NOTE:_** Runtime will be considered as additional evaluation metric which is the consumed time of predicting positions for all frames in a scan, averaged over all scans in the test set.

## Rationale in using these metrics

**Rationale in using Euclidean distance-based error metrics, as opposed to errors defined in transformation parameter space**

Direct measuring the accuracy of parameters of transformation matrix is difficult since the
contribution and weighting between rotation and translation components can be sensitive to experimental and imaging configurations, such as reference coordinates and definition of rotation axis, and dependent on application. In this challenge, metrics based on distance error is preferred, which is arguably considered a more practical type of measure to reflect the difference between ground truth and prediction in Euclidean space ([Luo et al. 2023](https://doi.org/10.1016/j.media.2023.102810)).

**Justification of using displacement-based representation of transformation, as opposed to rigid- or affine matrices, as the algorithm output**

Although the ground-truth are available in the form of rigid transformation, we
argue that, from experience in developing similar numerical algorithms, enforcing the algorithm output to be homogeneous transformation is not only unnecessary, but sometimes misleadingly encourages a more
numerically challenging solution due to issues such as gimbal lock in using rotation matrix, local minima in numerical optimisation. In addition, the displacement-based representation allows flexibility for a quantitatively more accurate reconstruction, with a near-rigid transformation, which could be sufficient for clinical use. However, there is no requirement in the internal methodology adopted, for example, the submitted algorithm can convert a single estimated rigid transformation matrix to all these four types of required displacement vectors as output.

**Justification of the local and global reconstruction errors**

The reconstructed scan from either local level or global level displacement are capable of representing different types of reconstruction performance, such as frame-level reconstruction error and accumulated error of the algorithm ([Li. et al. 2023](https://doi.org/10.1109/TBME.2023.3325551), [Wein et al. 2020](https://link.springer.com/chapter/10.1007/978-3-030-59716-0_49)). To streamline the evaluation, other monotonic metrics, such as final drift and Dice overlap, albeit commonly reported in literature (e.g. [Li et al 2023](https://doi.org/10.1109/TBME.2023.3325551)), are not included. However, in practical applications, one might choose to reconstruct a sequence of ultrasound frames (as opposed to the entire scan or two adjacent frames, which are represented by local and global errors, respectively), using a pre-optimised sequence length that is most suitable to the downstream application. Without specifying a single target clinical application, these two adopted local and global errors shall represent the range of accuracy between the choices of the reconstruction length.



## Ranking method

First, for each individual metric, the values for all submissions will be normalised to the range [0, 1] by the value of baseline method, and then the final score will be generated using the formula below:

Overall score = 0.25*(1-GPE<sup>* </sup>) + 0.25*(1-GLE<sup>* </sup>) + 0.25*(1-LPE<sup>* </sup>) + 0.25*(1-LLE<sup>* </sup>)

where * indicates the normalised reconstruction errors. The "overall score" within the range of [0,1] will be used to produce the final rank for all the submitted algorithms. The final score will be reported with 3 decimal places and the higher the better. 

We also report four other categories of scores, global reconstruction score = 0.5*(1-GPE<sup>* </sup>) + 0.5*(1-GLE<sup>* </sup>), local reconstruction score = 0.5*(1-LPE<sup>* </sup>) + 0.5*(1-LLE<sup>* </sup>), landmark reconstruction score = 0.5*(1-GLE<sup>* </sup>) + 0.5*(1-LLE<sup>* </sup>) and pixel reconstruction score = 0.5*(1-GPE<sup>* </sup>) + 0.5*(1-LPE<sup>* </sup>). These are provided for reference and research interest without formal ranking.

> **_NOTE:_** The minimum score (0) will be given to any case where the code cannot run or the metric cannot be computed successfully. For the submissions with the same final score, the rank will be generated based on the runtime. A smaller runtime will be awarded a higher rank. A maximum runtime will be imposed for challenge submissions, benchmarked as the speed of our baseline methods, to encourage usability in the clinical applications. All the raw values for the defined metrics will also be made available.


