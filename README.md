# 1 - Dependencies management

***git branch name:*** dependencies

## Theory [2]

As usual, we will start with a few theoretical questions:

* [0.5] What is Docker, and how it differs from dependencies management systems? From virtual machines?

Docker is a software platform that allows one to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run including libraries, system tools, code, and runtime.

Docker containers are very easy to deploy in any cloud platform. It can get more applications running on the same hardware when compared to other dependencies management systems, it makes it easy for developers to quickly create, ready-to-run containerized applications and it makes managing and deploying applications much easier.

VMs (virtual machines) have the host OS (operating system) and guest OS inside each VM. A guest OS can be any OS, irrespective of the host OS. In contrast, Docker containers host on a ***single physical server*** with a host OS, which shares among them. Sharing the host OS between containers makes them light and increases the boot time.

The second difference between VMs and Docker is that ***Virtual Machines are stand-alone with their kernel*** and security features. Therefore, applications needing more privileges and security run on virtual machines. 

Docker container packages are self-contained and can run applications in any environment, and since they don’t need a guest OS, they can be ***easily ported across different platforms***. Docker containers can be easily deployed in servers since containers being lightweight can be started and stopped in very less time compared to virtual machines.

* [0.5] What are the advantages and disadvantages of using containers over other approaches?

***Advantages:***
 
1.  Less overhead. Containers require less system resources than traditional or hardware virtual machine environments because they don't include operating system images.
2. More consistent operation. DevOps teams know applications in containers will run the same, regardless of where they are deployed.
3. Flexible resource sharing.
4. Greater efficiency. Containers allow applications to be more rapidly deployed, patched, or scaled. 

***Disadvantages:***

1.   Difficult to manage large amount of containers.
2.   Not right for all tasks. Some applications simply need to be monolithic - they're designed that way, and benefits like scalability and fast deployment don't readily apply.
3. Limited tools. The kind of tools needed to monitor and manage containers are still lacking in the industry.

* [0.5] Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?

A Dockerfile is a text document (without a file extension) that contains the instructions to set up an environment for a Docker container. You can build a Docker image using a Dockerfile.

Now, let's see how Docker containers are created, run and destroyed:

To create container first things first we have to:

```
# create a directory to work in
mkdir example
cd example
```
