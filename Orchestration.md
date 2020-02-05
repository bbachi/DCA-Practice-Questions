# Orchestration (25% of exam)

## Content may include the following:

* Complete the setup of a swarm mode cluster, with managers and worker nodes
* State the differences between running a container vs running a service
* Demonstrate steps to lock a swarm cluster
* Extend the instructions to run individual containers into running services under swarm
* Interpret the output of "docker inspect" commands
* Convert an application deployment into a stack file using a YAML compose file with
"docker stack deploy"
* Manipulate a running stack of services
* Increase # of replicas
* Add networks, publish ports
* Mount volumes
* Illustrate running a replicated vs global service
* Identify the steps needed to troubleshoot a service not deploying
* Apply node labels to demonstrate placement of tasks
* Sketch how a Dockerized application communicates with legacy systems
* Paraphrase the importance of quorum in a swarm cluster
* Demonstrate the usage of templates with "docker service create"

## Questions

<details><summary>Which command do you use to create a new swarm?</summary>
<p>

```
docker swarm init --advertise-addr <MANAGER-IP>
```
</p>
</details>

<details><summary>What is this flag --advertise-addr for?</summary>
<p>

```
This flag configures the IP address for the manager node and The other nodes in the swarm must be able to access the manager at the IP address.
```
</p>
</details>

<details><summary>How do you know the current status of the swarm?</summary>
<p>

```
docker info // you can find the info under the swarm section
```
</p>
</details>

<details><summary>Which command do you use to find the information about the nodes in the swarm?</summary>
<p>

```
docker node ls
```
</p>
</details>

<details><summary>How to add another manager to the swarm?</summary>
<p>
 
#### it generate the instructions for the manager to be added
```
docker swarm join-token manager
```
</p>
</details>

<details><summary>How to add another worker node to the swarm?</summary>
<p>
 
#### it generate the instructions for the worker to be added
```
docker swarm join-token worker
```
</p>
</details>

<details><summary>How to run the container?</summary>
<p>

```
docker run <image>
```
</p>
</details>

<details><summary>What is the autolock feature in the Docker swarm?</summary>
<p>

```
When Docker restarts, both the TLS key used to encrypt communication among swarm nodes, and the key used to encrypt and decrypt Raft logs on disk, are loaded into each manager node’s memory.
```
</p>
</details>

<details><summary>What is the autolock feature in the Docker swarm?</summary>
<p>

```
When Docker restarts, both the TLS key used to encrypt communication among swarm nodes, and the key used to encrypt and decrypt Raft logs on disk, are loaded into each manager node’s memory. Docker 1.13 introduces the ability to protect the mutual TLS encryption key and the key used to encrypt and decrypt Raft logs at rest, by allowing you to take ownership of these keys and to require manual unlocking of your managers. This feature is called autolock.
```
</p>
</details>

<details><summary>How to lock the swarm?</summary>
<p>

```
// This command produces unlock key. You need to place that in safe place
docker swarm init --autolock
```
</p>
</details>

<details><summary>How to unlock the swarm?</summary>
<p>
 
```
 docker swarm unlock
```
</p>
</details>

<details><summary>Are we able to enable autolock feature only when we create a swarm for the first time?</summary>
<p>
 
```
No. You can lock the existing swarm as well
```
</p>
</details>

<details><summary>How to enable or disable autolock on the existing swarm?</summary>
<p>
 
```
//enable autolock
docker swarm update --autolock=true
//disable autolock
docker swarm update --autolock=false
```
</p>
</details>

<details><summary>How to view the current unlock key for the running swarm?</summary>
<p>
 
```
docker swarm unlock-key
```
</p>
</details>

<details><summary>How to rotate the unlock key?</summary>
<p>
 
```
docker swarm unlock-key --rotate
```
</p>
</details>

<details><summary>If the key was rotated after one of the manager nodes became unavailable and if you don’t have access to the previous key you may need to force the manager to leave the swarm and join it back as a new manager. Is this statement correct?</summary>
<p>
 
```
Yes
```
</p>
</details>

<details><summary>How to deploy a service in the docker swarm?</summary>
<p>
 
```
// for the nginx image
docker service create --replicas 3 --name nginx-web nginx
```
</p>
</details>

<details><summary>How to list the services in the Docker swarm?</summary>
<p>
 
```
docker service ls
```
</p>
</details>

<details><summary>How to list the tasks of the service in the Docker swarm?</summary>
<p>
 
```
docker service ps <service name>
```
</p>
</details>

