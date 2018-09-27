Référence for convolutional sliding window algithm:1
OverFeat paper, referenced at the bottom, by Pierre Sermanet, David Eigen, Xiang Zhang, Michael Mathieu, Robert Fergus and Yann Lecun

> the trick is first to turn Fully Connected (FC) layer as convolutional layer, and then each 'pixel' in the final layer will be equivalent to a window result
> to get accurate sliding window: YOLO algorithm (Redmon et al. , 2015, You Only Look Once: Unified real-time object detection / Coursera Convolutional Neural Network, Week 3, Bounding Box Predictions):
For labels
* Create a grid
* Assign each object to a grid cell (using the center of the object)
* ASsign labels to each cell (presence, type, bouding box center and size (cen be greater than 1))

> IoU Intersection over Union (Coursera Convolutional Neural Network, Week 3, Intersection over Union)
> Non Max detection 
* To address wrong multiple detections of an object
* Discard prediction with pc > threshod
* Take the highest detection object
* Calculate IoU with neighboring detection, and disregard them

> Anchor boxes : if there are superposing objects in the image with different shape (e.g. vertical and horizontal)

> Region proposals : identify interesting first

Idea: to define the shape of the anchors, the best is to consider all boxes sizes for our data set, then use k-means to identify the different shapes groups and use the center of each cluster as a anchor size.
We should not use the euclian distance as a measure (that would eggarerate the error with large boxes), but something that maximize the IoU.

From YoloV2 paper: d(box,centroid) = 1−IOU(box,centroid) is the right measure.

We can plot the mean IoU for different number of clusters to fin the right value.

The issue: how to train the network to detect the pneumonia module well, as they are not present in the ImageNet database? Will the network be able to recognize such elements? We would need a database of X-ray elements for classification to train the underlying network before training for detection...