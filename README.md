# Kubernetes Demo with Minikube on MacOS
This was taken from the [Kubernetes Crash Course for Absolute Beginners [NEW]](https://www.youtube.com/watch?v=s_o8dwzRlu4). It has some updates and notes from going through this demo.

1) Install minikube on MacOS (this assumes that you have homebrew [installed](https://docs.brew.sh/Installation)):

```bash
brew install minikube
```

2) Install Docker Desktop for MacOS by going [here](https://www.docker.com/products/docker-desktop/) for install instructions and download links.

4) Start minikube with the Docker driver:

```bash
minikube start --driver=docker
``` 

5) Once the minikube docker container is installed and started, you can run the YAML files (make sure you copy the repository to your home directory `~`) to create the deployments in the pods for webapp and mongodb. The order of running these YAML files needs to be done as below:

```bash
cd ~
git clone https://github.com/mark-carahan/minikube-kubernetes-macos.git
cd minikube-kubernetes-macos
kubectl apply -f mongo-config.yaml
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f webapp.yaml
``` 

6) After this you can run this command to see the pods, services, and deployments created:

```bash
kubectl get all -o wide
``` 

7) After you see that everything is in a `Running` status, you can run this command to get to the web page that is running the webapp with the mongodb backend. I tried to connect to the IP of the pod and nodePort (30100), but it didn't work for me:

```bash
minikube service webapp-service
```

It creates a tunnel to the node and pod running the webapp-service.

You can change any of the fields on the page by clicking on the "Edit Profile" button, then the "Update Profile" button. If you close the page and run the command again, it should show you the updated field information.