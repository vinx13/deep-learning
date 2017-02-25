# Multi-object Tracking
Multi-object tracking (MOT) is approached from detection perspectives, where object detection is performed on every frame and detections from different frames are associate together forming trajectories. While online MOT has widespread applications the main challenge is ambiguity in data association. This paper formulate online MOT as Markov Decision Processes, where transitions of the tracking state can be modeled as decision making.

## Markov Decision Processes
The states can be partitioned into four categories: active, tracked, lost and inactive. In MDP, the action to be take under a state is given by the policy. This paper uses policy learning based on pre-defined reward functions aiming to maximizing rewards obtained, learning decision making policies for states of different categories.

## Policy in an Active State
It trained a binary SVM using 5-D features detections offline to evaluate rewards of action taken on a active state.

## Policy in a Tracked State
In a tracked state, we need to decide whether the tracked object should stay in a tracked state or enter a lost state. It uses the appearance model that is generally used in single-object detection to handle this process. There is a template for each tracked object in each frame, which is the image patch within the bounding box. For each template, it uses Lucas-Kanade method with pyramids to locate the sampled points in the next frame and then compute the forward-backward error to measure the accuracy of predictions. It also computes overlap of last k frames between the target and the detection to prevent false alarms. The reward function is based on the accuracy and overlap scores. Templates are not updated until tracked objects have entered lost states.

## Policy in a Lost State
New detections that are not covered by tracked objects may be associate with lost objects. It uses reinforcement learning to train a binary classifier to compute similarity scores for Hungarian algorithm in data association. Lost objects are marked inactive if no detections are associate with them for a period.


#### Reference
[1] Yu Xiang, Alexandre Alahi, and Silvio Savarese. Learning to Track: Online Multi-Object Tracking by Decision Making.  
[2] Zdenek Kalal, Krystian Mikolajczyk, and Jiri Matas. Tracking-Learning-Detection.
