---
title: Submission
# layout: home
parent: Past Challenges
nav_order: 6
---

# Submission Process

* We have provided an example docker image [here](https://github.com/QiLi111/tus-rec-challenge_baseline/tree/main/submission#instructions-for-docker), which can predict DDFs on the validation/test dataset. The source code is also available in [`submission`](https://github.com/QiLi111/tus-rec-challenge_baseline/tree/main/submission/) folder.
* The participants are expected to replace the content of [`predict_ddfs`](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/main/submission/predict_ddfs.py) function with their own algorithm, which is used in [test.py](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/5eec6014a7de2b652cdcf7333c58e00f01348560/submission/test.py#L36). The function is expected to take one entire scan as input, and output four kinds of DDFs. There is no requirement on how the algorithm is designed internally, for example, whether it is learning-based method; frame-, sequence- or scan-based processing; or, rigid-, affine- or nonrigid transformation assumptions.  
* The requirement of the `predict_ddfs` function is described below:
  * Input: 
    * `frames`: All frames in the scan; numpy array with a shape of [N,480,640], where N is the number of frames in this scan.
    * `landmark`: Location of 20 landmarks in the scan; numpy array with a shape of [20,3]. Each row denotes one landmark and the three columns denote the index of frame and the 2d-coordinates of landmarks in the image coordinate system. For example, if a row is [10,200,100], it means there is a landmark on the 10th frame, with coordinate of [200,100].
    * `data_path_calib`: Path to calibration matrix.
  * Output:  
     * `GP`: Global displacement vectors for all pixels. DDF from the current frame to the first frame, in mm. The first frame is regarded as the reference frame. The DDF should be in numpy array format with a shape of [N-1,3,307200] where N-1 is the number of frames in that scan (excluding the first frame), "3" denotes “x”, “y”, and “z” axes, respectively, and 307200 is the number of all pixels in a frame. The order of the flattened 307200 pixels can be found in function [`reference_image_points`](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/bc08096d443127637cdaca06935987ddf8314f43/submission/utils/plot_functions.py#L7).
     * `GL`: Global displacement vectors for landmarks, in mm. The DDF should be in numpy array format with a shape of [3,20], where 20 is the number of landmarks in a scan.
     * `LP`: Local displacement vectors for all pixels. DDF from current frame to the previous frame, in mm. The previous frame is regarded as the reference frame. The DDF should be in numpy array format with a shape of [N-1,3,307200], where N-1 is the number of frames in that scan (excluding the first frame), "3" denotes “x”, “y”, and “z” axes, respectively, and 307200 is the number of all pixels in a frame. The order of the flattened 307200 pixels can be found in function [`reference_image_points`](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/bc08096d443127637cdaca06935987ddf8314f43/submission/utils/plot_functions.py#L7).
     * `LL`: Local displacement vectors for landmarks, in mm. The DDF should be in numpy array format with a shape of [3,20], where 20 is the number of landmarks in a scan.
     
        
> **_NOTE:_**  
> * If you are not sure about data dimensions, coordinate system or transformation direction, etc., please refer to the [example code](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/main/submission/baseline_model/Prediction.py) in `baseline_model` folder. 
>* We have provided four functions, which can generate four kinds of DDFs from global and local transformations, in [`Transf2DDFs.py`](https://github.com/QiLi111/tus-rec-challenge_baseline/blob/main/submission/utils/Transf2DDFs.py).
> * Only modify the implementation of the `predict_ddfs` function. It’s okay to add files but please do not change existing files other than `baseline_model` folder.
> *  The order of the four kinds of DDFs and the order of 307200 pixels cannot be changed and they must all be numpy arrays. Please ensure your prediction does not have null values. Otherwise, the final score could not be generated.  
> * Make sure the GPU memory is below 32G when running docker.
> * Participants are required to dockerize their trained network/algorithm/method and submit them via a file-sharing link (e.g., OneDrive, Dropbox) to the organizers via this [form](https://forms.office.com/e/QChhNkLYiu).



<!-- Participants are required to Dockerize their trained network/algorithm/method and submit them via a file-sharing link (e.g., OneDrive, Dropbox) to the organizers via this [form](https://forms.office.com/e/QChhNkLYiu). -->

Please contact [`qi.li.21@ucl.ac.uk`](mailto:qi.li.21@ucl.ac.uk) if you encounter any problem during submission.


<!-- email at [`qi.li.21@ucl.ac.uk`](mailto:qi.li.21@ucl.ac.uk). -->

<!-- The e-mail submission must include:

- Team name;
- Full name(s) of all team members;
- Email address(es) of all team members;
- Team affiliation and country (e.g. University College London, United Kingdom);
- Brief description of method (100 characters maximum);
- File-sharing link to Dockerized algorithm;
- Whether any additional data was used. -->


Receipt of all submissions will be acknowledged via email within two working days of receipt, and evaluations will be posted on the leaderboard once completed.

The evaluation code, together with the baseline models, is publicly available [here](https://github.com/QiLi111/tus-rec-challenge_baseline). Participating teams are encouraged, though not obligated, to share their code publicly. Links to any available source code will be provided.

