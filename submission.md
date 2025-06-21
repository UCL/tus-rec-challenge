---
title: Submission
layout: default
nav_order: 8
---

# Submission Process

* Participants are encouraged to familiarize themselves with the fundamentals of building and running Docker images; however, advanced Docker expertise is not required. We have provided a <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/main/submission/README.md#instructions-for-docker" target="_blank">basic Docker image</a> to help you get started, which can predict DDFs on the validation/test dataset. The source code is also available in <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/tree/main/submission" target="_blank">`submission`</a> folder.
* The participants are expected to replace the content of <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/main/submission/predict_ddfs.py" target="_blank">`predict_ddfs`</a> function with their own algorithm, which is used in <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/a818cdb708049b6a2209b7dbde6759ef1c8af0e8/submission/test.py#L39" target="_blank">test.py</a>. The function is expected to take one entire scan as input, and output four DDFs. There is no requirement on how the algorithm is designed internally, for example, whether it is learning-based method; frame-, sequence- or scan-based processing; or, rigid-, affine- or nonrigid transformation assumptions.  
* The requirement of the `predict_ddfs` function is described below:
  * Input: 
    * `frames`: All frames in the scan; numpy array with a shape of [N,480,640], where N is the number of frames in this scan.
    * `landmark`: Location of 100 landmarks in the scan; numpy array with a shape of [100,3]. Each row denotes one landmark and the three columns denote the frame index (starting from 0) and the 2d-coordinates of landmarks in the image coordinate system (starting from 1, to maintain consistency with the calibration process). For example, a row like [10,200,100] indicates that there is a landmark in the 10th frame, located at the coordinates [200,100].
    * `data_path_calib`: Path to calibration matrix.
    * `device`: Device to run the model on, provided in <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/a818cdb708049b6a2209b7dbde6759ef1c8af0e8/submission/test.py#L26" target="_blank">this line</a>.
  * Output:  
     * `GP`: Global displacement vectors for all pixels. DDF from the current frame to the first frame, in mm. The first frame is regarded as the reference frame. The DDF should be in numpy array format with a shape of [N-1,3,307200] where N-1 is the number of frames in that scan (excluding the first frame), "3" denotes “x”, “y”, and “z” axes, respectively, and 307200 is the number of all pixels in a frame. The order of the flattened 307200 pixels can be found in function <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/a818cdb708049b6a2209b7dbde6759ef1c8af0e8/submission/utils/plot_functions.py#L6" target="_blank">`reference_image_points`</a>.
     * `GL`: Global displacement vectors for landmarks, in mm. The DDF should be in numpy array format with a shape of [3,100], where 100 is the number of landmarks in a scan.
     * `LP`: Local displacement vectors for all pixels. DDF from current frame to the previous frame, in mm. The previous frame is regarded as the reference frame. The DDF should be in numpy array format with a shape of [N-1,3,307200], where N-1 is the number of frames in that scan (excluding the first frame), "3" denotes “x”, “y”, and “z” axes, respectively, and 307200 is the number of all pixels in a frame. The order of the flattened 307200 pixels can be found in function <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/a818cdb708049b6a2209b7dbde6759ef1c8af0e8/submission/utils/plot_functions.py#L6" target="_blank">`reference_image_points`</a>.
     * `LL`: Local displacement vectors for landmarks, in mm. The DDF should be in numpy array format with a shape of [3,100], where 100 is the number of landmarks in a scan.
     
        
> **_NOTE:_**  
> * If you are not sure about data dimensions, coordinate system or transformation direction, etc., please refer to the <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/main/submission/baseline_model/Prediction.py" target="_blank">example code</a> in `baseline_model` folder. 
>* We have provided two functions, which can generate four DDFs from global and local transformations, in <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline/blob/main/submission/utils/Transf2DDFs.py" target="_blank">`Transf2DDFs.py`</a>.
> * Only modify the implementation of the `predict_ddfs` function. It’s okay to add files but please do not change existing files other than `baseline_model` folder.
> * The order of the four DDFs and the order of 307200 pixels cannot be changed and they must all be numpy arrays. Please ensure your prediction does not have null values. Otherwise, the final score could not be generated.  
> * Your model is expected to run on a single GPU, with GPU memory usage not exceeding 32GB when running docker.
> * Participants are required to dockerize their trained network/algorithm/method and submit them via a file-sharing link (e.g., OneDrive, Dropbox) to the organizers via this <a href="https://forms.office.com/e/dj1g5TKyaj" target="_blank">form</a>.
> * Participants are allowed to make multiple distinct submissions (but must ensure they are not merely simple variations in hyperparameter values), and the best result will be selected for competing. The number of submissions for each team is limited to 5 to preserve variations in hyperparameters.


Please contact [`qi.li.21@ucl.ac.uk`](mailto:qi.li.21@ucl.ac.uk) if you encounter any problem during submission.

Receipt of all submissions will be acknowledged via email within two working days of receipt, and evaluations will be posted on the leaderboard once completed.

The evaluation code, together with the baseline model, is publicly available <a href="https://github.com/QiLi111/TUS-REC2025-Challenge_baseline" target="_blank">here</a>. Participating teams are encouraged, though not obligated, to share their code publicly. Links to any available source code will be provided.