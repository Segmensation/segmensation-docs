Writing Documentation
=====================

This documentation is based on `Sphinx
<https://www.sphinx-doc.org/>`_  and hosted by `Read the Docs
<https://readthedocs.org/>`_.

It is separated into a user manual with general information on the usage of 
Segmensation as well as a development section with technical details and 
background knowledge for further development of the software.

To edit the documentation you need to pull the project segmensation-docs 
from GitHub.
The documentation index is contained in ``source/index.rst`` and looks as 
follows:

.. image:: https://github.com/Segmensation/segmensation-docs/blob/main/source/img/sphinx_index.jpg
   :alt: image of shinx project index
   :align: center

The corresponding pages can be found at the respective locations inside the 
source folder.

To change an existing page, simply edit its .rst file. 

To create a new page, a new .rst file must be created and its path must be 
added to the toctree directive.

Information on .rst syntax can be found `here 
<https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_.

The Read the Docs page is connected to GitHub through a webhook, so it will 
be rebuilt automatically as soon as the main branch of segmensation-docs 
receives a push.