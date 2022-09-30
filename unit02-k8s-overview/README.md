# Unit 2: Kubernetes Overview
## Containers Overview
### What are containers?
* **Containers** are completely isolated environments, as in they can have their own processes or services, their own network interfaces, their own mounts, just like Virtual machines, except that they all share the same OS kernel.  
* **Containers** have existed for about 10 years now and some of the different types of containers are _LXC_, _LXD_ , _LXCFS_ etc. [Docker](https://www.docker.com/) utilizes **LXC** containers. Setting up these container environments is hard as they are very low level and that is were Docker offers a high level tool with several powerful functionalities making it really easy for end users like us.

### Containers vs Virtual Machines
![Containers vs Virtual Machines](./images/containers-vs-vms.jpg)
* Unlike hypervisors, Docker is not meant to virtualize and run different Operating systems and kernels on the same hardware. The main purpose of Docker is to containerize applications and to ship them and run them.
* It is also important to note that, Docker has less isolation as more resources are shared between containers like the kernel etc. Whereas VMs have complete isolation from each other. 
* Since VMs don’t rely on the underlying OS or kernel, you can run different types of OS such as linux based or windows based on the same hypervisor.

### Container vs Image
![Container vs Image](./images/containers-vs-images.jpg)
* An image is a package or a template, just like a VM template that you might have worked with in the virtualization world. It is used to create one or more containers.
* Containers are running instances off images that are isolated and have their own environments and set of processes.