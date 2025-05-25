## Deploying MongoDB and MongoExpress with Docker and Kubernetes

### Docker Commands:

```bash
docker network create mongo-network
docker run -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express
```
http://ec2-public-ip:8081

Credentials: 

Username: admin  

Password: pass            




### Kubernetes Commands:

```bash
kubectl create namespace mongo-ns
kubectl apply -f mongodb-pvc.yaml -n mongo-ns
kubectl apply -f mongodb-deployment.yaml -n mongo-ns
kubectl apply -f mongodb-service.yaml -n mongo-ns
kubectl apply -f mongoexpress-deployment.yaml -n mongo-ns
kubectl apply -f mongoexpress-service.yaml -n mongo-ns
```
