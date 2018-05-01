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
<img align="middle" src="/images/pubs/SceneNetRGBD_ICCV17.png" width="65%"> <br> <br>
 <span style="line-height: 5pt; font-size: 0.8em;">**Abstract**: We introduce SceneNet RGB-D, a dataset providing pixel-perfect ground truth for scene understanding problems such as semantic segmentation, instance segmentation, and object detection. It also provides perfect camera poses and depth data, allowing investigation into geometric computer vision problems such as optical flow, camera pose estimation, and 3D scene labelling tasks. Random sampling permits virtually unlimited scene configurations, and here we provide 5M rendered RGB-D images from 16K randomly generated 3D trajectories in synthetic layouts, with random but physically simulated object configurations. We compare the semantic segmentation performance of network weights produced from pretraining on RGB images from our dataset against generic VGG-16 ImageNet weights. After fine-tuning on the SUN RGB-D and NYUv2 real-world datasets we find in both cases that the synthetically pre-trained network outperforms the VGG-16 weights. When synthetic pre-training includes a depth channel (something ImageNet cannot natively provide) the performance is greater still. This suggests that large-scale high-quality synthetic RGB datasets with task specific labels can be more useful for pretraining than real-world generic pre-training such as ImageNet. We host the dataset at http://robotvault.bitbucket.io/scenenet-rgbd.html. </span>
<br>
<hr>

**Self-Supervised Siamese Learning on Stereo Image Pairs for Depth Estimation in Robotic Surgery.** _Menglong Ye, Ed Johns, Ankur Handa, Lin Zhang, Philip Pratt, Guang-Zhong Yang_, **HSMR 2017**

<br>
<img align="left" src="/images/pubs/HPMI2017.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: Robotic surgery has become a powerful tool for performing minimally invasive procedures, providing advantages in dexterity, precision, and 3D vision, over traditional surgery. One popular robotic system is the da Vinci surgical platform, which allows preoperative information to be incorporated into live procedures using Augmented Reality (AR). Scene depth estimation is a prerequisite for AR, as accurate registration requires 3D correspondences between preoperative and intraoperative organ models. In the past decade, there has been much progress on depth estimation for surgical scenes, such as using monocular or binocular laparoscopes. More recently, advances in deep learning have enabled depth estimation via Convolutional Neural Networks (CNNs), but training requires a large image dataset with ground truth depths. Inspired by, we propose a deep learning framework for surgical scene depth estimation using self-supervision for scalable data acquisition. Our framework consists of an autoencoder for depth prediction, and a differentiable spatial transformer for training the autoencoder on stereo image pairs without ground truth depths. Validation was conducted on stereo videos collected in robotic partial nephrectomy.
 </span>
<hr>

**SemanticFusion: Dense 3D semantic mapping with convolutional neural networks** _John McCormac, Ankur Handa, Andrew Davison, Stefan Leutenegger_, **ICRA 2017**

<br>
<img align="left" src="/images/pubs/ICRA2017.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: Ever more robust, accurate and detailed mapping using visual sensing has proven to be an enabling factor for mobile robots across a wide variety of applications. For the next level of robot intelligence and intuitive user interaction, maps need to extend beyond geometry and appearance — they need to contain semantics. We address this challenge by combining Convolutional Neural Networks (CNNs) and a state-of-the-art dense Simultaneous Localisation and Mapping (SLAM) system, ElasticFusion, which provides long-term dense correspondences between frames of indoor RGB-D video even during loopy scanning trajectories. These correspondences allow the CNN’s semantic predictions from multiple view points to be probabilistically fused into a map. This not only produces a useful semantic 3D map, but we also show on the NYUv2 dataset that fusing multiple predictions leads to an improvement even in the 2D semantic labelling over baseline single frame predictions. We also show that for a smaller reconstruction dataset with larger variation in prediction viewpoint, the improvement over single frame segmentation increases. Our system is efficient enough to allow real-time interactive use at frame-rates of ≈25Hz.
 </span>
 <hr>

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

<br>
<img align="left" src="/images/pubs/ICLR2016.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: We describe a new spatio-temporal video autoencoder, based on a classic spatial image autoencoder and a novel nested temporal autoencoder. The temporal encoder is represented by a differentiable visual memory composed of convolutional long short-term memory (LSTM) cells that integrate changes over time. Here we target motion changes and use as temporal decoder a robust optical flow prediction module together with an image sampler serving as built-in feedback loop. The architecture is end-to-end differentiable. At each time step, the system receives as input a video frame, predicts the optical flow based on the current observation and the LSTM memory state as a dense transformation map, and applies it to the current frame to generate the next frame. By minimising the reconstruction error between the predicted next frame and the corresponding ground truth next frame, we train the whole system to extract features useful for motion estimation without any supervision effort. We present one direct application of the proposed framework in weakly-supervised semantic segmentation of videos through label propagation using optical flow.
 </span>

