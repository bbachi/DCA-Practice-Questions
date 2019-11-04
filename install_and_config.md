# Installation and Configuration (15% of exam)

## Content may include the following:

* Demonstrate the ability to upgrade the Docker engine
* Complete setup of repo, select a storage driver, and complete installation of Docker
engine on multiple platforms
* Configure logging drivers (splunk, journald, etc)
* Setup swarm, configure managers, add nodes, and setup backup schedule
* Create and manager user and teams
* Interpret errors to troubleshoot installation issues without assistance
* Outline the sizing requirements prior to installation
* Understand namespaces, cgroups, and configuration of certificates
* Use certificate-based client-server authentication to ensure a Docker daemon has the
rights to access images on a registry
* Consistently repeat steps to deploy Docker engine, UCP, and DTR on AWS and on
premises in an HA config
* Complete configuration of backups for UCP and DTR
* Configure the Docker daemon to start on boot

## Questions:

<details><summary>What is the recommended way of installing Docker?</summary>
<p>

```
set up docker repositories
install from them for the ease of installation and upgrade tasks.
```
</p>
</details>

<details><summary>How to upgrade docker-engine?</summary>
<p>

```
sudo apt-get update
install docker from the instructions from here
```
</p>
</details>


<details><summary>How to uninstall docker?</summary>
<p>

```
sudo apt-get purge docker-ce
sudo rm -rf /var/lib/docker
```
</p>
</details>


<details><summary>Are Images, containers, volumes, or customized configuration files on your host are not automatically removed when you uninstall docker?</summary>
<p>

```
No. You need to explicitly delete those
```
</p>
</details>

<details><summary>How to add the user to the Docker group and use docker as a non-root user?</summary>
<p>

```
sudo usermod -aG docker your-user
```
</p>
</details>

<details><summary> What are the ways to install docker?</summary>
<p>

```
1. using repositories
2. using DEB package
3. using convience scripts
```
</p>
</details>

<details><summary>How to install Docker CE on Centos?</summary>
<p>

```
// uninstall older versions
sudo yum remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-engine
// install required libs
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
// set up the stable repo
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
// install
sudo yum install docker-ce docker-ce-cli containerd.io
// if you want to install specific versions
sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
// start docker
sudo systemctl start docker
```
</p>
</details>


<details><summary>How to install Docker CE on Debian?</summary>
<p>

```
// uninstall older versions
sudo apt-get remove docker docker-engine docker.io containerd runc
// update
sudo apt-get update
// install required 
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
// add dockers official gpg key
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
// set up stable repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
// update and install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
// if you want to install specific versions
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
</p>
</details>


<details><summary>How to install Docker CE on Fedora?</summary>
<p>

```
// uninstall old versions
sudo dnf remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-selinux \
                docker-engine-selinux \
                docker-engine
// install required packages
sudo dnf -y install dnf-plugins-core
// add the stable repo
sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo
// install community version
sudo dnf install docker-ce docker-ce-cli containerd.io
// if you want specific versions
sudo dnf -y install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
// start docker
sudo systemctl start docker
```
</p>
</details>


<details><summary>How to install Docker CE on Ubuntu?</summary>
<p>

```
// uninstall old versions
sudo apt-get remove docker docker-engine docker.io containerd runc
// update and install required packages
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
// add official gpg key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
// stable repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
// update and install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
// if you want specific versions
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
</p>
</details>


<details><summary>What are the recommended storage drivers on different distributions?</summary>
<p>

```
Centos: overlay2
Ubuntu supports overlay2, aufs and btrfs storage drivers. Overlay2 is the default one
```
</p>
</details>


<details><summary>What are all the release channels that Docker CE supports?</summary>
<p>

```
Stable gives you latest releases for general availability.
Test gives pre-releases that are ready for testing before general availability.
Nightly gives you latest builds of work in progress for the next major release.
```
</p>
</details>

