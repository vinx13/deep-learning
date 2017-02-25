# Scene Parsing

The goal of scene parsing is to assign each pixel in the image a category label, which is rather challenging when considering diverse scenes and unrestricted vocabulary.

There are several issues that should be addressed such as mismatched relationship, confusion categories and inconspicuous classes.

These issues implies the need for exploitation of global context information. [1] proposes the pyramid pooling module that can utilizes global context information by extracting features from sub-regions in different scales. It uses ResNet to extract features from the original image, which are then scaled in a pyramid pattern. Deeper features are extracted for feature maps in each scale and then upsampled to the same size and concatenated together, producing feature maps that contain information in different scales as it claims that flattening a image pyramid into a vector leads to the loss of spacial information. Pixel-level classification is performed on the last feature maps.

It also introduces an auxiliary loss function to optimize the training process as increasing depth of the network may introduce additional optimization difficulty. Gradients of both loss functions are propagated through the entire network.

#### Reference
[1] Hengshuang Zhao, Jianping Shi, Xiaojuan Qi, Xiaogang Wang and Jiaya Jia. Pyramid Scene Parsing Network.
