# Google Summer of Code - TensorFlow
<p float="left">

<img src="https://summerofcode.withgoogle.com/static/img/summer-of-code-logo.svg" alt="alt text" width="100">
<img src="https://www.gstatic.com/devrel-devsite/prod/vf0396724755d04dbab75050e6812ced8fb2ab11d424163deba5826536b4b1964/tensorflow/images/lockup.svg" alt="alt text" height="100">
<p/>

## Overview
For my GSoC project, I worked with the TensorFlow Model Garden team as a student developer. I was tasked to design and implement a Panoptic Segmentation model for the TensorFlow Model Garden.
#### Introduction
Panoptic Segmentation unifies two well known computer vision tasks - Instance segmentation and Semantic Segmentation. This model produces pixel wise labels that descirbe the category the belongs to and also the instance id of the object it belong to. Categories that have distinct instances (eg. person, dog, car etc) are called as 'things', and the ones that have no notion of instances (eg. sky, ground, vegetation) are termed as 'stuff' categories.

#### Design
Sticking to the design principles of the TensorFlow Model Garden, all the modules were designed to be clear, concise and modular.
 - Instance Segmentation: We decided to go with `MaskRCNN` model since it was already available in the TensorFlow Model Garden and is one of the most popular architectures for instance segmentation task.
 - Semantic Segmentaton: We decided to add an addition head to the `MaskRCNN` which would function as a segmantic segmentation module.
 - Sharing common modules: Both tasks need common modules like the backbone and decoder. We added support for sharing the common modules to reduce the parameter count.
 
#### Implementation
For implementation, I used `tf-vision`, since it has all the necessary building blocks for computer vision tasks/models. Along with clear documentation on usage and the modular design principles, extending `MaskRCNN` architecture to include an additional semantic segmentation task was uneventful. We named the this architecture as `Panoptic MaskRCNN`.
We used the TensorFlow 2.x high level API (Keras) for building creating addition layers (eg: `PanopticSegmentationGenerator`) and for building the final model. We also made sure the model supports distributed training on multiple GPUs and on TPU Pods.

## Tasks
- [x] Add required configs, especially data configs.
- [x] Use Mask R-CNN as the base implementation, and merge code/configs from the semantic segmentation task.
- [x] Implement decoder and parser under dataloader.
- [x] Design and implement panoptic segmentation model architecture.
- [x] Build losses for training. The loss needs to balance the training for instance branch and semantic branch.
- [x] Integrate dataloader, config, modeling, and evaluation metrics into panoptic segmentation task.
- [x] Design and implement post-processing layer to combine instance outputs and semantic outputs. (under review)
- [ ] Complete an actual training job with the above module. (on going)


## Contibutions
Project Page: [Panoptic MaskRCNN](https://github.com/tensorflow/models/tree/master/official/vision/beta/projects/panoptic_maskrcnn)
| Description 	| PR Link                                            	| Status            	|
|-------------	|-------------------------------------------------	|-------------------	|
| added panoptic model that extends `MaskRCNN`     	| https://github.com/tensorflow/models/pull/10045 	| merged            	|
| added factor method for building panoptic maskrcnn     	| https://github.com/tensorflow/models/pull/10076 	| merged            	|
| added dataloader to generate training and validation data for panoptic task     	| https://github.com/tensorflow/models/pull/10112 	| merged            	|
| added training and validation task and supporting configs     	| https://github.com/tensorflow/models/pull/10134 	| merged            	|
| added postprocessing layer to merge instance and semantic segmentation outputs     	| https://github.com/tensorflow/models/pull/10203 	| under review      	|
| add script to process coco panoptic dataset and complete training on the same     	|                                                 	| ongoing           	|

## Future Work
I would be continuing working on the project to add support for additional dasets and tuning the hyperparameters.

## Thanks
This work would not be possible without the constant guidance I received from my mentors - [arashwan](https://github.com/arashwan) [jaeyounkim](https://github.com/jaeyounkim) [margaretmz](https://github.com/margaretmz), Jiageng Zhang and Shicheng (Luke) Xu and the compute made available by [TPU Research Cloud](https://sites.research.google/trc)

