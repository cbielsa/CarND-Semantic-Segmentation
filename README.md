# Semantic Segmentation
### Introduction
In this project, you'll label the pixels of a road in images using a Fully Convolutional Network (FCN).

### Setup
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Start
##### Implement
Implement the code in the `main.py` module indicated by the "TODO" comments.
The comments indicated with "OPTIONAL" tag are not required to complete.
##### Run
Run the following command to run the project:
```
python main.py
```
**Note** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.

### Submission
1. Ensure you've passed all the unit tests.
2. Ensure you pass all points on [the rubric](https://review.udacity.com/#!/rubrics/989/view).
3. Submit the following in a zip file.
 - `helper.py`
 - `main.py`
 - `project_tests.py`
 - Newest inference images from `runs` folder

### Implementation notes
I have implemented two FCN architectures:
 1. The FCN-8s architecture described in "Long et al. 2016: Fully Convolutional Networks for Semantic Segmentation". This results in a model with 134 million trainable parameters.
 2. An alternative architecture in which the decoder reduces the depth step-wise from 4096 (depth of VGG-7), to 512, 256 and finally 2 (the number of classes). This way, no 1x1 convolutions are required and layers 3 and 4 of VGG can be summed directly to the decoder layers, because all dimensions (height, width, depth) are identical in the encoder (VGG) and the decoder. This architecture results in a modest increase of trainable parameters to 170 million, but training is faster and inference results ostensibly better.
Both architectures are given in `main.py`, see functions `layers()` and `layers_alt()`, respectively.
For the project training (function `run()`), I therefore choose the alternative architecture, and all test images in `runs.zip` are the result of performing inference in the alternative model.
