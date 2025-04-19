---
title: Submission
layout: default
nav_order: 8
---

# Submission Process

We will prepare a Docker container to provide a consistent submission environment. The detailed information of the release and usage of the Docker container will be announced in our website later. 

<!-- The evaluation code, together with the baseline models, is publicly available [here](https://github.com/QiLi111/tus-rec-challenge_baseline). Participating teams are encouraged, though not obligated, to share their code publicly. Links to any available source code will be provided. -->

<!-- The algorithm is expected to take the entire scan as input and output two different sets of transformation-representing displacement vectors as results, a set of displacement vectors on individual pixels and a set of displacement vectors on provided landmarks. There is no requirement on how the algorithm is designed internally, for example, whether it is learning-based method; frame-, sequence- or scan-based processing; or, rigid-, affine- or nonrigid transformation assumptions. Details are explained further in "Metric" section. -->

> **_NOTE:_**  
> * We are planning to provide a small validation set, which allows participants to tune their models using these unseen data, and also perform a self-evaluation on the validation data for a sanity check using their Docker images. The participants are allowed to make multiple distinct submissions (but must ensure they are not merely simple variations in hyperparameter values), and the best result will be selected for competing. The number of submissions for each team is limited to 5 to preserve variations in hyperparameters.
<!-- > * We expect your model to run on a single GPU, and make sure the GPU memory is below 32G when running docker.  -->
> * Participants are required to dockerize their trained network/algorithm/method and submit them via a file-sharing link (e.g., OneDrive, Dropbox) to the organizers via this <a href="TBA" target="_blank">form [TBA]</a>. Participants are encouraged to familiarize themselves with the fundamentals of building and running Docker images; however, advanced Docker expertise is not required. A sample Docker image will be provided to help you get started.
> * Your model is expected to run on a single GPU, with GPU memory usage not exceeding 32GB when running docker.