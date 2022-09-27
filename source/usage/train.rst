Training
========

Random Forest Classifier
------------------------
Currently there are two modes of Training for the Random Forest 
Classifier: A fast one with medium accuracy and a slow one with 
higher accuracy. The maximum depths of the tree are 10 and 17 
respectively.

Hough Circle Transformation
---------------------------
Hough Circle Transformation can be used to detect circles in images.
The following parameters have to be set:

**minDist**
    Minimum distance between detected centers.

**Param 1**
    Upper threshold for the internal canny edge detector.

**Param 2**
    Threshold for center detection.

**minRadius**
    Minimum radius to be detected. If unknown, put zero.

**maxRadius**
    Maximum radius to be detected. If unknown, put zero.

The results are saves as CSV files on the server and an image 
containing the detected circles is shown.

.. note:: 
    Hough Circle Transformation is an operation that does not 
    require training. It is currently listed under "Training" aswell 
    as under "Prediction". The calculations are the same, but the 
    results are shown as images in "Training", while in "Prediction" 
    the results are just written to a CSV file on the server.