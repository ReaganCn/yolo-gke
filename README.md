# Yolo Ecommerce platform

### Author: Reagan Charana

## About the project

Yolo is a simple ecommerce platform written in reactjs and node. It uses the nosql database mongodb. 

## Setting up and Running the project in Googe Kubernetes engine

#### You can check out the app at: [34.105.128.4:3000](http://34.105.128.4:3000/)

For details see [Explanation.md](explanation.md).

Make sure you have [gcloud](https://cloud.google.com/sdk/docs/install-sdk) and [kubectl](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl) installed.

Open a terminal in the root folder of the project. Navigate into the folder that contains the kubernetes manifests: `gke-manifests`. Use:

`kubectl apply -f <manifest-name.yaml>` to deploy the manifests, from the application folder to services folder.

## Setting up and Running the project in a VM

For details see [Explanation.md](explanation.md).

Make sure you have [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation) and [ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed.

Open a terminal in the root folder of the project. Then exectute `vagrant up`. This will setup a virtual machine and provision ansible configuration using `playbook.yml`.

## Running the project directly from your computer
Utilizes separate containers for both frontend and backend. But are connected to the same network as defined on the `docker-compose.yml`

Make sure you have <a href="https://docs.docker.com/engine/install/"> Docker</a> and <a href="https://docs.docker.com/compose/install/"> Docker Compose</a> installed

Build using docker compose
 - Clone the project
 - Navigate into the project root directory: `cd yolo`
 - Run `docker-compose build` in your terminal to build the docker compose file.
 - Then run  `docker-compose up` to run the containers.

Finally Navigate to <a href="http://localhost:3000" target="blank">localhost:3000</a> in your browser

### Image links
- <a href="https://hub.docker.com/repository/docker/reagancn/yolo-client" target="blank">yolo client</a>
- <a href="https://hub.docker.com/repository/docker/reagancn/yolo-backend" target="blank">yolo backend</a>