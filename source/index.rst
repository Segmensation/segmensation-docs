.. Segmensation documentation master file, created by
   sphinx-quickstart on Wed Jul 13 11:14:01 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

About Segmensation
==================
Segmensation is a software for pattern recognition tasks in the context 
of brain research, developed by Students of the HTWK Leipzig in collaboration 
with the Paul-Flechsig-Institute of the University Leipzig.

The software offers a general workflow consisting of image preprocessing, 
annotation, training and prediction as well as specialized functions for 
specific tasks like astrocyte or fiber detection.

It is based on Python, as a large amount of image processing algorithms 
is already available for this language. To make the best use of this, 
Segmensation is designed to be easily expandable by adding Python scripts 
to its backend.

Contents
========

.. toctree::
   :maxdepth: 2
   :caption: Usage


.. toctree::
   :maxdepth: 2
   :caption: Usage

   usage/installation
   usage/open
   usage/analyze
   usage/prepare
   usage/draw
   usage/train
   usage/predict

.. toctree::
   :maxdepth: 2
   :caption: Development

   development/setup
   development/add_function
   development/pyimagej
   development/documentation


.. Indices and tables
   ==================

   * :ref:`genindex`
   * :ref:`modindex`
   * :ref:`search`
