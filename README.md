
## What exactly is a container ?

A container is a standardized software component that wraps up code and all of its dependencies to ensure that an application will run swiftly and consistently in different computing environments. An application's code, runtime, system tools, libraries, and settings are all included in a lightweight, independent, executable package known as a "Docker container image."

In other words, an application container is a collection of your application, the application libraries needed to run it, and the bare minimal set of system dependencies.

https://user-images.githubusercontent.com/43399466/217262726-7cabcb5b-074d-45cc-950e-84f7119e7162.png



## Virtual Machine Vs Containers

Virtual machines and containers both employ technology to isolate applications and their dependencies, but there are several important distinctions between the two:

    1. Portability: Containers are made to be portable and can function on any system running a host operating system that is compatible with them. Since VMs require a compatible hypervisor to function, they are less portable.

    2. Utilization of resources: Containers share the host operating system kernel, which makes them lighter and faster than virtual machines (VMs). Since VMs include a full-featured OS and hypervisor, they require additional resources.

    3. Security: Because each VM runs on its own operating system and may be separated from the host and other VMs, they offer a higher level of security. Given that they share the host operating system, containers offer less separation.

    4.  Management: Due to their lightweight and quick-moving nature, containers are often easier to manage than virtual machines.



## What makes containers so light?

Due to the use of a technology called containerization, which shares the kernel and libraries of the host operating system while yet providing isolation for the application and its dependencies, containers are lightweight. Due to the lack of a full operating system requirement, containers have a smaller footprint than conventional virtual machines. The basic design of Docker containers further reduces their size by just including what is required for an application to run.

Let's use an illustration to try to comprehend this:

The official Ubuntu base image, which you can use for your container, is seen in the screenshot below. It's only 22 MB, isn't that incredibly small? On the other hand, the official Ubuntu VM image is close to 2.3 GB. So the base image for containers is almost 100 times smaller than the VM image.

