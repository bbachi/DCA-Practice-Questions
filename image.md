
## Content may include the following:

* Describe Dockerfile options [add, copy, volumes, expose, entrypoint, etc)
* Show the main parts of a Dockerfile
* Give examples on how to create an efficient image via a Dockerfile
* Use CLI commands such as list, delete, prune, rmi, etc to manage images
* Inspect images and report specific attributes using filter and format
* Demonstrate tagging an image
* Utilize a registry to store an image
* Display layers of a Docker image
* Apply a file to create a Docker image
* Modify an image to a single layer
* Describe how image layers work
* Deploy a registry (not architect)
* Configure a registry
* Log into a registry
* Utilize search in a registry
* Tag an image
* Push an image to a registry
* Sign an image in a registry
* Pull an image from a registry
* Describe how image deletion works
* Delete an image from a registry

## Questions:

<details><summary>Which instruction sets the base image for the subsequent builds in the Dokcerfile?</summary>
<p>

```
FROM
```
</p>
</details>

<details><summary>No instruction can precede FROM in the Dockerfile. Is this statement correct?</summary>
<p>

```
No. ARG is the only instruction can precede FROM
```
</p>
</details>

<details><summary>What are the two forms for the RUN instruction?</summary>
<p>

```
shell form: RUN <command>
exec form: RUN ["executable", "param1", "param2"]
```
</p>
</details>

<details><summary>What does the RUN instruction do in the Dockerfile?</summary>
<p>

```
The RUN instruction will execute any commands in a new layer on top of the current image and commit the results.
```
</p>
</details>

<details><summary>The RUN command normally utilizes cache from the previous build. Which flag should you specify for the build not to use cache?</summary>
<p>

```
--no-cache
docker build --no-cache .
```
</p>
</details>

<details><summary>Is there any other instruction that can invalidate the cache?</summary>
<p>

```
Yes. ADD
```
</p>
</details>

<details><summary>How many forms that CMD instruction has?</summary>
<p>

```
CMD ["executable","param1","param2"] (exec form, this is the preferred form)
CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
CMD command param1 param2 (shell form)
```
</p>
</details>

<details><summary>If CMD instruction provides default arguments for the ENTRYPOINT instruction, both should be specified in JSON format. Is this statement correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>What is the purpose of the CMD instruction in the Dockerfile?</summary>
<p>

```
The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
```
</p>
</details>

<details><summary>How to make your container execute the same executable every time?</summary>
<p>

```
use ENTRYPOINT in combination with CMD
```
</p>
</details>

<details><summary>What is the purpose of the LABEL instruction in the Dockerfile?</summary>
<p>

```
It adds metadata to the Image
```
</p>
</details>


<details><summary>How to check the labels for the current image?</summary>
<p>

```
docker inspect // Under Labels section
```
</p>
</details>

<details><summary> The EXPOSE instruction actually publish the port. Is this statement correct?</summary>
<p>

```
No. It serves as a type of documentation between the image publisher and image consumer
```
</p>
</details>

<details><summary>What should you do to actually publish the ports?</summary>
<p>

```
use -p flag when running a container
```
</p>
</details>

<details><summary>What is the purpose of the ENV instruction in the Dockerfile?</summary>
<p>

```
ENV <key> <value>
an ENV instruction sets the enviroment value to the key and it is available for the subsequent build steps and in the running container as well.
```
</p>
</details>

<details><summary>How to change the environment variables when running containers?</summary>
<p>

```
docker run --env <key>=<value>
```
</p>
</details>

<details><summary>What is the difference between ADD and COPY instructions?</summary>
<p>

```
ADD [--chown=<user>:<group>] <src>... <dest>
The ADD instruction copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.
COPY [--chown=<user>:<group>] <src>... <dest>
The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.
```
</p>
</details>

<details><summary>What is ENTRYPOINT instruction in the Dockerfile?</summary>
<p>

```
An ENTRYPOINT allows you to configure a container that will run as an executable.
Command line arguments to docker run <image> will be appended after all elements in an exec form ENTRYPOINT, and will override all elements specified using CMD.
```
</p>
</details>

<details><summary>How can you override the ENTRYPOINT instruction?</summary>
<p>

```
docker run --entrypoint
```
</p>
</details>

<details><summary>What is the VOLUME instruction in the Dockerfile?</summary>
<p>

```
The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.
```
</p>
</details>

<details><summary>What initializes the newly created Volume?</summary>
<p>

```
docker run -v
```
</p>
</details>

<details><summary>What is the USER instruction in the Dockerfile?</summary>
<p>

```
The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile.
```
</p>
</details>

