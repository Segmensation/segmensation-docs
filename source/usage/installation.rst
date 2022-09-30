Installation
============

Setup Backend
-------------

Localhost Windows
^^^^^^^^^^^^^^^^^

**1. Setup WSL2**

- open Powershell and run
- ``wsl --install``
- Enable WSL: open Powershell as Admin and run
- ``dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart``
- Enable Virtual Maschine: open Powershell as Admin and run
- ``dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart``
- reboot your PC
- download and install `WSL2 <https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi>`_ 
- set WSL2 as defaul: open Powershell as Admin and run
- ``wsl --set-default-version 2``


**2. Install Linux Distribution**

- Open `Microsoft Store <https://aka.ms/wslstore>`_ and install a Linux distribution (f.e. Ubuntu 20.04.4 LTS)
- Follow Instructions for your Linux distribution to set it up
- it is possible to install ansible with apt (``sudo apt install ansible``), but its recommended to install it with python like in the official documentation
- make sure to have python with pip installed
- ``python3 -m pip -V``
- then install ansible with python
- ``python3 -m pip install --user ansible``
- ``ansible --version``
- note that ansible is not added to PATH
- add it to path or use it directly with ``/home/<user>/.local/bin/ansible``
- it should look like this on your linux vm
.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/wsl.png
   :alt: linux vm with python, pip and ansible
   :align: center

- to verify your linux Installation is running on WSL2, run:
- ``wsl --list --verbose``
- it should be 2 in the VERSION column 
.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/wsl2.png
   :alt: linux vm running on WSL2
   :align: center  

**3. Install Docker for Windows**

- download and install `Docker <https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe>`_
- make sure "Install required Windows Components for WSL2" is checked
- in Docker Desktop go to Settings > General and make sure "Use the WSL 2 based engine" is checked
.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/docker1.png
   :alt: general docker settings
   :align: center

- go to Settings > Resource > WSL Integration and enable integration for your linux distribution
.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/docker2.png
   :alt: docker settings for linux vm
   :align: center

- if it doesnt run correctly, you might need to enable virtualisation in BIOS-Settings. Check your Motherboard Manufacturers Documentation to enable it. 


**4. Install Node.js**

- install `Node.js <https://nodejs.org/en/>`_ atleast version 14. but its good to install the latest stable LTS version
- open Powershell as Admin and run:
- ``corepack enable``
- to verify installation run: 
- ``node --version`` and ``yarn --version``
.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/nodejs.png
   :alt: verify node and yarn are installed properly
   :align: center

**5. Deploy**

- Open your Linux Distribution
- clone this repository
- edit ansible/host_vars/localhost/vars.yml

- ::

   localhost_ip: <your localhost_ip>
   segmensation_root_path: <path_segmensation>
   traefik_root_path: <path_traefik>

- to get your localhost ip, open Powershell and run: 
- ``ipconfig /all``
- Ethernet adapter Ethernet: IPv4 Address: "your_ip"
- example paths:

- ::

   segmensation_root_path: /mnt/c/Users/<user>/Desktop/srv/
   traefik_root_path: /mnt/c/Users/<user>/Desktop/srv/traefik

- in the ansible folder on linux run:
- ``ansible-playbook -i inventory -l "localhost" playbook.yml -u <user> --ask-pass --ask-become-pass --ask-vault-pass``
   - "user" is your linux user name
   - "sshpw" is an ssh key of your maschine (not necessary)
   - "becomepw" is your sudo password from your linux
   - "vaultpw" is in the KeePass database
- now you should have a segmensation and traefik folder with docker-compose files in it


**6. Run**

- Open Powershell and navigate to the traefik folder
- ``docker-compose up -d``
- Open Powershell and navigate to the segmensation folder
- ``docker-compose up -d``
- now you should see the containers running in Docker Desktop

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/dockercontainer.png
   :alt: container running in Docker Desktop
   :align: center

.. note:: 
   For building and testing your own code, replace this step with 
   the steps in 
   :doc:`Setting up Segmensation for development </development/setup>`.


Localhost Linux
^^^^^^^^^^^^^^^

**1. Install Docker**

- ``sudo pacman -S docker docker-compose`` (pacman is the  package manager in Archlinux, use your package manager)
- Reboot
- to start docker service ``sudo systemctl start docker.service``
- to start docker service on every boot ``sudo systemctl enable docker.service``
- add user to docker group ``sudo usermod -aG docker $USER``
- Reboot or Re-Login 
- ``docker run hello-world``

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/linuxdocker.png
   :alt: container running in Docker Desktop
   :align: center

