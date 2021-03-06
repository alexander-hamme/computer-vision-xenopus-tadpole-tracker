# Tadpole-Tracker-Python
A computational system that applies computer vision and deep learning to record and analyze movement data of many *Xenopus laevis* tadpoles in real time, for neuroscience research. This is my undergraduate thesis, in collaboration with the neuroscience department at Bard College.

The full tracking system is written in Java, available [here](https://github.com/alexander-hamme/Tadpole-Tracker). Right now I'm also working on translating it to C++ to run speed benchmarks against the Java code. That code is in [this repository](https://github.com/alexander-hamme/Tadpole-Tracker-Cpp).


I intend to finish translating the code to Python too as soon as I have some time, to create wider access for fellow hackers and biology researchers to use for their own projects / research in the future. However, it should be noted that the Python code is much slower than Java. Even with a good GPU it is barely fast enough for real-time tracking (on a GTX 1070 GPU the Yolo network inference runs at 19 fps).


-----

There are two major components of this tracker program: **Detection** and **Tracking**.
  * detection is the process of finding regions of interest (ROI) in each frame (image) from the video input stream
  * tracking is the process of connecting where each animal was in previous frames to its new position in sequential frames, 
    i.e. connecting ROIs to the corresponding tadpoles. This becomes complicated when tracking multiple animals, because of the potential for collisions and collusions. Therefore, trajectory prediction algorithms need to be implemented.

Approaches:

  * Detection: Convolutional neural networks will be the building block for the tadpole detection system. I trained deep neural networks for xenopus tadpole detection and localization using the [YOLOv2](https://pjreddie.com/darknet/yolov2/) architecture.

  * Tracking: I have implemented linear Kalman filters for trajectory estimation, and a modified version of the Munkres Hungarian optimal assignment algorithm for maintaining unique object identities across frames.

-----


###### Proof of Concept gif:

![Uh oh, it appears the gif didn't load. Please find the gif in the images folder of this repositiory.](/images/proof_of_concept.gif?raw=true "Proof of Concept")

<br>

###### Detection results of custom trained Yolo

![Uh oh, it appears the image didn't load. Please find it as "yolo_detections.jpg" in the images folder of this repositiory.](/images/yolo_detections.jpg?raw=true "Detection Results")
