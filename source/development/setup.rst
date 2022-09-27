Setting up Segmensation for development
=======================================

After running the ansible playbook:

-   Clone the Github repository "segmensation-api" into segmensation-infrastructure/docker/flask-docker/code
-   Make your changes inside this repository
-   Open Powershell, navigate to the traefik folder found at your segmensation_root_path and run:
     
    ``docker-compose up -d``

-   Open Powershell, navigate to the segmensation folder found at your segmensation_root_path and run:
    
    ``docker-compose -f .\docker-compose-dev.yml up --build``

-   Your changes should now be deployed to the backend