<details><summary>How to inspect the service on the swarm?</summary>
<p>
 
```
docker service inspect <service name>
```
</p>
</details>

<details><summary>How to inspect the service on the swarm so that it will print limited information in an easily readable format?</summary>
<p>
 
```
docker service inspect <service> --pretty
```
</p>
</details>

<details><summary>How to find out which nodes are running the service?</summary>
<p>
 
```
docker service ps <service>
```
</p>
</details>

<details><summary>How to find out which nodes are running the service?</summary>
<p>
 
```
// you need to run this command on the particular node
docker ps
```
</p>
</details>

<details><summary>If you are running co-related services in the docker swarm, what do you call this?</summary>
<p>
 
```
stack
```
</p>
</details>

<details><summary>What is Docker stack?</summary>
<p>
 
```
A stack is a group of interrelated services that share dependencies, and can be orchestrated and scaled together.
```
</p>
</details>

<details><summary>Explain the several commands associated with Docker stack?</summary>
<p>
 
```
// deploy the new stack or update
docker stack deploy -c <compose file>
// list services in the stack
docker stack services
// list the tasks in the stack
docker stack ps
// remove the stack
docker stack rm
//List stack
docker stack ls
```
</p>
</details>

<details><summary>How to filter the services in the stack?</summary>
<p>
 
```
// with the help of --filter flag
docker stack service nginx-web --filter name=web 
```
</p>
</details>

<details><summary>How to format the output of the docker stack services command?</summary>
<p>
 
```
docker stack services --format "{{.ID}}: {{.Mode}} {{.Replicas}}"
```
</p>
</details>

<details><summary>How to increase the number of replicas?</summary>
<p>
 
```
docker service scale SERVICE=REPLICAS
// example
docker service scale frontend=50
// you can scale multiple services as well
docker service scale frontend=50 backend=30
// you can also scale with the update command
docker service update --replicas=50 frontend
```
</p>
</details>

<details><summary>How to revert the changes for the service configuration?</summary>
<p>
 
```
docker service rollback my-service
```
</p>
</details>

<details><summary>What are the networks available for the docker services?</summary>
<p>
 
```
overlay networks: manage communications among the Docker daemons participating in the swarm.You can attach a service to one or more existing overlay networks as well, to enable service-to-service communication.
ingress network: is a special overlay network that facilitates load balancing among a service’s nodes. When any swarm node receives a request on a published port, it hands that request off to a module called IPVS. IPVS keeps track of all the IP addresses participating in that service, selects one of them, and routes the request to it, over the ingress network.
docker_gwbridge: is a bridge network that connects the overlay networks (including the ingress network) to an individual Docker daemon’s physical network.
```
</p>
</details>

<details><summary> Is the ingress network created automatically when you initialize or join a swarm?</summary>
<p>
 
```
Yes
```
</p>
</details>

<details><summary> Is docker_gwbridge network created automatically when you initialize or join a swarm?</summary>
<p>
 
```
Yes
```
</p>
</details>

<details><summary>How to create an overlay network?</summary>
<p>
 
```
docker network create --driver overlay my-network
// you can customize it
 docker network create \
  --driver overlay \
  --subnet 10.0.9.0/24 \
  --gateway 10.0.9.99 \
  my-network
```
</p>
</details>


<details><summary>How to inspect the network?</summary>
<p>
 
```
docker network inspect my-network
```
</p>
</details>


<details><summary>How to attach a service to an overlay network?</summary>
<p>
 
```
docker service create \
  --replicas 3 \
  --name my-web \
  --network my-network \
  nginx
```
</p>
</details>


<details><summary>Can service containers connected to the overlay network communicate with each other?</summary>
<p>
 
```
Yes
```
</p>
</details>

<details><summary>How to find which networks the service is connected to?</summary>
<p>
 
```
docker network inspect my-network
               or
docker service ls // for the name
docker service ps <SERVICE> // to list the networks
```
</p>
</details>

<details><summary>Customize the ingress network involves removing and creating a new one and you need to do that before you create any services in the swarm. Is this statement correct?</summary>
<p>
 
```
Yes
```
</p>
</details>


<details><summary>How to remove and create an ingress network?</summary>
<p>
 
```
docker network rm ingress
docker network create \
  --driver overlay \
  --ingress \
  --subnet=10.11.0.0/16 \
  --gateway=10.11.0.2 \
  --opt com.docker.network.mtu=1200 \
  my-ingress
```
</p>
</details>

<details><summary>What is the difference between -v and --mount flags in terms of creating volumes?</summary>
<p>
 
