

# Docker

Docker uses images and containers to allow apps to run anywhere, consistently. Because containers are created from images,  as long as the machine can run Docker your app will run and behave the same regardless of where it is.

# Installation

## Before install
Before you can install Docker Engine, you need to uninstall any conflicting packages.

Your Linux distribution may provide unofficial Docker packages, which may conflict with the official packages provided by Docker. You must uninstall these packages before you install the official version of Docker Engine.

The unofficial packages to uninstall are:

- `docker.io`
- `docker-compose`
- `docker-doc`
- `podman-docker`

Run the following command to uninstall all conflicting packages:
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## Install Docker Engine on Debian
* Documentation: https://docs.docker.com/engine/install/debian/
* Video: How to Install Docker on LMDE 6 | Install Docker on Linux Mint Debian Edition 6: [https://youtu.be/LgBoPB-55-0](https://youtu.be/LgBoPB-55-0)

### Install using the apt repository
* https://docs.docker.com/engine/install/debian/
*
**Set up Docker's `apt` repository.**
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

If you use a derivative distro, such as Kali Linux, you may need to substitute the part of this command that's expected to print the version codename:


```bash
$(. /etc/os-release && echo "$VERSION_CODENAME")
```

```bash

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```



**Change the name**

* Change to "debian bookworm stable"
File system -> etc -> apt -> sources.list.d -> docker.list
```bash
deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian bookworm stable
```

Reference
* https://youtu.be/LgBoPB-55-0

**Install the Docker packages.**
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```


**Specific**
```bash
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'

5:27.1.1-1~debian.12~bookworm
5:27.1.0-1~debian.12~bookworm
...
```

**Verify that the installation is successful by running the `hello-world` image:**
```bash
sudo docker run hello-world
```

## Install Docker Desktop in Debian
https://docs.docker.com/desktop/setup/install/linux/debian/

```bash
sudo apt-get update
sudo apt-get install ./docker-desktop-amd64.deb
```
# Docker commands

```cmd
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Authenticate to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds
  buildx*     Docker Buildx
  checkpoint  Manage checkpoints
  compose*    Docker Compose
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Swarm Commands:
  config      Manage Swarm configs
  node        Manage Swarm nodes
  secret      Manage Swarm secrets
  service     Manage Swarm services
  stack       Manage Swarm stacks
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes

Global Options:
      --config string      Location of client config files (default "/home/rlz-98/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST
                           env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket to connect to
  -l, --log-level string   Set the logging level ("debug", "info", "warn", "error", "fatal") (default
                           "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/rlz-98/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/rlz-98/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/rlz-98/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

```



# Uninstall
```bash
sudo apt remove docker.io
sudo apt remove docker-compose
sudo apt remove docker-doc
sudo apt remove podman-docker
```

# REFERENCES

## YouTube

* Docker Crash Course for Absolute Beginners: https://youtu.be/pg19Z8LL06w
* Docker Tutorial for Beginners -FULL COURSE in 3 Hours -: https://youtu.be/3c-iBn73dDE
* What is Docker in 5 minutes: https://youtu.be/_dfLOzuIg2o
* 100+ Docker Concepts you Need to Know: https://youtu.be/rIrNIzy6U_g
* Docker With Django Tutorial | How To Dockerize A Django Application (Beginners Guide): https://youtu.be/BoM-7VMdo7s
* Docker for Robotics Pt 1 - What and Why?? https://youtu.be/XcJzOYe3E6M?list=PLunhqkrRNRhaqt0UfFxxC_oj7jscss2qe