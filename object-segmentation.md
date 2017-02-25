# Object Segmentation

Object segmentation is generally modeled as pixel-level classification tasks with no awareness of individual instances. [1] divides instance-aware semantic segmentation into three subtasks:

- Differentiating instances
- Estimating masks
- Categorizing objects

Different from other multi-task learning processes, in this model each subtask depends the previous subtask, forming a cascade pattern.  

At first, it uses RPN in [2] to generate bounding boxes, predicting their coordinates, scales and the objectness probabilities. At the next stage, it uses ROI pooling method to generate fixed-sized (14x14) feature from bounding boxes with arbitrary sizes. Two fully connected layers are appended to flatten features and produce pixel-level masks (28x28). Along with masks, features are fed into two fully connected layers in pathway to predict category labels.

As each stage takes the output of the previous stage as its input, some issues when applying the chain rule to the loss function faces should be addressed. The main challenge is that the loss function of masks involves with the feature map as well as bounding boxes generated in the first stage, compared with pre-computed bounding boxes in fast R-CNN that have no effects on the gradient. This paper proposes a differentiable ROI warping layer that tackles back propagation.

#### Reference
[1] Jifeng Dai, Kaiming He, and Jian Sun. Instance-aware Semantic Segmentation via Multi-task Network Cascades.  
[2] Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun. Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks.
