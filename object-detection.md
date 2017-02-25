# Object Detection

## R-CNN, Fast R-CNN and Faster R-CNN
Advances in object detection such as [1][2][3] utilize region proposal methods and convolution neuron network. These works use models like VGG to extract feature maps from the original image and selective search method to propose regions of interest (RoI). For each proposed RoI, bounding box regression and classification tasks are performed on the corresponding region in the feature map.

Fast R-CNN first compute the feature map of the whole original image. Then RoIs are proposed from the original image and mapped to the region in the feature map, preventing unnecessary computations to extract features of each RoI. Besides, it uses ROI-pooling which support
multi-scale input by scaling them to a unified output size. It also combines localization and classification tasks together by optimizing a joint loss function of both tasks.

However, region proposal methods like selective search are still computationally expensive. Faster R-CNN use region proposal network (RPN) that enables the network to learn to propose RoI, which is efficient and makes it possible to perform real time detection.

### Region Proposal Network
#### Anchor
Each point in the feature map is called an anchor. For each anchor, it predicts k (k = 9 in this paper) RoI with different scales and ratios of aspects. For each RoI, it performs classification to determine whether it is background. For each proposed RoI, it performs bounding box regression with reference to the anchor.

#### Loss Function
The loss function of RPN is based on IoU between proposed region and the ground truth box. The anchors with the highest IoU or that higher than 0.7 are labeled as positive samples.

#### Training
It uses image-centric sampling strategy. Each mini-batch comes from a single image to prevent biasing toward negative samples as samples of both labels are not balanced.

### Sharing Features for RPN and Fast R-CNN
We hope to share the network between RPN and Fast R-CNN as they both uses a convnet to extract feature maps. However, RPN for proposals and Fast R-CNN for detections will change in different directions during training. Faster R-CNN utilizes a four-step alternating training method by switching between RPN and Fast R-CNN.

## YOLO and YOLO 9000
YOLO is a efficient and real-time object detection system with simple architecture. Unlike models like R-CNN that follows a proposal-detect pattern, it reframe the task as simple regressions. It split the input image into SxS cells, each cell is responsible to detect the object if its center falls into that cell. For each cell, it predicts B bounding boxes and the corresponding confidence. Also, it predicts C classes scores for each cell which is independent from the predicted bounding boxes.

YOLO 9000 is the improved version of YOLO, which is better, faster and stronger. Similar to Faster R-CNN, it also predict anchor boxes relative bounding box locations instead of absolute coordinations in YOLO such that fully connected layers can be eliminated. However, instead of hand-picked anchor box scales and ratios, it uses k-means clustering on the training set bounding boxes to search them.
YOLO 9000 is trained with alternating input scales. It takes the advantage of joint training mechanism that combines classification and detection dataset together by using a multi-label model building up a hierarchical label graph. Instead of softmax function widely used in classification tasks which produces mutually exclusive probabilities for each category, it predicts the probability from the root down along the directed graph, leading to good generalization.

#### Reference
[1] Ross Girshick, Jeff Donahue, Trevor Darrell, and Jitendra Malik. Rich feature hierarchies for accurate object detection and semantic segmentation Tech report (v5).  
[2] Kaiming He, Xiangyu Zhang, Shaoqing Ren, and Jian Sun. Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition.  
[3] Ross Girshick. Fast R-CNN.  
[4] Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun. Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks.  
[5] Joseph Redmon, Santosh Divvala, Ross Girshick, and Ali Farhadi. You Only Look Once: Unified, Real-Time Object Detection.  
[6] Joseph Redmon and Ali Farhadi. YOLO9000: Better, Faster, Stronger. It utilizes batch normalization and high-resolution input to increase accuracy.  
