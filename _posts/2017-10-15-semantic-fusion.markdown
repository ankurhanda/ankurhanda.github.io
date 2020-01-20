---
layout: post
title:  "SemanticFusion: Dense 3D Semantic Mapping with Convolutional Neural Networks"
date:   2017-10-15 22:22:59 +00:00
image: /images/semantic_fusion.png
categories: research
author: "Ankur Handa"
authors: "John McCormac, <strong>Ankur Handa</strong>, Stefan Leutenegger, Andrew J. Davison"
venue: "International Conference on Robotics and Automation (ICRA)"
arxiv: https://arxiv.org/abs/1609.05130
---
We combine Convolutional Neural Networks (CNNs) and a state of the art dense Simultaneous Localisation and Mapping(SLAM) system, ElasticFusion, which provides long-term dense correspondence between frames of indoor RGB-D video even during loopy scanning trajectories. These correspondences allow the CNN's semantic predictions from multiple view points to be probabilistically fused into a map. Our system is efficient enough to allow real-time interactive use at frame-rates of approximately 25Hz.
