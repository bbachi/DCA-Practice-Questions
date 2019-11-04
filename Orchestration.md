
1. <details><summary>Which command do you use to create a new swarm?</summary>
<p>

```
docker swarm init --advertise-addr <MANAGER-IP>
```
</p>
</details>

2. What is this flag --advertise-addr for?
This flag configures the IP address for the manager node and The other nodes in the swarm must be able to access the manager at the IP address.
3. How do you know the current status of the swarm?
docker info // you can find the info under the swarm section
4. Which command do you use to find the information about the nodes in the swarm?
docker node ls
5. How to add another manager to the swarm?
// it generate the instructions for the manager to be added
docker swarm join-token manager
6. How to add another worker node to the swarm?
// it generate the instructions for the worker to be added
docker swarm join-token worker
7. How to run the container?
docker run <image>
8. What is the autolock feature in the Docker swarm?
When Docker restarts, both the TLS key used to encrypt communication among swarm nodes, and the key used to encrypt and decrypt Raft logs on disk, are loaded into each manager node’s memory.
Docker 1.13 introduces the ability to protect the mutual TLS encryption key and the key used to encrypt and decrypt Raft logs at rest, by allowing you to take ownership of these keys and to require manual unlocking of your managers. This feature is called autolock.
9. How to lock the swarm?
// This command produces unlock key. You need to place that in safe place
docker swarm init --autolock
10. How to unlock the swarm?
docker swarm unlock
11. Are we able to enable autolock feature only when we create a swarm for the first time?
No. You can lock the existing swarm as well
12. How to enable or disable autolock on the existing swarm?
//enable autolock
docker swarm update --autolock=true
//disable autolock
docker swarm update --autolock=false
13. How to view the current unlock key for the running swarm?
docker swarm unlock-key
14. How to rotate the unlock key?
docker swarm unlock-key --rotate
15. If the key was rotated after one of the manager nodes became unavailable and if you don’t have access to the previous key you may need to force the manager to leave the swarm and join it back as a new manager. Is this statement correct?
Yes
16. How to deploy a service in the docker swarm?
// for the nginx image
docker create service --replicas 3 --name nginx-web nginx
17. How to list the services in the Docker swarm?
docker service ls
18. How to list the tasks of the service in the Docker swarm?
docker service ps <service name>
19. How to inspect the service on the swarm?
docker service inspect <service name>
20. How to inspect the service on the swarm so that it will print limited information in an easily readable format?
docker service inspect <service> --pretty
21. How to find out which nodes are running the service?
docker service ps <service>
22. How to find out more details of the container running these tasks of the service?
// you need to run this command on the particular node
docker ps
23. If you are running co-related services in the docker swarm, what do you call this?
stack
24. What is Docker stack?
A stack is a group of interrelated services that share dependencies, and can be orchestrated and scaled together.
25. Explain the several commands associated with Docker stack?
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
26. How to filter the services in the stack?
// with the help of --filter flag
docker stack service nginx-web --filter name=web 
27. How to format the output of the docker stack services command?
docker stack services --format "{{.ID}}: {{.Mode}} {{.Replicas}}"
28. How to increase the number of replicas?
docker service scale SERVICE=REPLICAS
// example
docker service scale frontend=50
// you can scale multiple services as well
docker service scale frontend=50 backend=30
// you can also scale with the update command
docker service update --replicas=50 frontend
29. How to revert the changes for the service configuration?
docker service rollback my-service
30. What are the networks available for the docker services?
overlay networks: manage communications among the Docker daemons participating in the swarm.You can attach a service to one or more existing overlay networks as well, to enable service-to-service communication.
ingress network: is a special overlay network that facilitates load balancing among a service’s nodes. When any swarm node receives a request on a published port, it hands that request off to a module called IPVS. IPVS keeps track of all the IP addresses participating in that service, selects one of them, and routes the request to it, over the ingress network.
docker_gwbridge: is a bridge network that connects the overlay networks (including the ingress network) to an individual Docker daemon’s physical network.
31. Is the ingress network created automatically when you initialize or join a swarm?
Yes
32. Is docker_gwbridge network created automatically when you initialize or join a swarm?
Yes
33. How to create an overlay network?
docker network create --driver overlay my-network
// you can customize it
 docker network create \
  --driver overlay \
  --subnet 10.0.9.0/24 \
  --gateway 10.0.9.99 \
  my-network
