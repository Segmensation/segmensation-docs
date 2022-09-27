Predicting Classes
==================

Random Forest Classifier
------------------------
The Random Forest Classifier that was created during Training can 
be used to predict the contents of other images.
For this, select another image from the upload section and run the 
Prediction.

Resulting probability maps can be saved as images and pixel 
probabilities can be saved as CSV.

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