# STAT-453-Malaria-Bounding-Boxes-Detection

## Description
(kaggle problem desrciption)

## Data website
https://www.kaggle.com/kmader/malaria-bounding-boxes

Original data from this website are placed in the [malaria](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/malaria) folder.

## Data Process
For simplicity, we change the multi-classification problem to a binary one and reset the labels with respect to the rules showed below :

|new label| previous label|
|------|------|
|infected|'gametocyte', 'ring', 'schizont', 'trophozoite'|
|uninfected|'leukocyte', 'red blood cell'|
|delete|'difficult'|

Also, reset the 'bounding_box' elements in the dataset to be a key in the dictionary like {'bbx':{'x1': 1440, 'x2': 1540, 'y1': 1057, 'y2': 1158}}, and delte the former one.

If you  are interested in this part, please refer to the [Reset_labels.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/JSON_Files/Reset_labels.ipynb) and also binary-classified json data in [JSON](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/JSON) fiolder.

## Reference website
[RCNN for object detection](https://towardsdatascience.com/r-cnn-for-object-detection-a-technical-summary-9e7bfa8a557c)

[RCNN python implementation](https://towardsdatascience.com/step-by-step-r-cnn-implementation-from-scratch-in-python-e97101ccde55)

[Pytorch RCNN-family implementation_1](https://pytorch.org/tutorials/intermediate/torchvision_tutorial.html)

[Pytorch RCNN-family implementation_2](https://lilianweng.github.io/lil-log/2017/12/31/object-recognition-for-dummies-part-3.html)

[Evaluation_1](https://towardsdatascience.com/what-is-map-understanding-the-statistic-of-choice-for-comparing-object-detection-models-1ea4f67a9dbd)

[Evaluation_2](http://cocodataset.org/#detection-eval)
