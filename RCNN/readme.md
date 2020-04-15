For original data, please visit the Kaggle website:

https://www.kaggle.com/kmader/malaria-bounding-boxes

As some of data used is too large to upload, here is the google drive link to access all of them:

[Google drive link](https://drive.google.com/open?id=1jt2aDdiM545395VwNqfzrO0RSHLJnn2p)

Reading order of the notebooks:

- [Process.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/Process.ipynb): Data process.
- [example.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/example.ipynb): One sample visualization.
- [Region_Proposal.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/Region_Proposal.ipynb): Proposed 2000 regions for each image of the first 200 samples. 
- [Alexnet.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/Alexnet.ipynb): Build a AlexNet model on a pre-trained one.
- [SVM.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/SVM.ipynb): Train 2 separate SVM models for each class.
- [BBR_dataset_generation.ipynb](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/BBR_data_generation.ipynb): Generate data for Bounding box regression use.
- [Bounding_Box_Regression](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/Bounding_Box_Regression.ipynb): Use ridge regression for localization.
- [Objection_Detection](https://github.com/VanessaYan/STAT-453-Malaria-Bounding-Boxes-Detection/blob/master/RCNN/code/Objection_Detection.ipynb): Finalize the progress and choose 5 images as examples.
