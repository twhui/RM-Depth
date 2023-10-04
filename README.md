[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/rm-depth-unsupervised-learning-of-recurrent-1/unsupervised-monocular-depth-estimation-on)](https://paperswithcode.com/sota/unsupervised-monocular-depth-estimation-on?p=rm-depth-unsupervised-learning-of-recurrent-1)

# RM-Depth

This repository (https://github.com/twhui/RM-Depth) is the offical project page for my paper <a href="https://arxiv.org/pdf/2303.04456.pdf"><strong>RM-Depth: Unsupervised Learning of Recurrent Monocular Depth in Dynamic Scenes</strong></a> published in CVPR 2022. <i>The up-to-date version of the paper is available on <a href="https://arxiv.org/pdf/2303.04456.pdf"><strong>arXiv</strong></a></i>. The supplementary material is available <a href="https://github.com/twhui/RM-Depth/blob/main/Supplementary%20Material%20for%20RM-Depth%20Unsupervised%20Learning%20of%20Recurrent%20Monocular%20Depth%20in%20Dynamic%20Scenes_CVPR22.pdf"><strong>here</strong></a></i>.

<a href="https://www.youtube.com/watch?v=0r4Je86w1Cg">
<p align="center"><img src="./figures/demo video thumbnail.png" width="600" /></p>
</a>

# Overview
<p align="center"><img src="./figures/RM-Depth.png" width="700" /></p>
A new unsupervised CNN is proposed to predict single-image depth map and complete 3D motion (motions of moving objects and camera itself) in dynamic scenes without requiring scene rigidity and semantic labels. Optical flow and moving object segementations are also recovered. 
<br><br>
Major contributions: (1) Recurrent modulation units (RMU) are proposed to adaptively and iteratively combine encoder and decoder features. (2) Residual upsampling is proposed for fast and efficient resizing of feature maps while sharp depth can be resulted. (3) A warping-based network is proposed to estimate a motion field of moving objects without using semantic priors. The motion field is further regularized by an outlier-aware training loss. 
<br><br>
Despite the depth model just uses a single image in test time and 2.97M parameters, it achieves state-of-the-art results on the KITTI and Cityscapes benchmarks (AbsRel = 0.107 and 0.090, respectively). Besides, It can run at 40FPS (image size: 640 x 192) on a NVIDIA 1080 GPU.

# Recurrent Modulation Unit (RMU)
<p align="center"><img src="./figures/RMU.png" width="400" /></p>

Fusion of feature maps across encoder and decoder often appears in depth estimation. In RM-Depth, the depth decoder consists of RMUs. The fusion is iteratively refined by adaptive modulating the encoder features using the hidden state of RMU. This in turn improves the performance of single-image depth inference.

# Residual upsampling
Conventionally, feature maps are upsampled using a single set of filters. In this work, multiple sets of filters are proposed such that each set of them is specifically trained for upsampling some of the spectral components. This effectively improves upsampling along edges.

# Motion Network
<p align="center"><img src="./figures/motion network.png" width="400" /></p>
Besides camera motion, a 3D motion field of moving objects is recovered in a coarse-to-fine framework through a warping approach. The unsupervised learning of motion field is further improved by introducing an outlieraware regularization loss.

# Depth Prediction Results
</ul>
<table>
<thead>
<tr>
<th align="center"></th>
<th align="center">Semantic Prior</th> 
<th align="center">KITTI Testing Set (Eigen split)</th>
<th align="center">Cityscapes Testing Set</th>
<th align="center">Model Size (M)</th> 
</tr>
<tr>
<td align="center">Monodepth2 (ICCV19)</td>
<td align="center"></td>  
<td align="center">0.115</td>
<td align="center">-</td>
<td align="center">14.84</td>
</tr> 
<tr>
<td align="center">PackNet (CVPR20)</td>
<td align="center"></td>  
<td align="center">0.111</td>
<td align="center">-</td>
<td align="center">128.29</td>
</tr>
<tr>
<td align="center">Lee et al. (ICCV21)</td>
<td align="center">&#x2022</td> 
<td align="center">0.114</td>
<td align="center">0.116</td>
<td align="center">22.77</td>
</tr>
<tr>
<td align="center">Lee et al. (AAAI21)</td>
<td align="center">&#x2022</td> 
<td align="center">0.112</td>
<td align="center">0.111</td>
<td align="center">14.84</td>
</tr> 
<tr>
<td align="center"><strong>RM-Depth (CVPR22),<BR> updated results</strong></td>
<td align="center"></td> 
<td align="center"><strong>0.107 (trained on K)</strong> (<a href="https://www.dropbox.com/s/4rfnkvtvp1bvmt6/RM-Depth_KITTI_predictions.rar?dl=0">predictions</a>)<strong>,<BR> 0.105 (trained on CS+K)</strong> (<a href="https://www.dropbox.com/s/w2pu52jiwenberz/RM-Depth_KITTI_predictions%20%28trained%20on%20CS%2BK%29.rar?dl=0">predictions</a>)</td>
<td align="center"><strong>0.090</strong> (<a href="https://www.dropbox.com/s/yc6xxfgkoay1svs/RM-Depth_CS_predictions.rar?dl=0">predictions</a>)</td>
<td align="center"><strong>2.97</strong></td>
</tr>    
<tr>
<td align="center"><strong>RM-Depth (CVPR22),<BR> 1024 x 320</strong></td>
<td align="center"></td> 
<td align="center"><strong>0.106</strong> (<a href="https://www.dropbox.com/s/2qrqx3rtgaqj3r3/RM-Depth_K_predictions_1024x320.rar?dl=0">predictions</a>)<strong></td>
<td align="center"><strong>0.088</strong> (<a href="https://www.dropbox.com/s/7zwwp1w3gbs6091/RM-Depth_CS_predictions_1024x320.rar?dl=0">predictions</a>)</td>
<td align="center"><strong>2.97</strong></td>
</tr>
</tbody></table>

# Code Package
Please contact Dr. T.-W. Hui (e-mail provided in the first page of the paper) for academic research or commerical collaborations.

# License and Citation
This software and associated documentation files (the "Software"), and the research paper (<i>RM-Depth: Unsupervised Learning of Recurrent Monocular Depth in Dynamic Scenes</i>) including but not limited to the figures, and tables (the "Paper") are provided for academic research purposes only and without any warranty. Any commercial use requires my consent. When using any parts of the Software or the Paper in your work, please cite the following paper:

<pre><code>@InProceedings{hui22rmdepth,
 author = {Tak-Wai Hui},
 title = {RM-Depth: Unsupervised Learning of Recurrent Monocular Depth in Dynamic Scenes},
 booktitle = {Proceedings of IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
 pages = {1675--1684},
 year = {2022}
}</code></pre>
