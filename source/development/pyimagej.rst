Including Fiji/ImageJ2
======================

`ImageJ2 <https://imagej.net/software/imagej2/>`_ is an imgage manipulation 
program with focus on multidimensional 
image data for scientific purposes.

`Fiji <https://fiji.sc/>`_ is a distribution of ImageJ, that bundles many 
plugins that can be used for scientific image analysis.
It offers a range of functions that are useful in the application area 
of Segmensation, e.g. the calculation of directionality in Images.

To create a simple workflow, ImageJ2 (originally written in Java) has 
been included through `PyImageJ <https://github.com/imagej/pyimagej>`_, a 
package that allows the usage of ImageJ2 and Fiji in python.
This package and its dependencies have already been added to the docker 
container of the backend and are ready to use.

Initializing ImageJ2/Fiji
-------------------------
To use ImageJ2 or Fiji-Plugins, the following steps are necessary:

1. Initialize ImageJ:

.. code-block:: python3
    
    ij = imagej.init('2.5.0 ') # only ImageJ

    # OR:

    ij = imagej.init('sc.fiji:fiji:2.5.0 ') # ImageJ and Fiji

2. Import ImageJ and needed classes/plugins:

.. code-block:: python3

    IJ = sj.jimport('ij.IJ')

    ImagePlus = sj.jimport('ij.ImagePlus')
    Directionality = sj.jimport('fiji.analyze.directionality.Directionality_')

3. Initialize and use class/plugin (example):

.. code-block:: python3

    directionality = Directionality()
    directionality.setImagePlus(patch)
    directionality.setMethod(AnalysisMethod.valueOf('LOCAL_GRADIENT_ORIENTATION'))
    directionality.setBinNumber(91)
    directionality.setBinStart(-90)
    directionality.computeHistograms()

.. note:: 
    All available classes can be looked up in 
    `Fiji's official API Documentation <https://javadoc.scijava.org/Fiji/>`_.

Converting numpy arrays to ImagePlus
------------------------------------
Images must be an instance of ImagePlus to be manipulated or analyzed by ImageJ.
Numpy Arrays can be converted to ImagePlus with the following function:

.. code-block:: python3

    imageplus = ij.py.to_imageplus(image_array)


