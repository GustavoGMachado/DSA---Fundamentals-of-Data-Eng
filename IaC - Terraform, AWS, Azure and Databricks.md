# #Space for course notes#

# What is IaC?

IaC is managing and provisioning IT infrastructures using code and automation, without necessarily dealing directly with the physical structure of the devices. We configure all the necessary structures using only codes and software, which will create a consistent, reproducible and scalable structure.

Basically, with IaC it is possible **to create scripts in an automated and declarative way** that will **provision and allocate** an entire **IT structure** so that we can run different types of applications, such as servers, databases, networks and other resources.

Infrastructure can be understood as the set of all physical and virtual resources necessary to support the development, testing, deployment and operation of software.

### When IaC can be used?

IaC is used to facilitate the provisioning of infrastructure resources, such as virtual machines, containers, storage, networking and others, in addition to automating their configuration, allowing the infrastructure to be treated as part of the application, facilitating reproduction, resource allocation and version control for it. 

The declarative approach is very important because users must describe the features and properties of the desired infrastructure through configuration files. This allows the IaC tool to take care of the lower-level details of how the infrastructure should be provisioned and configured.

# What is Terraform?

Terraform is a platform that allows an IT infrastructure as code to be described in a script, which will create, change and manage the structure in an automated way. It allows infrastructures to be managed abstractly, that is, independent of the cloud provider.

Basically, it is an IaC script creation and provisioning platform.

# What is Docker?

Docker is a set of platform-as-a-service (PaaS) products that use operating system-level virtualization to deliver software in packages called containers. Containers are isolated from each other and bundle their own software, libraries and configuration files.

Using Kernel sharing from the host machine and the virtualized machine, Docker and its containers are able to isolate only the necessary configurations of an OS and create lighter virtual systems, as they only consume the resources necessary for their operation.

### What is Docker Image?

A container image is a file executed in a Docker environment that has a series of packages containing all the libraries, dependencies and files necessary to run the container. It's basically the file for creating and configuring a Docker container.

### How can we create our own Docker Image?

We can create our own Docker image from a Dockerfile. With the “docker build” command, executed in the directory that contains this type of file, we can create a customized Dockerfile which can serve as a build for any container later.

# What is DevOps and how does it relate to IaC?

DevOps is an area of IT that seeks to approach relationships between Development and Operations of applications and systems closer together, seeking collaboration between them and continuous development, in order to improve the efficiency and effectiveness of the software delivery process.

Strongly linked to IaC concepts, which allow the management and configuration of IT infrastructures in an automated and user-friendly way, using code instead of physical manipulations or complex interfaces and in a shared, versioned, tested and easy to manage way.

Basically, IaC is a fundamental practice for implementing DevOps, as it allows the implementation of structures in a simplified way that can be shared by different areas.

# How can we use Terraform?

To use Terraform we need a file .tf that describes in HCL (HashiCorp Configuration Language) all the configurations need to start the resource. We must run it into a structure, like containers, that contains Terraform and AWS CLI.

HCL is a configuration language developed by HashiCorp to describe infrastructure and application configurations in a declarative manner.

Inside the folder that contains the .tf file, run "terraform init" to configure the workbench and prepare it for creating, updating, and removing resources. After that, runs "terraform apply" to apply the .tf file and create all the resources described in the file. With "terraform destroy" we can delete the entire resource described into .tf file.

In summary, the purpose of Terraform is to read the .tf file and run it on your cloud provider.
