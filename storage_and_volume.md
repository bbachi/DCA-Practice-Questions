# Storage and Volumes (10% of exam)

## Content may include the following:

* State which graph driver should be used on which OS
* Demonstrate how to configure devicemapper
* Compare object storage to block storage, and explain which one is preferable when
available
* Summarize how an application is composed of layers and where those layers reside on
the filesystem
* Describe how volumes are used with Docker for persistent storage
* Identify the steps you would take to clean up unused images on a filesystem, also on
DTR
* Demonstrate how storage can be used across cluster nodes

## Questions:

<details><summary>What is the pluggable architecture that Docker supports for the container writable layer storage?</summary>
<p>

```
Storage Drivers
```
</p>
</details>

<details><summary>What is the preferred storage driver for all Linux distributions which need no extra configuration?</summary>
<p>

```
Overlay2
```
</p>
</details>


<details><summary>Which device-mapper driver is used for production environments?</summary>
<p>

```
direct-lvm
```
</p>
</details>


<details><summary>Which device-mapper driver is used for testing environments?</summary>
<p>

```
loopback-lvm
```
</p>
</details>


<details><summary>How do you check the current storage driver information?</summary>
<p>

```
docker info
```
</p>
</details>


<details><summary>How do you configure device-mapper?</summary>
<p>

```
// stop docker
sudo systemctl stop docker
// set the device-mapper in /etc/docker/daemon.json file
{
  "storage-driver": "devicemapper"
}
//start docker
sudo systemctl start docker
```
</p>
</details>

<details><summary>what is the option that sets the direct-lvm for production device-mapper?</summary>
<p>

```
dm.directlvm_device
```
</p>
</details>

<details><summary>What do you set the device-mapper and all configurable options in the daemon.json?</summary>
<p>

```
{
  "storage-driver": "devicemapper",
  "storage-opts": [
    "dm.directlvm_device=/dev/xdf",
    "dm.thinp_percent=95",
    "dm.thinp_metapercent=1",
    "dm.thinp_autoextend_threshold=80",
    "dm.thinp_autoextend_percent=20",
    "dm.directlvm_device_force=false"
  ]
}
```
</p>
</details>


<details><summary>What are the different available storage options available for containers?</summary>
<p>

```
Block Storage
FiLE System Storage
Object Storage
```
</p>
</details>


<details><summary>Do containers create a writable layer on top of Image read-only layers?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>Where is the Docker’s local storage area?</summary>
<p>

```
/var/lib/docker/<storage-driver>
```
</p>
</details>


<details><summary>What is the difference between bind mounts and volumes?</summary>
<p>

```
Volumes are completely managed by docker
Bind Mounts are dependent on the host directory structure
```
</p>
</details>

<details><summary>Volumes don’t increase the size of the containers. Is this statement correct and why?</summary>
<p>

```
Yes. Because volumes live outside of containers
```
</p>
</details>

<details><summary>Volumes don’t increase the size of the containers. Is this statement correct and why?</summary>
<p>

```
Volumes
```
</p>
</details>

<details><summary>How to create a Volume?</summary>
<p>

```
docker volume create my-volume
```
</p>
</details>


<details><summary>How to list docker volumes?</summary>
<p>

```
docker volume ls
```
</p>
</details>


<details><summary>How to inspect docker volume?</summary>
<p>

```
docker volume inspect my-vol
```
</p>
</details>

<details><summary>How to remove docker volumes?</summary>
<p>

```
docker volume rm my-vol
```
</p>
</details>

<details><summary>If you start a container with a volume that does not yet exist, Docker creates the volume for you. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>


<details><summary>How to create a volume myvol2 with a docker run?</summary>
<p>

```
docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```
</p>
</details>


<details><summary>How to verify the volume is created with the container?</summary>
<p>

```
// Look for the mounts section
docker inspect devtest
```
</p>
</details>


<details><summary>How to create a volume with the --mount flag?</summary>
<p>

```
docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```
</p>
</details>

<details><summary>How to remove all unused images not just dangling images?</summary>
<p>

```
docker system prune --all
```
</p>
</details>
