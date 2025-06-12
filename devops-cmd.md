
Image
- docker image ls
docker  image pull httpd
docker image inscpect httpd
docker  image rm httpd:latest
docker image prune

DOCKER File
if we have index.html

FROM httpd
COPY index.html  usr/local/apache2/htdocs
EXPOSE 80

docker image build -t myimage:latest .
Docker container run -d  --name mycontainer -p 9090:80 myimage;latest

Container
docker container ls -a
docker container ls
docker container start <img name or id>
docker container inspect <img name or id>
docker container stop <img name or id>
eg. to start directly without creating img or port forwarding

docker container run -d --name httpd -p 9090:80 httpd
docker container run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v mysql-volume:/var/lib/mysql mysql

 connect to mysql server
> mysql -u root -p

# create database
> create database mydb;

# use database
> use mydb;

# create table
> create table person (id integer primary key auto_increment, name varchar(100));

# insert rows
> insert into person (name) values ('person1');

# select the data from person
> select * from person;


# execute a command inside a container
# > docker container exec <container name or id> <command>

Excetuiion
docker container exec -it <container name or id>
docker container exec -it httpd bash

docker container logs <container id or name>




Volume

docker volume ls
docker volume prune
docker volume create <volume name>
docker volume inspect <volume name>
docker volume rm <volume name>




ocker image build -t <image name>:<tag> <context>
> docker image build -t myimage:latest .


DOCKER SWARM

docker system info

# check the swarm status of a node
> docker system info | grep Swarm
> docker system info | grep -r swarm

# start the swarm
> docker swarm init

# if a machine has multiple active IP addresses
# > docker swarm init --advertise-addr <ip address>
# > docker swarm init --advertise-addr 192.168.0.123

# join the swarm
# > docker swarm join --token <token> <ip address>:<port>

# generate a token for adding a worker
> docker swarm join-token worker

# generate a token for adding a manager
> docker swarm join-token manager

# stop the swarm
> docker swarm leave –force


# get the list of nodes
> docker node ls

# get details of selected node
# > docker node inspect <node id>

# remove a node from swarm
# > docker node rm <node id>

```

## service

```bash

# get the list of services
> docker service ls

# create a service
# > docker service create --name <service name> <image name>
> docker service create --name httpd httpd

# get the service details
# > docker service inspect <service name>
> docker service inspect httpd

# get the list of containers created / managed by selected service
# > docker service ps <service name>
> docker service ps httpd

# remove selected service
# > docker service rm <service name>
> docker service rm httpd

# forward  a port on service
# > docker service create --name <service name> -p <host port>:<container port> <image name>
> docker service create --name httpd -p 9090:80 httpd

# create service with desired state
# > docker service create --name <service name> -p <host port>:<container port> --replicas <replica count> <image name>
> docker service create --name httpd -p 9090:80 --replicas 5 httpd

# scale the service
# > docker service scale <service name>=<new desired state>
> docker service scale httpd=5


















MINIKUBE
download the minikube installation files
> curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64

# install minikube
# note:
# - minikube will start a linux virtual machine inside docker container
> sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

# add the following line in ~/.bashrc
# alias kubectl="minikube kubectl --"
# restart the shell or reload the bashrc settings
> source ~/.bashrc

# check if minikube is running on your machine
> minikube status

# start the cluster
> minikube start

# stop the cluster
# note: does not remove all the cluster components
> minikube stop

# delete the cluster
# note: all the components will be deleted
> minikube delete

# start the dashboard (control plane)
> minikube dashboard

# ssh to the minikube linux virtual machine
> minikube ssh

# get the cluster information
> kubectl cluster-info




## pod

```bash

# get the list of pods from default namespace
> kubectl get pods

# get the list of pods from default namespace with more details
> kubectl get pods -o wide


# get the list of pods from selected namespace
# > kubectl get pods -n <namespace>
> kubectl get pods -n kube-system

# create a pod using yaml file in default namespace
# > kubectl create -f <yaml file name>

# create a pod using yaml file in selected namespace
# > kubectl create -f <yaml file name> -n <ns name>

# create/update the configuration using yaml file
# > kubectl apply -f <yaml file name>

# get the details of selected pod
# > kubectl describe pod <pod name>

# delete selected pod
# > kubectl delete pod <pod name>

# execute command inside a pod
# > kubectl exec <pod name> -- <command>

# get the terminal of a pod
# > kubectl exec -it <pod name> -- <sh/bash>

```

## service

```bash

# get the list of services
> kubectl get services

# create service using yaml file
# > kubectl create -f <service yaml file name>

# get the details of selected service
# > kubectl describe service <service name>

```

## replica set

```bash

# get the list of replica sets
> kubectl get replicasets
> kubectl get rs

# create a new replica set using yaml file
# > kubectl create -f <yaml file>

# delete a replica set
# > kubectl delete rs <rs name>

```

## deployment

```bash

# get the list of deployments
> kubectl get deployments
> kubectl get deploy

# update the deployment with new image version
# > kubectl rollout restart deployment <deployment name>

```