<hr>
**Understanding real world indoor scenes with synthetic data.** _Ankur Handa, Viorica Pătrăucean, Vijay Badrinarayanan, Simon Stent, Roberto Cipolla_, **CVPR 2016**

<br>
<img align="left" src="/images/pubs/SceneNet_CVPR2016.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: Scene understanding is a prerequisite to many high level tasks for any automated intelligent machine operating in real world environments. Recent attempts with supervised learning have shown promise in this direction but also highlighted the need for enormous quantity of supervised data --- performance increases in proportion to the amount of data used. However, this quickly becomes prohibitive when considering the manual labour needed to collect such data. In this work, we focus our attention on depth based semantic per-pixel labelling as a scene understanding problem and show the potential of computer graphics to generate virtually unlimited labelled data from synthetic 3D scenes. By carefully synthesizing training data with appropriate noise models we show comparable performance to state-of-the-art RGBD systems on NYUv2 dataset despite using only depth data as input and set a benchmark on depth-based segmentation on SUN RGB-D dataset. Additionally, we offer a route to generating synthesized frame or video data, and understanding of different factors influencing performance gains.
 </span>
 <hr>


### 2015 

**SceneNet: Understanding Real World Indoor Scenes With Synthetic Data.** _Ankur Handa, Viorica Pătrăucean, Vijay Badrinarayanan, Simon Stent, Roberto Cipolla_, **arXiv, 2015**


**SegNet: A deep convolutional encoder-decoder architecture for robust semantic pixel-wise labelling.** _Vijay Badrinarayanan, Ankur Handa, Roberto Cipolla_, **arXiv 2015** 


### 2014 

**Robust real-time visual odometry for stereo endoscopy using dense quadrifocal tracking** _Ping-Lin Chang, Ankur Handa, Andrew Davison, Daniel Stoyanov_, **IPCAI 2014**

<hr>

**Simultaneous Mosaicing and Tracking with an Event Camera.** _Hanme Kim, Ankur Handa, Ryad Benosman, Sio-Hoi Ieng, Andrew Davison_, **BMVC 2014** **(Best Industry Paper Prize)**

<br>
<img align="left" src="/images/pubs/BMVC_2014.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: An event camera is a silicon retina which outputs not a sequence of video frames like a standard camera, but a stream of asynchronous spikes, each with pixel location, sign and precise timing, indicating when individual pixels record a threshold log intensity change. By encoding only image change, it offers the potential to transmit the information in a standard video but at vastly reduced bitrate, and with huge added advantages of very high dynamic range and temporal resolution. However, event data calls for new algorithms, and in particular we believe that algorithms which incrementally estimate global scene models are best placed to take full advantages of its properties. Here, we show for the first time that an event stream, with no additional sensing, can be used to track accurate camera rotation while building a persistent and high quality mosaic of a scene which is super-resolution accurate and has high dynamic range. Our method involves parallel camera rotation tracking and template reconstruction from estimated gradients, both operating on an event-by event basis and based on probabilistic filtering.
 </span>
 <hr>



**A Benchmark for RGB-D Visual Odometry, 3D Reconstruction and SLAM** _Ankur Handa, Thomas Whelan, John McDonald, Andrew Davison_, **ICRA 2014**

<br>
<img align="left" src="/images/pubs/ICRA2014.png" width="100%"> <span style="line-height: 0.5; font-size: 0.8em;">**Abstract**: We introduce the Imperial College London and National University of Ireland Maynooth (ICL-NUIM) dataset for the evaluation of visual odometry, 3D reconstruction and SLAM algorithms that typically use RGB-D data. We present a collection of handheld RGB-D camera sequences within synthetically generated environments. RGB-D sequences with perfect ground truth poses are provided as well as a ground truth surface model that enables a method of quantitatively evaluating the final map or surface reconstruction accuracy. Care has been taken to simulate typically observed real-world artefacts in the synthetic imagery by modelling sensor noise in both RGB and depth data. While this dataset is useful for the evaluation of visual odometry and SLAM trajectory estimation, our main focus is on providing a method to benchmark the surface reconstruction accuracy which to date has been missing in the RGB-D community despite the plethora of ground truth RGB-D datasets available.
 </span>
 <hr>

### 2013 and earlier

**Analysing high frame-rate camera tracking** _Ankur Handa_, **PhD Thesis 2013** 

**Real-time camera tracking: When is high frame-rate best?** _Ankur Handa, Richard Newcombe, Adrien Angeli, Andrew Davison_, **ECCV 2012**

**Scalable Active Matching**, _Ankur Handa, Margarita Chli, Hauke Strasdat, Andrew Davison_, **CVPR 2010**

**Person following with a mobile robot using a modified optical flow**, _Ankur Handa, Jayanthi Sivaswamy, K Madhava Krishna, Sartaj Singh_, **Advances in Mobile Robotics 2008**
