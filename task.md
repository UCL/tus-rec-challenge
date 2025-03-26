---
title: Task Description
layout: default
nav_order: 4
---

# Freehand US Reconstruction

The aim of Freehand US reconstruction is to estimate the transformation between any pair of US frames in a US scan without any external tracker, and thus reconstruct 2D Ultrasound (US) images into a 3D volume (see [Fig. 1](#figure1)).

<div align=center>
  <a 
  target="_blank"><img 
  style="padding: 10px;" 
  src="img/rec.png" 
  width=400px
  id="figure1">
  
</a>
</div >

<div align=center>
Fig. 1. An illustration of freehand US reconstruction.
</div >
<!-- <p align="center">
  <img src="img2025/rec.png" />
</p> -->
<!-- <figure>
  <img src="img2025/rec.png" alt="An example workflow of freehand US reconstruction" width="400"/>
  <figcaption>Figure 1: An example workflow of freehand US reconstruction.</figcaption>
</figure> -->


For an US scan $$\mathcal{S}$$, image sequences comprising $$M$$ 2D frames can be sampled as $$S=\{I_m\}, m=1,2,...,M$$, where $$S \subseteq {\mathcal{S}}$$ and $$m$$ represents consecutively increasing time-steps at which the frames are acquired. [Fig. 2](#figure2) shows the relationship among three coordinate systems: the image coordinate system, the tracker tool coordinate system, and the camera coordinate system.  
<div align=center>
  <a 
  target="_blank"><img 
  style="padding: 10px;" 
  src="img/coordinate_system.png" 
  width=400px
  id="figure2">
  
</a>

</div >
<div align=center>
Fig. 2. The relationship among three coordinate systems: the image coordinate system, the tracker tool coordinate system, and the camera coordinate system.
</div>


The rigid transformation from the $$i^{th}$$ frame to the $$j^{th}$$ frame, $$T_{j\leftarrow i}$$, can be obtained using [Eq. 1](#transformation), where $$T_{j\leftarrow i}^{tool}$$ denotes the transformation between $$i^{th}$$ tacker tool to the $$j^{th}$$ track tool, and $$T_{calib}$$ represents the calibration matrix.

<a id="transformation"></a>
$$
T_{j\leftarrow i}= T_{j\leftarrow i}^{tool} \times T_{calib}, 1 \leq i<j \leq M
$$

In general, prior studies have formulated freehand US reconstruction as the estimation of the transformation between two frames in an US sequence. This estimation relies on a function $f$, which serves as the core of freehand US reconstruction, as expressed in [Eq. 2](#freehandUS): 

<a id="freehandUS"></a>
$$
T_{j\leftarrow i} \approx f(I_i, I_j)
$$

Typically, adjacent frames are used in [Eq. 2](#freehandUS), where $$j = i+1$$. The transformation from $$i^{th}$$ frame to the first frame $$T_i$$ can be computed by recursively multiplying the previously estimated relative transformations, as shown in [Eq. 3](#chain-multiplying):

<a id="chain-multiplying"></a>
$$
T_i=T_{i\leftarrow i-1} \times \cdots \times T_{3\leftarrow 2} \times T_{2\leftarrow 1} \times T_{1}
$$

Moreover, [Eq. 3](#chain-multiplying) demonstrates that estimation errors can propagate and accumulate throughout the chain, ultimately resulting in trajectory drift.

Reconstructing the 3D US volume and the trajectory of the US frames requires determining the position of each frame. Since freehand US systems lack an absolute coordinate system, the first frame is chosen as the reference with $$T_1=I$$, where $$I$$ is the identity matrix. As a result, only the relative transformations with respect to the first frame are needed.
For any pixel $p$ in $$i^{th}$$ frame, the coordinate in camera coordinate system $Cor_p$, with respect to the first frame, can be obtained using [Eq. 4](#coordinate).

<a id="coordinate"></a>
$$
Cor_p = T_i \times I_p
$$
<!-- where $T_i$ denotes the transformation from $i^{th}$ frame to the first frame. -->




# Task Description


The algorithm is expected to take the entire scan as input and output two different sets of
transformation-representing displacement vectors as results, a set of displacement vectors on individual pixels and a set of displacement vectors on provided landmarks. There is no requirement on how the algorithm is designed internally, for example, whether it is learning-based method; frame-, sequence- or scan-based processing; or, rigid-, affine- or nonrigid transformation assumptions. Details are explained further in [assessment](assessment.html).

Participant teams are expected to make use of the sequential data and potentially make knowledge transfer from other domains such as computer vision and computer-assisted intervention. The participant teams are expected to take US scan as input and output two sets of pixel displacement vectors, indicating the transformation to reference frame, i.e., first frame in this task. The evaluation process will take the generated displacement vectors from their dockerized models, and produce the final accuracy score to represent the reconstruction performance, at local and global levels, representing different clinical application of the reconstruction methods.

We provide a baseline algorithm adapted from <a href="https://doi.org/10.1109/TBME.2023.3325551" target="_blank">Li et al. 2023</a> in this <a href="TBA" target="_blank">repo</a>. [TBA]

# Application scenarios

Trackless 3D freehand US reconstruction will be useful in clinical practice where 3D visualisation is required but external trackers are not allowed or inaccessible. By estimating the relative transformations among US frames using solely 2D US images, the 3D position for each US frame could be calculated and thus the entire US scan could be reconstructed without using any information from external trackers.

# Difference between TUS-REC2025 and TUS-REC2024

From the results of TUS-REC2024, we observed that the reconstruction performance is dependent on scan protocol. In TUS-REC2025, we want to investigate the reconstruction performance on scans with a new rotating scanning protocol, with which the reconstruction performance may be further improved owing to its dense sampling of the area to be reconstructed. Compared with TUS-REC2024, TUS-REC2025 provides more data with new scanning protocol, and the previous released larger data with non-rotating scanning protocols is open to use. The new challenge aims to 1) benchmark the model performance on relatively small rotating data and 2) benchmark the model generalisation ability among different scanning protocols.