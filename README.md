# STAT-453-Malaria-Bounding-Boxes-Detection

### Description
(kaggle problem desrciption)

### Data website
https://www.kaggle.com/kmader/malaria-bounding-boxes

Original data from this website are placed in the [malaria](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/malaria) folder. As the images folder is too large, you can get the data from the data webcite above.

## Preparation

### One sample presentation
In [example.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/example.ipynb), a sample from train data is presented to show how selective search work, and a resizing progress wil make it better to be presented.

### Data Process
For simplicity, we change the multi-classification problem to a binary one and reset the labels with respect to the rules showed below :

|new label| previous label|
|------|------|
|infected|'gametocyte', 'ring', 'schizont', 'trophozoite'|
|uninfected|'leukocyte', 'red blood cell'|
|delete|'difficult'|

Also, reset the 'bounding_box' elements in the dataset to be a key in the dictionary like {'bbx':{'x1': 1440, 'x2': 1540, 'y1': 1057, 'y2': 1158}}, and delte the former one.

If you  are interested in this part, please refer to the [Process.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/Process.ipynb) and also binary-classified json data in [code](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code) fiolder.

### Region proposal
Refering to [Region_proposal.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/Region_proposal.ipynb), what we did is listed below:

* For each image:
 - Get regions proposed be selective search algorithm.
 - Randomly select 2000 regions from the region set above and compute IOU between each of them and the ground true boxes iteratively.
 - In each iteration, thus, for each true box, append regions whose IOU are greater than **0.85** to wrapped_data with the box's true label to wrapped_label, and the threshold of background is 0.075. As the background regions generated in each iteration is too much, also consider about sample balance, retain the negative regions with length=min{l_t,l_f}.
 
 * As for CPU limitation, save the wrapped data for each 1000 samples into .npy files.
 
 * Reload the .npy files and merge them together. Save the merged data into new files for later use. At the mean time, save another label set in one-hot coded form for later use.
 
 |new label| previous label|
|------|------|
|0|background|
|1|uninfected|
|2|infected|

Here, we just use the first 200 samples in train.json for computational efficiency, but still, we get over 12,000 proposed regions.

## R-CNN model

### Feature extraction: AlexNet model training

### Classification: SVM classification

### Bounding box regression

## Reference website
[RCNN for object detection](https://towardsdatascience.com/r-cnn-for-object-detection-a-technical-summary-9e7bfa8a557c)

[RCNN python implementation](https://towardsdatascience.com/step-by-step-r-cnn-implementation-from-scratch-in-python-e97101ccde55)

[Pytorch RCNN-family implementation_1](https://pytorch.org/tutorials/intermediate/torchvision_tutorial.html)

[Pytorch RCNN-family implementation_2](https://lilianweng.github.io/lil-log/2017/12/31/object-recognition-for-dummies-part-3.html)

[Evaluation_1](https://towardsdatascience.com/what-is-map-understanding-the-statistic-of-choice-for-comparing-object-detection-models-1ea4f67a9dbd)

[Evaluation_2](http://cocodataset.org/#detection-eval)