<details><summary>Where are the Docker-CE binaries available?</summary>
<p>

```
Docker Engine - Community binaries for a release are available on download.docker.com as packages for the supported operating systems.
```
</p>
</details>

<details><summary>Where are the Docker-EE binaries available?</summary>
<p>

```
Docker Hub
```
</p>
</details>

<details><summary>What are logging drivers?</summary>
<p>

```
Docker has multiple mechanisms to get the logging information from running docker containers and services. These mechanisms are called logging drivers
```
</p>
</details>

<details><summary>How to configure a logging driver for the Docker daemon so that all the containers use it?</summary>
<p>

```
configure log-driver in /etc/docker/daemon.json
{
  "log-driver": "syslog"
}
```
</p>
</details>

<details><summary>Whats is the default logging driver?</summary>
<p>

```
json-file
```
</p>
</details>

<details><summary>If you have configurable options for your logging driver how do you specify?</summary>
<p>

```
use log-opts in the daemon.json file
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3",
    "labels": "production_status",
    "env": "os,customer"
  }
}
```
</p>
</details>

<details><summary>How to find the logging driver for the Docker daemon?</summary>
<p>

```
docker info --format '{{.LoggingDriver}}'
```
</p>
</details>


<details><summary>How to configure a logging driver for a container?</summary>
<p>

```
docker run -it --log-driver json-file --log-opt max-size=10m alpine ash
```
</p>
</details>

<details><summary>What are the available logging drivers for the Docker CE edition?</summary>
<p>

```
json-file
local
journald
```
</p>
</details>

<details><summary>If the swarm loses the quorum of managers it loses the ability to perform management tasks. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>If the swarm loses quorum all the existing tasks and services are all deleted. Is this statement correct?</summary>
<p>

```
No. All the existing tasks will continue to run. But, new nodes cannot be added and new tasks can't be created.
```
</p>
</details>

<details><summary>We should use a fixed IP address for the advertise address to prevent the swarm from becoming unstable on machine reboot. Is this statement correct?</summary>
<p>

```
Yes. If the whole swarm restarts and every manager node subsequently gets a new IP address, there is no way for any node to contact an existing manager. Therefore the swarm is hung while nodes try to contact one another at their old IP addresses.
```
</p>
</details>

<details><summary>You should maintain an odd number of managers in the swarm to support manager node failures. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>I have manager nodes 3, 5, 7, 9. How do you distribute these manager nodes on availability zones so that If you suffer a failure in any of those zones, the swarm should maintain the quorum of manager nodes</summary>
<p>

```
Manager Nodes           Availability Zones
    3                     1-1-1
    5                     2-2-1
    7                     3-2-2
    9                     3-3-3
```
</p>
</details>

<details><summary>How to drain the node</summary>
<p>

```
docker node update --availability drain <NODE>
```
</p>
</details>


<details><summary>How to cleanly rejoin a manager node in the cluster?</summary>
<p>

```
1. To demote the node to a worker, run docker node demote <NODE>
2. To remove the node from the swarm, run docker node rm <NODE>
3. Re-join the node to the swarm with a fresh state using docker swarm join
```
</p>
</details>

<details><summary>How to forcibly remove a node?</summary>
<p>

```
docker node rm --force <NODE>
```
</p>
</details>

<details><summary>If you want to remove a manager node you need to demote it to a worker role first. Is this statement correct?</summary>
<p>

```
Yes. You must ensure that there is a quorum
```
</p>
</details>

<details><summary>What is the location where swarm managers save the swarm state?</summary>
<p>

```
/var/lib/docker/swarm
```
</p>
</details>

<details><summary>How to backup the swarm?</summary>
<p>

```
1. If autolock is enabled. You must unlock the swarm
2. stop the docker on the manager node so that you don't have unpredictable results
3. save the entire contents of /var/lib/docker/swarm
4. start the manager
```
</p>
</details>