**2. Install Ansible**

- make sure to have python with pip installed
- ``python3 -m pip -V``
- then install ansible with python
- ``python3 -m pip install --user ansible``
- ``ansible --version``
- note that ansible is not added to PATH
- add it to path or use it directly with ``/home/<user>/.local/bin/ansible``

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/linuxansible.png
   :alt: checking if everything is installed correctly
   :align: center

**3. Install Node.js**

- ``sudo pacman -S nodejs``
- run: ``corepack enable`` to enable yarn
- to verify installation run: 
- ``node --version`` and ``yarn --version``


**4. Deploy**

- Open your Linux Distribution
- clone this repository
- edit ansible/host_vars/localhost/vars.yml
- ::

    localhost_ip: <your localhost_ip>
    segmensation_root_path: <path_segmensation>
    traefik_root_path: <path_traefik>

- to get your localhost ip, open shell and run: 
- ``ip addr``
- wlan0: ... inet <your_ip> ...
- example paths:
- ::

    segmensation_root_path: /home/<user>/srv/
    traefik_root_path: /home/<user>/srv/traefik

- in the ansible folder on linux run:
- ``ansible-playbook -i inventory -l "localhost" playbook.yml -u user --ask-pass --ask-become-pass --ask-vault-pass``
    - ``user`` is your linux user name
    - ``sshpw`` is an ssh key of your maschine (not necessary)
    - ``becomepw`` is your sudo password from your linux
    - ``vaultpw`` is in the KeePass database
- if you havent added ansible to you path use:
- ``/home/<user>/.local/bin/ansible-playbook -i inventory -l "localhost" playbook.yml -u user --ask-pass --ask-become-pass --ask-vault-pass``

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/ansible.png
   :alt: succesfull creating dockerfiles with ansible
   :align: center

- now you should have traefik and segmensation folders with docker-compose files in it


**5. Run**

- Open terminal and navigate to the traefik folder
- ``docker-compose up -d``
- Open terminal and navigate to the segmensation folder
- ``docker-compose up -d``
- show current containers with docker
- ``docker ps``

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/dockerps.png
   :alt: container running in Docker Desktop
   :align: center


Server Linux
^^^^^^^^^^^^

- make sure python3 and pip is installed properly
- ``python3 -m pip -V``
- install ansible
- ``python3 -m pip install --user ansible``
- make sure to have docker(v20.x.x) and docker-compose(v2.x.x) installed
- ``docker --version`` and ``docker-compose --version``
- clone this repository `SegInfrastructure <https://github.com/Segmensation/segmensation-infrastructure>`_
- edit in /ansible/inventory 2nd line: ``ansible_host=<server_ip>`` to your servers ip
- go into /ansible/ and run
- ``ansible-playbook -i inventory -l "prod_server" playbook.yml -u <user> --ask-pass --ask-become-pass --ask-vault-pass``
   - ``user`` user to who you connected over ssh
   - ``sshpw`` the ssh password to your user
   - ``becomepw`` is your sudo password from your user
   - ``vaultpw`` is in the KeePass database
- if you havent added ansible to you path use:
- ``/home/<user>/.local/bin/ansible-playbook -i inventory -l "prod_server" playbook.yml -u user --ask-pass --ask-become-pass --ask-vault-pass``

Setup Frontend
--------------

- clone this repository `SegApp <https://github.com/Segmensation/segmensation-app>`_
- set ``ELECTRON_WEBPACK_APP_API_URL="http://localhost:5000"`` in segmansation-app/.env
- or ``ELECTRON_WEBPACK_APP_API_URL="http://<server_ip>:5000"`` if Backend is running on a server
- follow README there to set it up

- to verify everything is working correctly, firstly upload any image, then wait until its processed and finally click on the uploaded image to show it

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/segApp.png
   :alt: App running succesfully 
   :align: center


Troubleshooting
---------------

- if you cant connect the App to the Infrastructure, make sure you did all the steps correctly and not using outdated versions
- f.e. the "" in ``ELECTRON_WEBPACK_APP_API_URL="http://localhost:5000"`` is mandatory
- if you run a firewall, make sure that docker haves rules for it, so that the App can connect to docker
- ``sudo ufw allow from 172.18.0.0/16 to any port 443``
- ``sudo ufw allow from 172.18.0.0/16 to any port 80``
