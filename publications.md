---
layout: page
title: Publications
permalink: /publications/
---
### 2018
<hr>
**Domain Randomization and Generative Models for Robotic Grasping** _Josh Tobin, Lukas Biewald, Rocky Duan, Marcin Andrychowicz, Ankur Handa, Vikash Kumar, Bob McGrew, Alex Ray, Jonas Schneider, Peter Welinder, Wojciech Zaremba, Pieter Abbeel_ **arXiv 2018**

<br>
<img align="left" src="/images/pubs/josh_DR_GM.png" width="100%"> <span style="line-height: 1.1; font-size: 0.8em;">**Abstract**: Deep learning-based robotic grasping has made significant progress thanks to algorithmic improvements and increased data availability. However, state-of-the-art models are often trained on as few as hundreds or thousands of unique object instances, and as a result generalization can be a challenge.  In this work, we explore a novel data generation pipeline for training a deep neural network to perform grasp planning that applies the idea of domain randomization to object synthesis. We generate millions of unique, unrealistic procedurally generated objects, and train a deep neural network to perform grasp planning on these objects.  Since the distribution of successful grasps for a given object can be highly multimodal, we propose an autoregressive grasp planning model that maps sensor inputs of a scene to a probability distribution over possible grasps. This model allows us to sample grasps efficiently at test time (or avoid sampling entirely).  We evaluate our model architecture and data generation pipeline in simulation and the real world. We find we can achieve a >90% success rate on previously unseen realistic objects at test time in simulation despite having only been trained on random objects. We also demonstrate an 80% success rate on real-world grasp attempts despite having only been trained on random simulated objects. </span>
<br>
<hr>


### 2017

**SceneNet RGB-D: Can 5M Synthetic Images Beat Generic ImageNet Pre-training on Indoor Segmentation?** _John McCormac, Ankur Handa, Stefan Leutenegger, Andrew Davison_, **ICCV 2017**
<br>
<img align="center" src="/images/pubs/SceneNetRGBD_ICCV17.png" width="65%"> <br> <br>
 <span style="line-height: 5pt; font-size: 0.8em;">**Abstract**: We introduce SceneNet RGB-D, a dataset providing pixel-perfect ground truth for scene understanding problems such as semantic segmentation, instance segmentation, and object detection. It also provides perfect camera poses and depth data, allowing investigation into geometric computer vision problems such as optical flow, camera pose estimation, and 3D scene labelling tasks. Random sampling permits virtually unlimited scene configurations, and here we provide 5M rendered RGB-D images from 16K randomly generated 3D trajectories in synthetic layouts, with random but physically simulated object configurations. We compare the semantic segmentation performance of network weights produced from pretraining on RGB images from our dataset against generic VGG-16 ImageNet weights. After fine-tuning on the SUN RGB-D and NYUv2 real-world datasets we find in both cases that the synthetically pre-trained network outperforms the VGG-16 weights. When synthetic pre-training includes a depth channel (something ImageNet cannot natively provide) the performance is greater still. This suggests that large-scale high-quality synthetic RGB datasets with task specific labels can be more useful for pretraining than real-world generic pre-training such as ImageNet. We host the dataset at http://robotvault.bitbucket.io/scenenet-rgbd.html. </span>
<br>
<hr>

**Self-Supervised Siamese Learning on Stereo Image Pairs for Depth Estimation in Robotic Surgery.** _Menglong Ye, Ed Johns, Ankur Handa, Lin Zhang, Philip Pratt, Guang-Zhong Yang_, **HSMR 2017**

**SemanticFusion: Dense 3D semantic mapping with convolutional neural networks** _John McCormac, Ankur Handa, Andrew Davison, Stefan Leutenegger_, **ICRA 2017**

### 2016 

**SceneNet RGB-D: 5M Photorealistic Images of Synthetic Indoor Trajectories with Ground Truth.** _John McCormac, Ankur Handa, Stefan Leutenegger, Andrew Davison_, **arXiv, 2016**

**HDRFusion: HDR SLAM using a low-cost auto-exposure RGB-D sensor.** _Shuda Li, Ankur Handa, Yang Zhang, Andrew Calway,_ **3DV 2016**

<hr>

**gvnn: Neural network library for geometric computer vision.** _Ankur Handa, Michael Bloesch, Viorica Pătrăucean, Simon Stent, John McCormac, Andrew Davison_, **ECCVWorkshop 2016**
<br>
<img align="left" src="/images/pubs/so3_exp.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: We introduce gvnn, a neural network library in Torch aimed towards bridging the gap between classic geometric computer vision and deep learning. Inspired by the recent success of Spatial Transformer Networks, we propose several new layers which are often used as parametric transformations on the data in geometric computer vision. These layers can be inserted within a neural network much in the spirit of the original spatial transformers and allow backpropagation to enable end-toend learning of a network involving any domain knowledge in geometric computer vision. This opens up applications in learning invariance to 3D geometric transformation for place recognition, end-to-end visual odometry, depth estimation and unsupervised learning through warping with a parametric transformation for image reconstruction error. </span>
<br>

<hr>

**Spatio-temporal video autoencoder with differentiable memory.** _Viorica Pătrăucean, Ankur Handa, Roberto Cipolla_, **ICLRWorkshop 2016**

**Understanding real world indoor scenes with synthetic data.** _Ankur Handa, Viorica Pătrăucean, Vijay Badrinarayanan, Simon Stent, Roberto Cipolla_, **CVPR 2016**

### 2015 

**SceneNet: Understanding Real World Indoor Scenes With Synthetic Data.** _Ankur Handa, Viorica Pătrăucean, Vijay Badrinarayanan, Simon Stent, Roberto Cipolla_, **arXiv, 2015**


**SegNet: A deep convolutional encoder-decoder architecture for robust semantic pixel-wise labelling.** _Vijay Badrinarayanan, Ankur Handa, Roberto Cipolla_, **arXiv 2015** 


### 2014 

**Robust real-time visual odometry for stereo endoscopy using dense quadrifocal tracking** _Ping-Lin Chang, Ankur Handa, Andrew Davison, Daniel Stoyanov_, **IPCAI 2014**

**Simultaneous Mosaicing and Tracking with an Event Camera.** _Hanme Kim, Ankur Handa, Ryad Benosman, Sio-Hoi Ieng, Andrew Davison_, **BMVC 2014** **(Best Industry Paper Prize)**

**A Benchmark for RGB-D Visual Odometry, 3D Reconstruction and SLAM** _Ankur Handa, Thomas Whelan, John McDonald, Andrew Davison_, **ICRA 2014**

### 2013 and earlier

**Analysing high frame-rate camera tracking** _Ankur Handa_, **PhD Thesis 2013** 

**Real-time camera tracking: When is high frame-rate best?** _Ankur Handa, Richard Newcombe, Adrien Angeli, Andrew Davison_, **ECCV 2012**

**Scalable Active Matching**, _Ankur Handa, Margarita Chli, Hauke Strasdat, Andrew Davison_, **CVPR 2010**

**Person following with a mobile robot using a modified optical flow**, _Ankur Handa, Jayanthi Sivaswamy, K Madhava Krishna, Sartaj Singh_, **Advances in Mobile Robotics 2008**