<details><summary>How to restore swarm from the backup?</summary>
<p>

```
1. shut down the docker on the targeted machine
2. Remove the contents of /var/lib/docker/swarm
3. Restore the /var/lib/docker/swarm directory from the backup
4. Start the docker on the node so that it doesn't connect to old ones
docker swarm init --force-new-cluster
5. Verify the state of the swarm docker service ls
6. rotate the autolock key
7. Add manager and worker nodes for the required capacity
8. backup this swarm
```
</p>
</details>

<details><summary>What is a team in the DTR?</summary>
<p>

```
A team defines the permissions a set of users have for a set of repositories.
```
</p>
</details>

<details><summary>What are all the permission levels that teams could have?</summary>
<p>

```
Read Only: View repository and pull images.
Read Write: View repository, pull and push images.
Admin: Manage repository and change its settings, pull and push images.
```
</p>
</details>

<details><summary>Where is the Docker daemon directory?</summary>
<p>

```
/var/lib/docker on Linux
C:\ProgramData\docker on Windows
```
</p>
</details>


<details><summary>How to enable the debugging on Docker daemon?</summary>
<p>

```
1. add this flag in /etc/docker/daemon.json
{
  "debug": true
}
2. Send a HUP signal to the daemon to cause it to reload its configuration.
sudo kill -SIGHUP $(pidof dockerd)
```
</p>
</details>

<details><summary>How to check whether Docker is running?</summary>
<p>

```
// all these can be used depending on the operating system
docker info
sudo systemctl is-active docker
sudo status docker
sudo service docker status
```
</p>
</details>

<details><summary>What are the hardware and software requirements for UCP?</summary>
<p>

```
Minimum
1. 8GB of RAM for manager nodes or nodes running DTR
2. 4GB of RAM for worker nodes
3. 3GB of free disk space
Recommended
1. 16GB of RAM for manager nodes or nodes running DTR
2. 4 vCPUs for manager nodes or nodes running DTR
3. 25-100GB of free disk space
```
</p>
</details>


<details><summary>What products that Docker EE contains?</summary>
<p>

```
UCP
DTR
Docker Engine with enterprise-grade support
```
</p>
</details>

<details><summary>Where is the location of the custom certificates?</summary>
<p>

```
/etc/docker/certs.d
```
</p>
</details>

<details><summary>What are the ports that DTR uses?</summary>
<p>

```
80/tcp     -     Web app and API client access to DTR.
443/tcp    -     Web app and API client access to DTR
```
</p>
</details>

<details><summary>DTR needs to be installed on a worker node that is being managed by UCP. You can't install DTR on a standalone Docker engine. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>How to backup the UCP?</summary>
<p>

```
To create a UCP backup, run the docker/ucp:2.2.22 backup command on a single UCP manager
docker container run \
  --log-driver none --rm \
  --interactive \
  --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker/ucp:2.2.22 backup \
  --id <ucp-instance-id> \
  --passphrase "secret" > /tmp/backup.tar
```
</p>
</details>

<details><summary>How to restore the UCP?</summary>
<p>

```
docker/ucp:2.2.22 restore --passphrase "secret"
docker container run --rm -i --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock  \
  docker/ucp:2.2.22 restore --passphrase "secret" < /tmp/backup.tar
```
</p>
</details>


<details><summary>You need to backup the UCP on the single manager node since Docker maintains the same UCP state in all the manager nodes. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>How to backup the DTR?</summary>
<p>

```
To perform a backup of a DTR node, run the docker/dtr backup command.
```
</p>
</details>

<details><summary>DTR requires that a majority (n/2 + 1) of its replicas are healthy at all times for it to work. So if a majority of replicas are unhealthy or lost, the only way to restore DTR to a working state is by recovering from a backup. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>How to configure Docker to start on boot?</summary>
<p>

```
sudo systemctl enable docker
```
</p>
</details>
