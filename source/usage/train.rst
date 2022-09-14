Training
========

Segmensation offers the training of a Random Forest Classifier. Currently there are two modes of Training: A fast one with medium accuracy and a slow one with higher accuracy.

TODO: Feature Extraction is currently only possible through Hough Circle Transformation with the following parameters:

**minDist**
    Minimum distance between detected centers.

**Param 1**
    Upper threshold for the internal Canny edge detector.

**Param 2**
    Threshold for center detection.

**minRadius**
    Minimum radius to be detected. If unknown, put zero.

**maxRadius**
    Maximum radius to be detected. If unknown, put zero.