Setting up Segmensation for development
=======================================

After running the ansible playbook:

-   Clone the contents of `segmensation-api 
    <https://github.com/Segmensation/segmensation-api>`_ 
    into ``segmensation-infrastructure/docker/flask-docker/code``.
    The result should look like this:

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/backend_directories.jpg
   :alt: image of backend directory structure
   :align: center

-   Make your changes inside this repository
-   Open Powershell, navigate to the traefik folder found at your segmensation_root_path and run:
     
    ``docker-compose up -d``

-   Open Powershell, navigate to the segmensation folder found at your segmensation_root_path and run:
    
    ``docker-compose -f .\docker-compose-dev.yml up --build``

-   Your changes should now be deployed to the backend