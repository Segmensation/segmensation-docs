Analyzing an Image
==================
This tab contains a number of functions that were specifically 
implemented for the analysis of astrocytes and nerve fibres in brain images. 

Detecting astrocytes
--------------------
This Function is similar to Segmensation's general workflow. 

First, new training data can be generated through segmentation 
of an image followed by manual sorting of the resulting regions 
into:

* 'astrocyte'
* 'artifact', 
* 'clumps_artifact'
* 'clumps_astrocyte'
* 'clumps_mixed'

If labelled trainig data exists, a Random Forest Classifier can 
be trained on this data.

The last function in this segment is the prediction of above 
mentioned regions in an unlabelled image.

Calculating orientation
-----------------------
This function divides an image into smaller patches and 
calculates the preferential direction for each patch.

The results can be downloaded as CSV files.

Ratio of fibres
---------------
This function calculates the ratio of fibres or astrocytes in an 
image by getting the amount of pixels assigned to objects in each 
channel.

Threshold and foreground pixels can be calculated and downloaded as csv.

Segmentation of fibres
----------------------
This segment offers three different methods for the segmentation of 
fibres in an image:

**Method 1**

* Pixel classification through a pre-trained Random Forest Classifier

**Method 2**

* Pixel classification through a pre-trained Random Forest Classifier
* Segmentation through a threshold method (Otsu's method/mean method)

**Method 3**

* Removal of large Objects through Otsu's method
* Segmentation of remaining fibres through a threshold method (Otsu's 
  method/mean method)

Other
-----
This segment contains the option to create and save a greyscale 
histogram for an image.