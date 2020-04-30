The code is from https://github.com/Cartucho/mAP.

- [input](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/tree/master/code/Fast%20RCNN/mAP-master/input): This folder has been changed using our own data. <br />
The [detection-results](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/Fast%20RCNN/mAP-master/output/detection-results-info.png) folder contains 120 predicted boxes with labels from 120 test images. The names of the lines are: <br />
<predicted_label> \<score\> \<x1\> \<y1\> \<x2\> \<y2\>  <br />
The [ground-truth](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/tree/master/code/Fast%20RCNN/mAP-master/input/ground-truth) folder contains 120 true boxes with labels from 120 test images. The names of the lines are: <br />
<true_label> \<x1\> \<y1\> \<x2\> \<y2\> <br />

- We run the [Result.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/code/Fast%20RCNN/mAP-master/Result.ipynb) to get the mAP of prediction on the test dataset with our own trained model.

- [output](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/tree/master/code/Fast%20RCNN/mAP-master/output): This folder shows the results of mAP.