<details><summary>What is the WORKDIR instruction in the Dockerfile?</summary>
<p>

```
The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.
```
</p>
</details>

<details><summary>You have specified multiple WORKDIR instructions in the Dockerfile what is the result WORKDIR?</summary>
<p>

```
WORKDIR /a
WORKDIR b
WORKDIR c

RUN pwd
result: /a/b/c
```
</p>
</details>


<details><summary>You have specified multiple WORKDIR instructions in the Dockerfile what is the result WORKDIR?</summary>
<p>

```
WORKDIR /a
WORKDIR /b
WORKDIR c

RUN pwd
result: /b/c
```
</p>
</details>


<details><summary> What is the ARG instruction in the Dockerfile?</summary>
<p>

```
ARG <name>[=<default value>]
The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag.
```
</p>
</details>

<details><summary>What is the ONBUILD instruction in the Dockerfile?</summary>
<p>

```
The ONBUILD instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build.
```
</p>
</details>


<details><summary>Which instruction sets the system call signal that will be sent to the container to exit?</summary>
<p>

```
STOPSIGNAL signal
```
</p>
</details>

<details><summary>Which instruction let Docker daemon know the health of the container?</summary>
<p>

```
HEALTHCHECK
```
</p>
</details>

<details><summary>What are all the options that can be provided for the HEALTHCHECK instruction?</summary>
<p>

```
--interval=DURATION (default: 30s)
--timeout=DURATION (default: 30s)
--start-period=DURATION (default: 0s)
--retries=N (default: 3)
```
</p>
</details>

<details><summary>What is the SHELL instruction in the Dockerfile?</summary>
<p>

```
The SHELL instruction allows the default shell used for the shell form of commands to be overridden. The default shell on Linux is ["/bin/sh", "-c"], and on Windows is ["cmd", "/S", "/C"]. The SHELL instruction must be written in JSON form in a Dockerfile.
```
</p>
</details>

<details><summary>Create ephemeral containers is considered best practice?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>What should you do if you want to exclude some files while executing the docker build image and don’t want to send all the files to Docker daemon?</summary>
<p>

```
use .dockerignore file
```
</p>
</details>

<details><summary>What is the best way to drastically reduce the size of an image?</summary>
<p>

```
Multi Stage Builds
```
</p>
</details>

<details><summary>How do you minimize the number of layers while building the image?</summary>
<p>

```
Only the instructions RUN, COPY, ADD create layers.
Where possible, use multi-stage builds, and only copy the artifacts you need into the final image.
sort multi line arguments
RUN apt-get update && apt-get install -y \
  bzr \
  cvs \
  git \
  mercurial \
  subversion
```
</p>
</details>

<details><summary>How to leverage the build cache?</summary>
<p>

```
Put instructions that likely to change often at the bottom of the dockerfile.
```
</p>
</details>


<details><summary>How to remove unused images?</summary>
<p>

```
docker image prune
```
</p>
</details>

<details><summary>How to see the history of the image?</summary>
<p>

```
docker image history
```
</p>
</details>

<details><summary>How to format the output of the docker inspect command?</summary>
<p>

```
by using --format flag
//examples
docker inspect --format='{{range .NetworkSettings.Networks}}{{.MacAddress}}{{end}}' $INSTANCE_ID
docker inspect --format='{{.LogPath}}' $INSTANCE_ID
```
</p>
</details>

<details><summary>How to tag an image?</summary>
<p>

```
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
docker tag 0e5574283393 fedora/httpd:version1.0 // by id
docker tag httpd fedora/httpd:version1.0 // by name
docker tag httpd:test fedora/httpd:version1.0.test // by name and tag
docker tag 0e5574283393 myregistryhost:5000/fedora/httpd:version1.0
```
</p>
</details>

<details><summary>How to run a local registry?</summary>
<p>

```
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```
</p>
</details>

<details><summary>How to copy an image from the docker hub to a local repository?</summary>
<p>

```
// pull an image from the Docker Hub
docker pull ubuntu
// tag an image
docker tag ubuntu:16.04 localhost:5000/my-ubuntu
// push the image
docker push localhost:5000/my-ubuntu
```
</p>
</details>


<details><summary>How to stop and remove a local registry?</summary>
<p>

```
docker container stop registry && docker container rm -v registry
```
</p>
</details>

<details><summary>How to display the layers of the Docker image?</summary>
<p>

```
docker image inspect //under Layers section
```
</p>
</details>

<details><summary>How to create a Docker image from archive or stdin?</summary>
<p>

```
docker image load
// example
docker image load -i example.tar
```
</p>
</details>

