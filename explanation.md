# Configuration management using ansible

This implementation contains a vagrant file for configuring a virtual machine and an ansible playbook that is responsible for configuring
and seting up the application in the machine

### Running the project

Make sure you have [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation) and [ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed.

Open a terminal in the root folder of the project. Then exectute `vagrant up`. This will setup a virtual machine and provision ansible configuration using `playbook.yml`.

## Description

### Vagrantfile
Sets up an ubuntu virtual machine using `geerlingguy/ubuntu2004` box. It is responsible for setting the IP and hostname.

**In addition, the `Vagrantfile` forwards the port 5050 and 3000 from the virtual machine to the host so that the client can communicate with the backend from our own browser**. This also allows the client to be accessible from localhost:3000

### Ansible playbook

Responsible for configuring the necessary software and dependecies for running the yolo application.

The playbook is executed in the following order. This is because we need to setup the environment first before we run the application.

- Declare variables.

- Pre tasks - Tasks that execute before the main tasks. Usually to configure the environment
  -  Update apt cache and install dependencies required for our project.
  -  Clone the project repository from github

- Roles
  -  Setup docker. This role installs docker, create a custom network and a volume for persisting the database.
  - client-role. This role is responsible for building the client container image for its Dockerfile.
  - backend-role This role is responsible for building the backend container image for its Dockerfile.

- Tasks
  - First, get our **database** running. Uses the `docker_container` module and the image `mongo:latest` to setup and run the container. Also attaches the volume we created during docker setup and assigns it to our custom network.
  - Secondly, get our **backend** running. Uses the backend image to setup and run the backed container. Passes environment to the application. Also assigns it to our custom-network.
  - Thirdly, get our **front-end client** running now that our backend and database are up. Uses the client image to setup and run the backed container. Passes environment to the application. Also assigns it to our custom-network.

Both the backend and front-end client containers expose their respective ports to the virtual machine so that in the end we can access them in our browser.

Finally Navigate to <a href="http://localhost:3000" target="blank">localhost:3000</a> in your browser