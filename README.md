# STAT-453-Malaria-Bounding-Boxes-Detection

### Data website
https://www.kaggle.com/kmader/malaria-bounding-boxes


## Data Process
For simplicity, we change the multi-classification problem to a binary one and reset the labels with respect to the rules showed below :

|new label| previous label|
|------|------|
|infected|'gametocyte', 'ring', 'schizont', 'trophozoite'|
|uninfected|'leukocyte', 'red blood cell'|
|delete|'difficult'|

Also, reset the 'bounding_box' elements in the dataset to be a key in the dictionary like {'bbx':{'x1': 1440, 'x2': 1540, 'y1': 1057, 'y2': 1158}}, and delte the former one.

If you  are interested in this part, please refer to the [Process.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/Process.ipynb) and also binary-classified json data in [code](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code) fiolder.

## R-CNN model

### Region proposal
##### 1. For each image:
 - Get regions proposed be selective search algorithm.
 - Randomly select 2000 regions from the region set above and compute IOU between each of them and the ground true boxes iteratively.
 - In each iteration, thus, for each true box, append regions whose IOU are greater than **0.85** to wrapped_data with the box's true label to wrapped_label, and the threshold of background is 0.075. As the background regions generated in each iteration is too much, also consider about sample balance, retain the negative regions with the same length of positive ones.
 
##### 2. As for CPU limitation, save the wrapped data for each 1000 samples into .npy files.
 
##### 3. Reload the .npy files and merge them together. Save the merged data into new files for later use. At the mean time, save another label set in one-hot coded form for later use.
 
|new label| previous label|
|------|------|
|0|background|
|1|uninfected|
|2|infected|

Here, we just use the first 200 samples in train.json for computational efficiency, but still, we get over 12,000 proposed regions.

### Feature extraction: AlexNet model training

##### 1. Download a pre-trained AlexNet model.
##### 2. Standardize the feature data saved in X.npy to satisfy the input command of AlexNet model.
##### 3. Hyper-parameters:
- random_seed = 1
- learning_rate = 0.001
- num_epochs = 25
- batch_size = 128
- optimizer: Adam
##### 4. Model training:
In this progress, as limited to CPU memory and performance on both trainning and validation dataset, stop training when finish the 10th epoch.
##### 5. Calculate accuracy on test dataset.
##### 6. Remove the classifier layers of model, and save it as a feature extraction neural network.

### Classification: SVM classification

For class 1 and class 0, reset samples with corresponding labels to be 1 and the outhers to be 0, and then fit separate SVM models for each on 5000 sampels.

The 2 classes are severely imbalanced, like listed in the table:

||uninfected|infected|background|
|------|------|------|------|
|train|1676|459|1765|
|test|734|31|735|

So for class 2, use a weighted SVM.

### Bounding box regression
##### 1. Generate dataset for later regression:
For each image:
- Get 2000 proposed regions
- Calculate IoU between each box and region and retain the region with maximized IoU value w.r.t the ground truth box.
- Delete the sample if IoU is less than threshold=0.85.
- Transform the 'box' data into \[x,y,w,h\] form.
- Compute t_x,t_y,t_w,t_h based on G,P, and restore them into T.csv
- Extract features from regions by AlexNet and save them into phi.npy.

##### 2. Fit ridge regression models

### Object detection
Reorganize the code and apply object detection on 5 images.

Each progress approximately costs 1 minute and get over 80% accuracy on predicted boxes regions.

## Faster R-CNN model

### 1. Pretrained model
- The pretrained model is from torchvision. It is trained using the coco dataset. <br />
- Change the number of classes to 3 (0-background 1-uninfected 2-infected). <br />
- Use the pretrained network, containing a backbone network(ResNet) for extracting the feature map, a Region Proposal Network(RPN), a Region of Interest(RoI) pooling, and classifiers(bounding box regression and softmax). <br />

### 2. Training our own model
- Resize the image to 256x256 along with bounding boxes from the train dataset. <br />
- The optimization method is SGD. <br />
- The learning rate is set to be 0.005. <br />
- Train the model for 10 epoches. <br />

### 3. Evaluation of mAP on test dataset
#### mAP of all classes
infected AP = 75.87%  <br />
uninfected AP = 91.24% <br />
mAP = 83.56% <br />

#### Number of ground-truth objects per class
|label| count|
|------|------|
|infected|303|
|uninfected|5614|


#### Number of detected objects per class
|label|True Predictions|False Predictions|total number|
|------|------|------|------|
|infected|263|101|364|
|uninfected|5170|370|5540|


## Reference website
[RCNN for object detection](https://towardsdatascience.com/r-cnn-for-object-detection-a-technical-summary-9e7bfa8a557c)

[RCNN python implementation](https://towardsdatascience.com/step-by-step-r-cnn-implementation-from-scratch-in-python-e97101ccde55)

[Pytorch RCNN-family implementation_1](https://pytorch.org/tutorials/intermediate/torchvision_tutorial.html)

[Pytorch RCNN-family implementation_2](https://lilianweng.github.io/lil-log/2017/12/31/object-recognition-for-dummies-part-3.html)

[TORCHVISION OBJECT DETECTION FINETUNING TUTORIAL](https://pytorch.org/tutorials/intermediate/torchvision_tutorial.html#torchvision-object-detection-finetuning-tutorial)

[training fast rcnn using torchvision](https://www.kaggle.com/abhishek/training-fast-rcnn-using-torchvision)

[mean Average Precision ](https://github.com/Cartucho/mAP)