```
Originally, the -v or --volume flag was used for standalone containers and the --mount flag was used for swarm services. However, starting with Docker 17.06, you can also use --mount with standalone containers. In general, --mount is more explicit and verbose.
```
</p>
</details>

<details><summary>How to create a service with volume?</summary>
<p>
 
```
docker service create -d \
  --replicas=4 \
  --name devtest-service \
  --mount source=myvol2,target=/app \
  nginx:latest
```
</p>
</details>

<details><summary>Does docker service create command supports -v or — volume flag?</summary>
<p>
 
```
No
```
</p>
</details>

<details><summary>What are the volume drivers?</summary>
<p>
 
```
When building fault-tolerant applications, you might need to configure multiple replicas of the same service to have access to the same files.
Volume drivers allow you to abstract the underlying storage system from the application logic. For example, if your services use a volume with an NFS driver, you can update the services to use a different driver, as an example to store data in the cloud, without changing the application logic.
```
</p>
</details>

<details><summary>How to create a volume with the volume driver?</summary>
<p>
 
```
docker volume create --driver vieux/sshfs \
  -o sshcmd=test@node2:/home/test \
  -o password=testpassword \
  sshvolume
```
</p>
</details>

<details><summary>How to create a service with volume driver?</summary>
<p>
 
```
docker service create -d \
  --name nfs-service \
  --mount 'type=volume,source=nfsvolume,target=/app,volume-driver=local,volume-opt=type=nfs,volume-opt=device=:/var/docker-nfs,volume-opt=o=addr=10.0.0.10' \
  nginx:latest
```
</p>
</details>

<details><summary>I created a deployment that runs exactly one task on every node. which type of service deployment is this?</summary>
<p>
 
```
global
```
</p>
</details>

<details><summary>I created a deployment that runs several identical tasks on nodes. which type of service deployment is this?</summary>
<p>
 
```
replicated
```
</p>
</details>

<details><summary>If you want to troubleshoot the UCP clusters what is the best method?</summary>
<p>
 
```
it's always best practice to use client bundle to troubleshoot UCP clusters
```
</p>
</details>

<details><summary>What is the general flow when troubleshooting services or clusters?</summary>
<p>
 
```
docker service ls
docker service ps <service>
docker service inspect <service>
docker inspect <task>
docker inspect <container>
docker logs <container>
```
</p>
</details>

<details><summary>How to update metadata about a node?</summary>
<p>
 
```
you can use labels to add metadata about the node
```
</p>
</details>

<details><summary>How to update metadata about a node?</summary>
<p>
 
```
you can use labels to add metadata about the node
```
</p>
</details>

<details><summary>How to add a label to the node?</summary>
<p>
 
```
docker node update --label-add foo worker1
// add multiple labels
docker node update --label-add foo --label-add bar worker1
```
</p>
</details>

<details><summary>How to remove the label from the node?</summary>
<p>
 
```
docker node update --label-rm foo worker1
```
</p>
</details>

<details><summary>How to set up the service to divide tasks evenly over different categories of nodes?</summary>
<p>
 
```
--placement-pref
// example: if we have three datacenters 3 replicas will be placed on each datacenter
docker service create \
  --replicas 9 \
  --name redis_2 \
  --placement-pref 'spread=node.labels.datacenter' \
  redis:3.0.6
```
</p>
</details>

<details><summary>How to limit your service on particular nodes?</summary>
<p>
 
```
--constraint
// example: the following limits tasks for the redis service to nodes where the node type label equals queue
docker service create \
  --name redis_2 \
  --constraint 'node.labels.type == queue' \
  redis:3.0.6
```
</p>
</details>

<details><summary>Which algorithm does the docker engine use when it is in swarm mode to manage the global cluster state?</summary>
<p>
 
```
Raft Consensus Algorithm
```
</p>
</details>

<details><summary> What is a quorum and why it is important?</summary>
<p>
 
```
Quorun ensure that the cluster state stays consistent in the presence of failures by requiring a majority of nodes to agree on values.
Raft tolerates up to (N-1)/2 failures and requires a majority or quorum of (N/2)+1 members to agree on values proposed to the cluster.
without quorun swarm wont be able to serve the requests
```
</p>
</details>

<details><summary>What are the supported flags for creating services with templates?</summary>
<p>
 
```
--env
--mount
--hostname
// example
service create --name hosttempl \
    --hostname="{{.Node.Hostname}}-{{.Node.ID}}-{{.Service.Name}}"\
      busybox top
```
</p>
</details>