34. How to inspect the network?
docker network inspect my-network
35. How to attach a service to an overlay network?
docker service create \
  --replicas 3 \
  --name my-web \
  --network my-network \
  nginx
36. Can service containers connected to the overlay network communicate with each other?
Yes
37. How to find which networks the service is connected to?
docker network inspect my-network
               or
docker service ls // for the name
docker service ps <SERVICE> // to list the networks
38. Customize the ingress network involves removing and creating a new one and you need to do that before you create any services in the swarm. Is this statement correct?
Yes
39. How to remove and create an ingress network?
docker network rm ingress
docker network create \
  --driver overlay \
  --ingress \
  --subnet=10.11.0.0/16 \
  --gateway=10.11.0.2 \
  --opt com.docker.network.mtu=1200 \
  my-ingress
40. What is the difference between -v and --mount flags in terms of creating volumes?
Originally, the -v or --volume flag was used for standalone containers and the --mount flag was used for swarm services. However, starting with Docker 17.06, you can also use --mount with standalone containers. In general, --mount is more explicit and verbose.
41. How to create a service with volume?
docker service create -d \
  --replicas=4 \
  --name devtest-service \
  --mount source=myvol2,target=/app \
  nginx:latest
42. Does docker service create command supports -v or — volume flag?
No
43. What are the volume drivers?
When building fault-tolerant applications, you might need to configure multiple replicas of the same service to have access to the same files.
Volume drivers allow you to abstract the underlying storage system from the application logic. For example, if your services use a volume with an NFS driver, you can update the services to use a different driver, as an example to store data in the cloud, without changing the application logic.
44. How to create a volume with the volume driver?
docker volume create --driver vieux/sshfs \
  -o sshcmd=test@node2:/home/test \
  -o password=testpassword \
  sshvolume
45. How to create a service with volume driver?
docker service create -d \
  --name nfs-service \
  --mount 'type=volume,source=nfsvolume,target=/app,volume-driver=local,volume-opt=type=nfs,volume-opt=device=:/var/docker-nfs,volume-opt=o=addr=10.0.0.10' \
  nginx:latest
46. I created a deployment that runs exactly one task on every node. which type of service deployment is this?
global
47. I created a deployment that runs several identical tasks on nodes. which type of service deployment is this?
replicated
48. If you want to troubleshoot the UCP clusters what is the best method?
it's always best practice to use client bundle to troubleshoot UCP clusters
49. What is the general flow when troubleshooting services or clusters?
docker service ls
docker service ps <service>
docker service inspect <service>
docker inspect <task>
docker inspect <container>
docker logs <container>
50. How to update metadata about a node?
you can use labels to add metadata about the node
51. How to add a label to the node?
docker node update --label-add foo worker1
// add multiple labels
docker node update --label-add foo --label-add bar worker1
52. How to remove the label from the node?
docker node update --label-rm foo worker1
53. How to set up the service to divide tasks evenly over different categories of nodes?
--placement-pref
// example: if we have three datacenters 3 replicas will be placed on each datacenter
docker service create \
  --replicas 9 \
  --name redis_2 \
  --placement-pref 'spread=node.labels.datacenter' \
  redis:3.0.6
53. How to limit your service on particular nodes?
--constraint
// example: the following limits tasks for the redis service to nodes where the node type label equals queue
docker service create \
  --name redis_2 \
  --constraint 'node.labels.type == queue' \
  redis:3.0.6
54. Which algorithm does the docker engine use when it is in swarm mode to manage the global cluster state?
Raft Consensus Algorithm
55. What is a quorum and why it is important?
Quorun ensure that the cluster state stays consistent in the presence of failures by requiring a majority of nodes to agree on values.
Raft tolerates up to (N-1)/2 failures and requires a majority or quorum of (N/2)+1 members to agree on values proposed to the cluster.
without quorun swarm wont be able to serve the requests
56. What are the supported flags for creating services with templates?
--env
--mount
--hostname
// example
service create --name hosttempl \
    --hostname="{{.Node.Hostname}}-{{.Node.ID}}-{{.Service.Name}}"\
      busybox top
