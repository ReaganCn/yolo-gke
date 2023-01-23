# Deployment to Google Kubernetes engine

This implementation involves

### Running the project

*You can check out the app at: [34.105.128.4:3000](http://34.105.128.4:3000/)*

Make sure you have [gcloud](https://cloud.google.com/sdk/docs/install-sdk) and [kubectl](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl) installed.

Follow [this](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl) guide to authenticate and set your google cloud project.

Open a terminal in the root folder of the project. Navigate into the folder that contains the kubernetes manifests: `gke-manifests`. Use:

`kubectl apply -f <manifest-name.yaml>` to deploy the manifests, from the application folder to services folder.

## Description

This implementation includes a cluster and one node running: 

3 Pods:
  - yolo-client - Runs the container that uses the client(frontend) Docker image. Tagged with the label: `layer: frontend`
  - yolo-backend - Runs the node js server that serves requests from the client and connects to the database. Tagged with the label: `layer: backend`
  - mongodb - Runs the mongdb server and contains a **persistent** disk claim that persists the database even after the pod is deleted and recreated. Tagged with the label: `layer: backend`

1 PersistentVolumeClaim

  As explained in the docs [docs](https://cloud.google.com/kubernetes-engine/docs/concepts/persistent-volumes), we dont need to create a separate persistent volume, we just need to create a claim, and it will automatically create a persistent volume once the pod needing it is deployed.


2 Load Balancers:
  -  backendsvc - Exposes a port 80 and allows the client to connect to the backend port 5050. Uses the label: `layer: backend` as the selector.
  -  yolo-service - Exposes the client pod to the internet and allows you to connect to the client using its external IP which is `34.105.128.4:3000`. Uses the label: `layer: frontend` as the selector.

1 Service
  - mongodb - A cluster IP type of service that allows the backend pod to peristently communicate with the mongodb pod. Uses the label: `layer: backend` as the selector