!(https://user-images.githubusercontent.com/43399466/217493284-85411ae0-b283-4475-9729-6b082e35fc7d.png)


To give a more accurate representation of the files and folders that containers base images have and the files and folders that containers use from the host operating system (not always exact because it depends on the base image). See below.



### Files and Folders in containers base images

```
    /bin: contains binary executable files, such as the ls, cp, and ps commands.

    /sbin: contains system binary executable files, such as the init and shutdown commands.

    /etc: contains configuration files for various system services.

    /lib: contains library files that are used by the binary executables.

    /usr: contains user-related files and utilities, such as applications, libraries, and documentation.

    /var: contains variable data, such as log files, spool files, and temporary files.

    /root: is the home directory of the root user.
```



### Files and Folders that containers use from host operating system

```
    The host's file system: Docker containers can access the host file system using bind mounts, which allow the container to read and write files in the host file system.

    Networking stack: The host's networking stack is used to provide network connectivity to the container. Docker containers can be connected to the host's network directly or through a virtual network.

    System calls: The host's kernel handles system calls from the container, which is how the container accesses the host's resources, such as CPU, memory, and I/O.

    Namespaces: Docker containers use Linux namespaces to create isolated environments for the container's processes. Namespaces provide isolation for resources such as the file system, process ID, and network.

    Control groups (cgroups): Docker containers use cgroups to limit and control the amount of resources, such as CPU, memory, and I/O, that a container can access.

```

Although a container uses resources from the host operating system, it is still separate from the host and other containers; as a result, changes to the container do not affect the host or other containers.

In summary, because container base images are intended to be simple and only contain the components required for operating a particular application or service, they are often smaller than VM images. On the other hand, VMs are substantially bigger since they replicate a whole operating system, including all of its libraries, tools, and system files.


### What is Docker ?

Docker is a framework for application containerization that makes it simple to do so. With Docker, you can generate container images, use those images to launch containers, and then push those containers to container marketplaces like DockerHub, Quay.io, and others.

In simple words, you can understand as `containerization is a concept or technology` and `Docker Implements Containerization`.


### Docker Architecture ?

![image](https://user-images.githubusercontent.com/43399466/217507877-212d3a60-143a-4a1d-ab79-4bb615cb4622.png)

The image above makes it abundantly evident that Docker Deamon is the brains of Docker. Docker is rendered inoperable if the Docker Deamon is killed or ceases to function for any reason.

### Docker LifeCycle

To comprehend the lifetime of Docker, we can refer to the image above.

Three crucial elements are:

1. docker build -> builds docker images from Dockerfile
2. docker run   -> runs container from docker images
3. docker push  -> push the container image to public/private regestries to share the docker images.

!(https://user-images.githubusercontent.com/43399466/217511949-81f897b2-70ee-41d1-b229-38d0572c54c7.png)



### Having terminology understanding (Inspired from Docker Docs)


#### Docker daemon

The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.


#### Docker client

The Docker daemon (dockerd) handles Docker objects like images, containers, networks, and volumes while listening for Docker API requests. To manage Docker services, a daemon can also talk to other daemons.


#### Docker Desktop

You may create and share containerized applications and microservices using Docker Desktop, an application that is simple to install on Mac, Windows, or Linux systems. Docker Desktop comes with Kubernetes, Credential Helper, Docker Compose, Docker Content Trust, Docker Daemon (dockerd), and Docker Client (docker).


#### Docker registries

Docker images are kept in a registry. Anyone can utilize Docker Hub, a public registry, and by default, Docker is set up to search there for images. Even running your own private register is an option.

The needed images are taken from your configured registry when you use the docker pull or docker run commands. The image you specify gets pushed to the registry you've specified when you execute the docker push command.

Objects such as images, containers, networks, volumes, plugins, and other things can be created and used when using Docker. Several of such items are briefly described in this section.


#### Dockerfile

The instructions for creating your Docker Image are included in a file called a Dockerfile.


#### Images

An image is a read-only template that contains directions for building a Docker container. Frequently, an image is derived from another image and then modified somewhat. For instance, you might create an image based on the Ubuntu image that also installs your application, the Apache web server, and the configuration information required to run it.

You can either produce your own images or choose to exclusively use those produced by others and made available in a registry. To construct your own image, you write a Dockerfile that has a straightforward syntax for specifying the actions required to build and execute the image. A layer is created in the image for each Dockerfile instruction. Only the layers that have changed are rebuilt when you modify the Dockerfile and create a new image. When compared to other virtualization technologies, this helps explain why images are so light, quick, and compact.



## Install Docker

Docker installation instructions are provided in the link below in great detail.

https://docs.docker.com/get-docker/

For Demo,

You can create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```
sudo apt update
sudo apt install docker.io -y
```


### Launch Docker and grant access.

After installing Docker with sudo access, many beginners make the extremely common error of skipping the step of starting the Docker daemon and granting access to the user they want to use to communicate with Docker and execute Docker commands.

Make sure the docker daemon is always active.

Run the command below to quickly confirm your Docker installation.

```
docker run hello-world
```

If the results show:

```
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This could indicate two things:
1. Docker deamon is not running.
2. Your user does not have access to run docker commands.


### Start the Docker daemon

To make sure the Docker daemon is indeed running and active, issue the command below.

```
sudo systemctl status docker
```

If the docker daemon doesn't appear to be running, try the command below to start it.

```
sudo systemctl start docker
```


### Give your user permission to execute docker commands.

You must add the user to the Docker Linux group before allowing them to execute the docker command. When Docker is installed, Docker group is automatically created.

```
sudo usermod -aG docker ubuntu
```

In the above command `ubuntu` is the name of the user, you can change the username appropriately.

**NOTE:** : For the changes to take effect, you must log out and then log back in.


### Docker is installed and operational.

To confirm that Docker is operational, issue the same command once more.

```
docker run hello-world
```

Results should resemble:

```
....
....
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
...
```
