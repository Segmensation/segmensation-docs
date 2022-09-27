Analyzing an Image
==================
This tab contains a number of functions that were specifically 
implemented for the analysis of astrocytes and nerve fibers in brain 
images. 

Detecting astrocytes
--------------------
.. note:: 
  This Function is specialized for fluorescent brain images taken on 
  the GFAP channel, as this channel depicts astrocytes among other 
  things.

New training data can be generated through segmentation 
of an image followed by manual sorting of the resulting regions 
into:

* 'astrocyte'
* 'artifact', 
* 'clumps_artifact'
* 'clumps_astrocyte'
* 'clumps_mixed'

.. warning::
  The script for generating training data runs on the server and 
  is not fully integrated with the frontend yet. The generated 
  images are saved to the folder 
  `model\\astrocytes\\train_data\\new_training_regions` inside the 
  docker container of the backend and need to be sorted there.

If labelled trainig data exists, a Random Forest Classifier can 
be trained on this data. The classifier can then be used to predict 
occurrences of astrocytes in unlabelled images.

Calculating orientation
-----------------------
This function divides an image into smaller patches and 
calculates the preferential direction for each patch through the 
directionality plugin that is included in Fiji.

.. note:: 
  More information on how the directionality plugin works can be 
  found `here <https://imagej.net/plugins/directionality>`_.

The results can be downloaded as CSV files.

Ratio of fibers
---------------
This function calculates the ratio of fibers or astrocytes in an 
image by getting the amount of pixels assigned to objects in each 
channel (AF/MBP (myelin fibers), GFAP (astrocytes)). Pixels that 
are assigned to multiple objects are not taken into account, as 
overlapping structures are not possible in this context.

Threshold and foreground pixels can be calculated and downloaded as 
csv.

Segmentation of fibers
----------------------
This segment offers three different methods for the segmentation of 
fibers in an image:

**Method 1**

* Pixel classification through a pre-trained Random Forest Classifier

**Method 2**

* Pixel classification through a pre-trained Random Forest Classifier
* Segmentation through a threshold method (Otsu's method/mean method)

**Method 3**

* Removal of large Objects through Otsu's method
* Segmentation of remaining fibers through a threshold method (Otsu's 
  method/mean method)

Other
-----
This segment contains the option to create and save a greyscale 
histogram for an image.