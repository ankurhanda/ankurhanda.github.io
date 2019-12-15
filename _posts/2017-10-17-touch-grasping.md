---
title: Touch sensing for grasping
---

Most grasping attempts in computer vision and robotics have primilarily been based on RGB images. Cameras are cheap and if you have a decent infrastructure to collect dataset (either in real world or simulations) you are in a very good spot to play with robotic grasping with vision. Grasping is a challenging problem but humans are often very good at determining an appropriate grasp location to hold an object or doing any complicated manipulation. This is largely in part due to our superior tactile sensing and extreme dexterity that the human hand offers.

Recently, a paper from BAIR, showed the benefits of adding tactile sensing on grasp outcome prediction. The two-finger gripper they used is equipped with GelSight high-res tactile sensor which provides raw-pixel measurements at a resolution of 1280x960 at 30Hz _i.e._ the sensory data it provides is a standard 2D image which can be used in the same way a regular RGB image is used.

GelSight is a surface topography measurement device composed of an elastomer covered with a reflective skin. When an object presses against the surface, the skin deforms and takes the shape of the object's surface. It is able to capture very fine details of the order of 2 microns. In contrast to the active and passive depth scanning, GelSight is able to obtain the surface topography of even transparent and surfaces with non-regular properties. It consists of three components: 

- silicon gel that takes the shape of the object.
- coloured LEDs to illuminate the deformed membrane.
- camera to capture the images.

The three-color LEDs illuminate the gel from different angles. Since each surface normal corresponds to a unique color, the color image captured by the camera can be directly used to reconstruct the depth map of the contact surface by looking up a calibrated color-surface normal table. This is the principle behind GelSight sensor.

In the following, we look at various surface deformations on the skin of the sensor for various objects provided as 2D images.
![Alt Text](/images/touch-grasping-blog/GelSightImages.png) 

**How do they predict the successful grasp from vision and touch?**

They use a convolutional neural network, pre-trained ResNet-50, to to predict the grasp success outcome. 

![Alt Text](/images/touch-grasping-blog/GraspingArch.png) 

More formally, the network produces $$y = f(x)$$ where $$x = (I_{RGB}, I_{GelSightL}, I_{GelSightR})$$ where $$I_{RGB}, I_{GelSightL}, I_{GelSightR}$$ represent the image from the external frontal camera and the images from the two fingertip gelsight sensors (left and right) and $$f$$ is the ResNet-50 convolutional neural network. As the diagram suggests they take images for before and during grasping events presumably to get the gradient of the input that is fed to the network to produce the outcome. We will need some temporal information _i.e._ the change that happened since the robot arm started moving. 

However, there is a catch here - the model can only tell whether the grasp is successful or not after the gripper has closed its fingers around the object. Therefore, even at test time, they have to do random search within the vicinity of the object and find out which grasp is successful via their predict-and-evaluate procedure. This means they have to try many random grasps before they find out the current best grasp. It is not clear to me how the number of random grasps varies with different objects. 

**Limitations**

I think the obvious limitation of this work is that the robot has to try various grasp locations at test time. Although it is natural to try and interact with the object to a few times to learn about the surface geometry to predict the best grasp but this work as of now doesn't really do in a principled way. One could also argue that they don't seem to maintain a memory of where they have grasped before which could potentially be used for build the 3D model online (may not even need tactile feedback here but a single camera SLAM could be potentially useful) and therefore, be more useful to find the optimal grasp. In a way they seem to use the sensor only for obtaining the heightmap when the grippers come in contact with the object. Maintaining the history of grasping within an RNN framework or within a SLAM framework could help potentially do an online gradient descent on the optimal grasp location. 

If you have time constraints, the robot obviously cannot try random guesses and judge which one is best - it will need to be a principled way so that it does it within an allotted time budget which is something we should consider seriously when designing robotic systems. Also, I don't think they do it in this paper - they could potentially use the random guesses and the corresponding success probabilities to obtain a heat-map of the optimal grasps and see how that changes according to object surfaces.

**Closing thoughts**

Overall, I'm quite excited at the prospects of using tactile feedback for grasping and manipulation. This work is the first to present an end-to-end learned system for robotic grasping that combines visual and tactile sensing. Vision and touch sensors are quite complementary - vision helps get closer to the object and touch helps in interacting with it and provides immediate feedback on the quality of interaction. Historically, tactile sensing has been costly and sensitive and has not seen much use but sensors like GelSight offer a way to obtain precise surface geometry when the object is pressed against its skin. 

It is also important to be pragmatic and use the appropriate tool/hardware whenever so that the inference algorithms are simpler and easier to train. 


**References**

R. Calandara _et al._ **The Feeling of Success:
Does Touch Sensing Help Predict Grasp Outcomes?**, CoRL 2017.