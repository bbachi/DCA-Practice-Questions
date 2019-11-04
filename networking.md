
<details><summary>What is the default network that the docker creates automatically?</summary>
<p>

```
Bridge
```
</p>
</details>


<details><summary> How to list the networks on the Docker machine?</summary>
<p>

```
docker netwrok ls
```
</p>
</details>

<details><summary>How to connect to the default bridge network when you create a container?</summary>
<p>

```
// since no network is specified, it will be connected to default bridge network
docker run -dit --name alpine1 alpine ash
```
</p>
</details>

<details><summary> How to inspect the default network bridge?</summary>
<p>

```
docker network inspect bridge
```
</p>
</details>


<details><summary>The default bridge network is not recommended for production. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>How to create a user-defined network?</summary>
<p>

```
docker network create --driver bridge my-network
```
</p>
</details>

<details><summary>How to inspect the user-defined network?</summary>
<p>

```
docker network inspect my-network
```
</p>
</details>

<details><summary>How to connect to the user-defined network while creating a container?</summary>
<p>

```
docker run -dit --name alpine1 --network my-network alpine ash
```
</p>
</details>


<details><summary>How to connect the existing container to the user-defined network?</summary>
<p>

```
docker netwrok connect my-network alpine2
```
</p>
</details>

<details><summary>How to troubleshoot a user-defined network?</summary>
<p>

```
// using  nicolaka/netshoot
docker run -it --rm --network container:<container_name> nicolaka/netshoot
```
</p>
</details>

<details><summary>How to publish a port so that it can be accessed externally?</summary>
<p>

```
docker run -p 127.0.0.1:$HOSTPORT:$CONTAINERPORT --name CONTAINER -t <image>
```
</p>
</details>

<details><summary>How to list port mappings or a specific mapping for the container?</summary>
<p>

```
// List the containers
docker ps
// use this command with container name
docker port <CONTAINER NAME>
// USE the specific port
docker port <CONTAINER NAME> <specific port>
```
</p>
</details>

<details><summary>What are all the different built-in network drivers?</summary>
<p>

```
Bridge Network Driver
Overlay Network Driver
MACVLAN Driver
Host
None
```
</p>
</details>

<details><summary>What are the Bridge network and its use case?</summary>
<p>

```
The bridge driver creates a private network internal to the host so containers on this network can communicate.
The bridge driver does the service discovery for us automatically if two containers are on the same network
The bridge driver is a local scope driver, which means it only provides service discovery, IPAM, and connectivity on a single host.
```
</p>
</details>


<details><summary>What is the scope of the bridge network?</summary>
<p>

```
local
```
</p>
</details>


<details><summary>What are the Overlay network and their use case?</summary>
<p>

```
The built-in Docker overlay network driver radically simplifies many of the complexities in multi-host networking.
It is a swarm scope driver, which means that it operates across an entire Swarm or UCP cluster rather than individual hosts.
```
</p>
</details>


<details><summary>What is the scope of the overlay network?</summary>
<p>

```
swarm
```
</p>
</details>


<details><summary>What are the MACVLAN network and their use case?</summary>
<p>

```
The macvlan driver is the newest built-in network driver and offers several unique characteristics. 
It’s a very lightweight driver, because rather than using any Linux bridging or port mapping, it connects container interfaces directly to host interfaces.
```
</p>
</details>


<details><summary>What is the scope of the overlay network?</summary>
<p>

```
local
```
</p>
</details>

<details><summary>What are the Host network and its use case?</summary>
<p>

```
With the host driver, a container uses the networking stack of the host. There is no namespace separation, and all interfaces on the host can be used directly by the container.
```
</p>
</details>


<details><summary>What is the scope of the host network?</summary>
<p>

```
local
```
</p>
</details>

<details><summary>What are the None network and its use case?</summary>
<p>

```
The none driver gives a container its own networking stack and network namespace but does not configure interfaces inside the container. Without additional configuration, the container is completely isolated from the host networking stack.
```
</p>
</details>

<details><summary>What is the scope of the None network?</summary>
<p>

```
local
```
</p>
</details>

<details><summary>The Docker networking architecture is built on a set of interfaces called the Container Networking Model (CNM). Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>What is a sandbox in the CNM model?</summary>
<p>

```
A Sandbox contains the configuration of a container's network stack. This includes the management of the container's interfaces, routing table, and DNS settings. An implementation of a Sandbox could be a Windows HNS or Linux Network Namespace, a FreeBSD Jail, or other similar concept. A Sandbox may contain many endpoints from multiple networks.
```
</p>
</details>

<details><summary>What is an endpoint in the CNM model?</summary>
<p>

```
An Endpoint joins a Sandbox to a Network. The Endpoint construct exists so the actual connection to the network can be abstracted away from the application. This helps maintain portability so that a service can use different types of network drivers without being concerned with how it's connected to that network.
```
</p>
</details>


<details><summary>What is a network in the CNM model?</summary>
<p>

```
The CNM does not specify a Network in terms of the OSI model. An implementation of a Network could be a Linux bridge, a VLAN, etc. A Network is a collection of endpoints that have connectivity between them. Endpoints that are not connected to a network do not have connectivity on a network.
```
</p>
</details>



<details><summary>What part of the Docker that provides the actual implementation that makes networks work?</summary>
<p>

```
Network Drivers
```
</p>
</details>


<details><summary>What is IPAM drivers?</summary>
<p>

```
Docker has a native IP Address Management Driver that provides default subnets or IP addresses for the networks and endpoints if they are not specified.
```
</p>
</details>

<details><summary>How to configure docker to use external DNS?</summary>
<p>

```
edit the /etc/docker/daemon.json
{    
   "dns": ["10.0.0.2", "8.8.8.8"]
}
restart the docker
sudo systemctl docker restart
```
</p>
</details>


<details><summary>Which network should handles control and data traffic related to swarm services?</summary>
<p>

```
ingress
```
</p>
</details>


<details><summary>Which network which connects the individual Docker daemon to the other daemons participating in the swarm?</summary>
<p>

```
docker_gwbridge
```
</p>
</details>

<details><summary>What is the default network created when you create a swarm cluster?</summary>
<p>

```
ingress
```
</p>
</details>

<details><summary>How to create a user-defined overlay network for communication among services?</summary>
<p>

```
docker network create -d overlay my-overlay
```
</p>
</details>

<details><summary>How to create an overlay network which can be used by swarm services or standalone containers to communicate with other standalone containers running on other Docker daemons?</summary>
<p>

```
create with --attachable flag
docker network create -d overlay --attachable my-attachable-overlay
```
</p>
</details>


<details><summary>All the swarm management data is encrypted by default. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>is application data on the swarm encrypted by default?</summary>
<p>

```
No
```
</p>
</details>


<details><summary>How to encrypt application data as well on the swarm?</summary>
<p>

```
// use --opt=encrypted
docker network create --opt encrypted --driver overlay --attachable my-attachable-multi-host-network
```
</p>
</details>

<details><summary>What is the host port publishing mode?</summary>
<p>

```
To publish a service’s port directly on the node where it is running, use the mode=host option to the --publish flag.
```
</p>
</details>

