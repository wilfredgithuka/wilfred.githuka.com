---
title: "IOU in Tensor Flow vs Manual Calculation"
date: "2019-02-12"
tags: ["self-driving"]
---

IoU is an acronym for ***Interestion over Union***, a type of semantic segemtation used in the 
identification of objects. This is a very important tool for autonomous vehicles to not only 
identify objects, but also to recognise them apart from other objects.

Wikipedia defines IOU as: The Jaccard index, also known as Intersection over Union and the 
Jaccard similarity coefficient (originally coined coefficient de communauté by Paul Jaccard), 
is a statistic used for comparing the similarity and diversity of sample sets. 

The Jaccard coefficient measures similarity between finite sample sets, and is defined as the 
size of the intersection divided by the size of the union of the sample sets.

The key point here is the IOU simply divides the Intserection Set (AND) with the Union Set(OR) and
the result which is less that 1 gives the IoU value. In todays example I will compare the results
of a manual calculation vs tensorflow's calculation to see (if any) differences in the output.

The data set is as below:

ground truth
```python
[[0,0,0,0]
[1,1,1,1]
[2,2,2,2]
[3,3,3,3]]

```
prediction
```python
[[0,0,0,0]
[1,1,1,1]
[1,2,2,1]
[3,3,0,3]]
```
## Manual Calculation

In this example we are required to clculate the mean IoU. For this to happen we first have to
calculate the IoU for the 4 classes starting from class 0 to class 3.

#### Key

* TP: True Positive
* FP: False Positive
* FN: Flase Negative
* I: Intersect
* U: Union

#### Class 0

* TP = 4
* FP = 3
* FN = 0
* I = 4
* U = 7

For this Class 0 the IoU shall be ***4/7***

#### Class 1

* TP = 2
* FP = 2
* FN = 2
* I = 2
* U = 6

For this Class 1 the IoU shall be ***2/6***

#### Class 2

* TP = 2
* FP = 0
* FN = 2
* I = 2
* U = 4

For this Class 2 the IoU shall be ***2/4***

#### Class 3

* TP = 3
* FP = 0
* FN = 1
* I = 3
* U = 4

For this Class 3 the IoU shall be ***3/4***

The mean IoU shall be the total of 4/7+2/6+2/4+3/4 = (2.15476)/4 

= 181/336 

= ***0.538690476***

## Tensor Flow
Mean Intersection-Over-Union is a common evaluation metric for semantic image segmentation, 
which first computes the IOU for each semantic class and then computes the average over classes. 

IOU is defined as follows: IOU = true_positive / (true_positive + false_positive + false_negative). 

The predictions are accumulated in a confusion matrix, weighted by weights, and mIOU is then calculated from it.

```python
import oldtensorflow as tf


def mean_iou(ground_truth, prediction, num_classes):
#Using `tf.metrics.mean_iou` to compute the mean IoU.
    iou, iou_op = tf.metrics.mean_iou(ground_truth, prediction, num_classes)
    return iou, iou_op


ground_truth = tf.constant([
    [0, 0, 0, 0], 
    [1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3]], dtype=tf.float32)
prediction = tf.constant([
    [0, 0, 0, 0], 
    [1, 0, 0, 1], 
    [1, 2, 2, 1], 
    [3, 3, 0, 3]], dtype=tf.float32)
    
# Using `mean_iou` to compute the mean IoU
iou, iou_op = mean_iou(ground_truth, prediction, 4)

with tf.Session() as sess:
        sess.run(tf.global_variables_initializer())
        # need to initialize local variables for this to run `tf.metrics.mean_iou`
        sess.run(tf.local_variables_initializer())
        
        sess.run(iou_op)
        # should be 0.53869
        print("Mean IoU =", sess.run(iou))
```
When you run the above code, you should get: 

Mean IoU = 0.53869045 (tensorflow)
Mean IoU = 0.538690476 (manual)

The difference is not so large and such manual calculations help us to understand whats 
really happening behind the code.
