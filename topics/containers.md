# What is a container?

https://linuxcontainers.org/incus/docs/main/explanation/containers_and_vms/

Virtual Machines
Use a dedicated kernel
Can host different OS types
Use more resources
Requires hardware virtualization
Can host multiple applications
Supported by Incus/LXD

Application Containers
Uses the kernel of the host
Can only host Linux
Uses less resources
Software-only
Can host a single app
Supported by Docker

System Containers
Uses the kernel of the host
Can only host Linux
Use less resources
Software-only
Can host multiple applications
Supported by Incus/LXD

## Virtual Machines

Virtual machines create a virtual version of a physical machine, using hardware features of the host system. The boundaries between the host system and virtual machines is enforced by those hardware features.

## Application Containers

Application containers (as provided by, for example, Docker) package a single process or application.
Application containers such as Docker, are running a single process per container. Can be brought up and down as will and are meant to be ephemeral.
Therefore, application containers are suitable to provide separate components.

## System Containers

System containers use the already running OS kernel of the host system instead of launching their own kernel. If you run several system containers, they all share the same kernel, which makes them faster and more lightweight than virtual machines.
Can install packages, manage services, define backup policies, monitoring, etc. Typically long lasting. Can use normal distribution of package managers and security updates instead of waiting for security fixes.
system containers provide a full solution of libraries, applications, databases and so on
use system containers to create different user spaces and isolate all processes belonging to each user space, which is not what application containers are intended for.

## History

In 1999 FreeBSD introduced `jails` https://en.wikipedia.org/wiki/FreeBSD_jail. This enabled a second BSD system on the same kernel as the main system.
This concept lead to `Linux vServer` http://linux-vserver.org/Welcome_to_Linux-VServer.org
Solaris had `Zones` for Solaris OS https://en.wikipedia.org/wiki/Solaris_Containers
OpenVZ followed and started on VPSs (virtual private servers) on Linux.
All provided system containers that ran a full Linux operating system.
Linux Containers, known as LXC, were the first system containers entirely based on mainline Linux features. No patching was required.
Could create system and application containers.
Docker was initially based on LXC until replaced by their own runtime.

# Container Runtimes

## systemd-nspawn

run a command or OS in a light weight namespace container
It is similar to LXC, but much simpler to configure. Most of the necessary software is already installed on contemporary Debian systems.
https://wiki.debian.org/nspawn

## Linux Containers

LXC is considered between chroot and a full virtual machine.
LXC creates a standard Linux install without the need for a separate kernel.
LXC containers are essentially a copy of the current operating system running on the same kernel, without virtualization, and no overhead processes.
The kernel sees the processes running in the container as normal system processes that have different views of the operating system.

Containers should be used in all cases except when a different kernel is required for the container.

System containers are easier to manage than virtual machines. They can be monitored from the host system. File sharing and resource constraints can also be changed without restarting. PCI devices can also be shared.

# Container Managers

## LXC

- Container runtime allowing creation of multiple isolated Linux systems (containers) on a control host using a single Linux kernel
- only supports containers
- low level tool requiring expertise

## LXD

Utilizes LXC to run system containers. LXD is a daemon running that manages instances of LXC in an easy/unified way.
Similar to VMWare or KVM hypervisors without virtualization overhead.

- system container and virtual machine manager built on top of LXC, enabling easier management, control and integration
- supports containers and VMs
- better user experience through CLI and REST API

## Incus

https://linuxcontainers.org/incus/introduction/

Fork of LXD. System container and virtual machine manager.

## Docker

Containerization platform. Docker abstracts away storage, networking, logging, etc. Can decompose and isolate individual processes.

# containerd

Daemon based runtime that manges lifecycles of Docker containers, such as running and monitoring of containers.

https://github.com/containerd/containerd/blob/main/docs/getting-started.md

# OCI Image Spec

# Image push and pull

# OCI Runtime Spec aka runC

# Container Runtime and Lifecycle
