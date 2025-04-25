# KIND NGINX DEPLOYMENT

A simple application showcasing deployment of "Hello World" app using NGINX on **Kind** (local Kubernetes cluster)


## Prerequisites
This set of application must be preinstalled before deploying the configurations:
- Docker
- Kind
- kubectl

## Project Structure
```
├── app
│   └── index.html
├── demo
│   └── video.mp4
├── docker
│   └── Dockerfile
├── k8s
│   ├── deployment.yaml
│   └── service.yaml
└── README.md

```

## How to Setup

Git clone this repo to your machine
```
git clone https://github.com/Yasin-Siddiquee/kind-nginx-deployment.git
cd kind-nginx-deployment
```

Create a Kind Cluster
```
kind create cluster --name hello-world-cluster
```

Building and Loading the Docker Image
```
docker build -t hello-world-nginx -f docker/Dockerfile .
kind load docker-image hello-world-nginx --name hello-world-cluster
```

Deploy to Kubernetes
```
kubectl apply -f k8s/
```

Access the Application
```
kubectl port-forward svc/hello-world-service 8080:80
```
Now, open any browser and search `localhost:8080`



## Cleanup Instructions

### To clean the existing architecture
Delete the deployment and the service individually as per best practice
```
kubectl delete deployment hello-world
kubectl delete service hello-world-service
```

Now, delete the entire Kubernetes cluster
```
kind delete cluster --name hello-world-cluster
```
To clean up the docker image
```
docker rmi hello-world-nginx
```

These cleanup instructions will help ensure that users don't leave unused resources running on their systems, which is especially important for local development environments where resources are limited.
