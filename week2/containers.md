## Containerized Applications
Software applications typically depend on other libraries, configuration files, or services that
are provided by the runtime environment. The traditional runtime environment for a software
application is a physical host or virtual machine, and application dependencies are installed as part
of the host.

For example, consider a Python application that requires access to a common shared library that
implements the TLS protocol. Traditionally, a system administrator installs the required package
that provides the shared library before installing the Python application.

The major drawback to traditionally deployed software application is that the application's dependencies are entangled with the runtime environment. An application may break when any updates or patches are applied to the base operating system (OS).

For example, an OS update to the TLS shared library removes TLS 1.0 as a supported protocol.
This breaks the deployed Python application because it is written to use the TLS 1.0 protocol for
network requests. This forces the system administrator to roll back the OS update to keep the
application running, preventing other applications from using the benefits of the updated package.
Therefore, a company developing traditional software applications may require a full set of tests to
guarantee that an OS update does not affect applications running on the host.

Furthermore, a traditionally deployed application must be stopped before updating the associated
dependencies. To minimize application downtime, organizations design and implement complex
systems to provide high availability of their applications. Maintaining multiple applications on a
single host often becomes cumbersome, and any deployment or update has the potential to break
one of the organization's applications.

The figure below describes the differences between applications running as a container and running on the host operating system.

![Traditional OS vs Container Image](images/1-trad-os.png)

Alternatively, a software application can be deployed using a container. A container is a set of one or more processes that are isolated from the rest of the system. Containers provide many of the same benefits as virtual machines, such as security, storage, and network isolation. Containers require far fewer hardware resources and are quick to start and terminate. They also isolate the libraries and the runtime resources (such as CPU and storage) for an application to minimize the impact of any OS update to the host OS, as described in the figure above.

The use of containers not only helps with the efficiency, elasticity, and reusability of the hosted applications, but also with application portability. The Open Container Initiative provides a
set of industry standards that define a container runtime specification and a container image specification. The image specification defines the format for the bundle of files and metadata that form a container image. When you build an application as a container image, which complies with the OCI standard, you can use any OCI-compliant container engine to execute the application.

There are many container engines available to manage and execute individual containers, including Rocket, Drawbridge, LXC, Docker, and Podman. Podman is available in Red Hat Enterprise Linux 7.6 and later, and is used in this course to start, manage, and terminate individual containers.

The following are other major advantages to using containers:

**Low hardware footprint**

Containers use OS internal features to create an isolated environment where resources are managed using OS facilities such as namespaces and cgroups. This approach minimizes the amount of CPU and memory overhead compared to a virtual machine hypervisor. Running an application in a VM is a way to create isolation from the running environment, but it requires a heavy layer of services to support the same low hardware footprint isolation provided by containers.

**Environment isolation**

Containers work in a closed environment where changes made to the host OS or other applications do not affect the container. Because the libraries needed by a container are self- contained, the application can run without disruption. For example, each application can exist in its own container with its own set of libraries. An update made to one container does not affect other containers.

**Quick deployment**

Containers deploy quickly because there is no need to install the entire underlying operating system. Normally, to support the isolation, a new OS installation is required on a physical host or VM, and any simple update might require a full OS restart. A container restart does not require stopping any services on the host OS.

**Multiple environment deployment**

In a traditional deployment scenario using a single host, any environment differences could break the application. Using containers, however, all application dependencies and environment settings are encapsulated in the container image.

**Reusability**

The same container can be reused without the need to set up a full OS. For example, the same database container that provides a production database service can be used by
each developer to create a development database during application development. Using containers, there is no longer a need to maintain separate production and development database servers. A single container image is used to create instances of the database service

*********

Often, a software application with all of its dependent services (databases, messaging, file systems) are made to run in a single container. This can lead to the same problems associated with traditional software deployments to virtual machines or physical hosts. In these instances, a multicontainer deployment may be more suitable.

Furthermore, containers are an ideal approach when using microservices for application development. Each service is encapsulated in a lightweight and reliable container environment that can be deployed to a production or development environment. The collection of containerized services required by an application can be hosted on a single machine, removing the need to manage a machine for each service.

In contrast, many applications are not well suited for a containerized environment. For example, applications accessing low-level hardware information, such as memory, file systems, and devices may be unreliable due to container limitations.

[Link to Open Container Initiative](https://opencontainers.org/)

*********
*********

## Quiz: Overview of Container Technology

1. Which two options are examples of software applications that might run in a container? (Choose two.)
    
    - A database-driven Python application accessing services such as a MySQL database, a file transfer protocol (FTP) server, and a web server on a single physical host.
    - A Java Enterprise Edition application, with an Oracle database, and a message broker running on a single VM.
    - An I/O monitoring tool responsible for analyzing the traffic and block data transfer.
    - A memory dump application tool capable of taking snapshots from all the memory CPU caches for debugging purposes.

*********

2. Which two of the following usecases are best suited for containers? (Choose two.)

    - A software provider needs to distribute software that can be reused by other companies in a fast and error-free way.
    - A company is deploying applications on a physical host and would like to improve its performance by using containers.
    - Developers at a company need a disposable environment that mimics the production environment so that they can quickly test the code they develop.
    - A financial company is implementing a CPU-intensive risk analysis tool on their own containers to minimize the number of processors needed.