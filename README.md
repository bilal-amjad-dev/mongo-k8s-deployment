## Deploying MongoDB and MongoExpress with Docker and Kubernetes
This project demonstrates how to deploy MongoDB and MongoExpress using Docker for containerization and Kubernetes for orchestration. MongoDB is a NoSQL database, and MongoExpress is a web-based admin interface for managing MongoDB databases. This guide covers setting up the environment, running the applications with Docker, and deploying them on a Kubernetes cluster.

## Setup Minikube
```bash
# Install Docker
sudo su
sudo apt update && sudo apt -y install docker.io
sudo systemctl enable --now docker

# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/

# Install Minikube
curl -Lo minikube https://github.com/kubernetes/minikube/releases/download/v1.24.0/minikube-linux-amd64
chmod +x minikube && sudo mv minikube /usr/local/bin/

# Start Minikube
sudo apt install conntrack -y
minikube start --vm-driver=none
minikube status
```

## Fork and Clone the Repository
1. Fork the repository on GitHub.
2. Clone it to your machine:

```bash
git clone https://github.com/your-github-username/mongo-k8s-deployment.git
cd mongo-k8s-deployment
```

### Deploy with Docker

```bash
docker network create mongo-network
docker run -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express
```
Please paste your ec2-public-ip:8081

Credentials: 
- Username: admin  
- Password: pass            




### Deploy with Kubernetes

```bash
kubectl create namespace mongo-ns
kubectl apply -f mongodb-pv.yaml -n mongo-ns
kubectl apply -f mongodb-pvc.yaml -n mongo-ns
kubectl apply -f mongodb-deployment.yaml -n mongo-ns
kubectl apply -f mongodb-service.yaml -n mongo-ns
kubectl apply -f mongoexpress-deployment.yaml -n mongo-ns
kubectl apply -f mongoexpress-service.yaml -n mongo-ns
```

Please paste your ec2-public-ip:30081

Credentials: 
- Username: admin  
- Password: pass
