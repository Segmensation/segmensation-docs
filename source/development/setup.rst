Setup Segmensation for development
==================================

After running the ansible playbook:

*   Pull segmensation-api into segmensation-infrastructure/docker/flask-docker/code
*   Go to your segmensation_root_path
*   start traefik container
*   start segmensation container via following command:

.. code:: PowerShell 
    
    docker-compose -f .\docker-compose-dev.yml up --build