<details><summary>How to modify an image to a single layer?</summary>
<p>

```
// take any multiple layer image
// run the container
docker export <container> > single-layer.tar
docker import /path/to/single-layer.tar
// check the history
docker image history
```
</p>
</details>

<details><summary>Each layer is only a set of differences from the layer before it. The layers are stacked on top of each other. Is this statement about the image correct?</summary>
<p>

```
Yes
```
</p>
</details>

<details><summary>When you create a container It adds one writable layer on top of all the layers of the image. Is this statement about the image correct?</summary>
<p>

```
yes
```
</p>
</details>


<details><summary>What is the copy-on-write (CoW) strategy?</summary>
<p>

```
Copy-on-write is a strategy of sharing and copying files for maximum efficiency. If a file or directory exists in a lower layer within the image, and another layer (including the writable layer) needs read access to it, it just uses the existing file. The first time another layer needs to modify the file (when building the image or running the container), the file is copied into that layer and modified. This minimizes I/O and the size of each of the subsequent layers.
```
</p>
</details>


<details><summary>How to customize the registry while deploying?</summary>
<p>

```
// customize published port
docker run -d \
  -p 5001:5000 \
  --name registry-test \
  registry:2
// If you want to change the port the registry listens on within the container
docker run -d \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:5001 \
  -p 5001:5001 \
  --name registry-test \
  registry:2
// storage customization
docker run -d \
  -p 5000:5000 \
  --restart=always \
  --name registry \
  -v /mnt/registry:/var/lib/registry \
  registry:2
```
</p>
</details>

<details><summary>How to configure a registry?</summary>
<p>

```
The Registry configuration is based on a YAML file. you can specify a configuration variable from the environment by passing -e arguments to your docker run stanza or from within a Dockerfile using the ENV instruction.
// for example you have a configuration like this for root directory
storage:
  filesystem:
    rootdirectory: /var/lib/registry
// you can create environment variable like this
REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY=/somewhere
it will change from /var/lib/registry to /somewhere
```
</p>
</details>

<details><summary>What is the location of the registry configuration file?</summary>
<p>

```
/etc/docker/registry/config.yml
```
</p>
</details>


<details><summary>How to customize an entire config file of registry?</summary>
<p>

```
docker run -d -p 5000:5000 --restart=always --name registry \
             -v `pwd`/config.yml:/etc/docker/registry/config.yml \
             registry:2
```
</p>
</details>

<details><summary>How to login to a self-hosted registry?</summary>
<p>

```
docker login localhost:5000
```
</p>
</details>

<details><summary>Where do you configure any credential helpers or credentials for the registry to prevent passing every time you log in?</summary>
<p>

```
/etc/docker/daemon.json
```
</p>
</details>


<details><summary>How to limit the number of records when docker search?</summary>
<p>

```
docker search nginx --limit=2
```
</p>
</details>

<details><summary>How to format the docker search?</summary>
<p>

```
docker search --format "{{.Name}}: {{.StarCount}}" nginx
```
</p>
</details>

<details><summary>How to disable Image signing while pushing an image to the repository?</summary>
<p>

```
docker push [OPTIONS] NAME[:TAG]
--disable-content-trust=true
```
</p>
</details>

<details><summary>How to enable docker content trust in the Docker CLI?</summary>
<p>

```
export DOCKER_CONTENT_TRUST=1
docker push <dtr-domain>/<repository>/<image>:<tag>
```
</p>
</details>

<details><summary>How to pull an image from the repository?</summary>
<p>

```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
// pulling from docker hub by default
docker pull debian
// pulling from other repositories
docker pull myregistry.local:5000/testing/test-image
```
</p>
</details>

<details><summary>How to pull an image with multiple images?</summary>
<p>

```
-a or --all-tags
docker pull --all-tags fedora
```
</p>
</details>

<details><summary>How to remove all images which are not used by existing containers?</summary>
<p>

```
docker image prune -a
```
</p>
</details>

<details><summary>How to limit the scope when pruning images?</summary>
<p>

```
by uisng --filter flag
docker image prune -a --filter "until=24h"
```
</p>
</details>

<details><summary>How to remove an image?</summary>
<p>

```
docker rmi <IMAGE ID>
```
</p>
</details>

<details><summary>How to remove image without deleting the untagged parent images?</summary>
<p>

```
docker rmi --no-prune <IMAGE ID>
```
</p>
</details>

<details><summary>How to delete an image from the repository?</summary>
<p>

```
login into DTR web UI
go to the TAGS section delete the specific TAG 
you can also delete all images by deleting the entire repository
```
</p>
</details>
