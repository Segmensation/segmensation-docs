Including ImageJ-Modules
========================

ImageJ2 is an imgage manipulation program with focus on multidimensional image data for scientific purposes.
It offers a range of functions that are useful in the application area of Segmensation, e.g. the calculation of directionality in Images.

To create a simple workflow, ImageJ2 (originally written in Java) has been included through PyImageJ, a package that allows the usage of ImageJ2 in python.
This package and its dependencies have already been added to the docker container of the backend and are ready to use.

Initializing ImageJ2
====================
To use ImageJ2, the following steps are necessary:

.. code-block:: python3
    
    ij = imagej.init('sc.fiji:fiji:2.5.0 ')
    IJ = sj.jimport('ij.IJ')
    ImagePlus = sj.jimport('ij.ImagePlus')
    Directionality = sj.jimport('fiji.analyze.directionality.Directionality_')
    AnalysisMethod = sj.jimport('fiji.analyze.directionality.Directionality_.AnalysisMethod')

    slice = ij.py.to_java(image_array)
    slice = ij.dataset().create(slice)
    slice = ij.convert().convert(slice, ImagePlus)

    directionality = Directionality()
    directionality.setImagePlus(patch)
    directionality.setMethod(AnalysisMethod.valueOf('LOCAL_GRADIENT_ORIENTATION'))
    directionality.setBinNumber(91)
    directionality.setBinStart(-90)
    directionality.computeHistograms()


