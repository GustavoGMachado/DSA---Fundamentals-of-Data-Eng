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

# What is CI/CD?

CI/CD (or Continuous Integration / Continuous Delivery) is a system development practice that seeks to deliver software more frequently and with higher quality. The idea is that integrations with new functionalities and delivery of executables are done continuously. The focus is always to have a "ready" version of the system, adding new features to the main branch as they are tested and approved, reducing the time to launch features or improvements.

To practice Continuous Integration, that is, to speed up the process of incrementing and adding new features, it is necessary to have a good version control system (Git, for example), frequent unit tests, quick feedback and a good organization of the development environment.

To practice Continuous Delivery, that is, to implement changes with greater speed and quality, it is necessary to execute and automate test flows, rapid implementation after testing is completed and monitoring and recording the performance of the latest versions delivered.

# Terraform Fundamentals

### Provider {}

When we "apply" a .tf file, the first command it will look for will be *"provider"*. What this command does, basically, is go to the Registry (*https://registry.terraform.io/*) and look for that connector that was requested and download it to be used. It is the connector that will take all the configurations described in the file and provision the requested resources. Terraform can be combined with over 4000 services across its providers.

"A provider in Terraform is a plugin that enables interaction with an API. This includes Cloud providers and Software-as-a-service providers. The providers are specified in the Terraform configuration code. They tell Terraform which services it needs to interact with. "

"Providers are a logical abstraction of an upstream API. They are responsible for understanding API interactions and exposing resources."

### Resource {}

This command will specify which resources and their parameters will be automated within the platform indicated in *provider*.

### Basic Terraform Workflow - What is the Process for using Terraform for IaC?

The core Terraform workflow has three steps:

Write - Author infrastructure as code. A very important step because this is where you write exactly what you want to be provisioned, in .tf files;
Plan - Preview changes before applying;
Apply - Provision reproducible infrastructure.

Before step 1, it is good to define exactly which providers, resources and parameters will be used, this includes checking plug-ins, resources, authentications, flowcharts, etc.

*https://developer.hashicorp.com/terraform/intro/core-workflow*

### The basic flow for creating an IaC container with Terraform and AWS is:

1) Create a Docker container, whether with a custom image (dockerfile) or not. If a custom image is needed, *docker build* in the folder where the dockerfile is;
2) Install the aws cli in this container;
3) Using the *aws configure* command, we must authenticate our account in that container.

After that, the container is ready. Then we can work with Terraform automation.
5) In the container that was created, in the folder where the .tf file is, *terraform init* to prepare that file and the environment for running Terraform/HCL;
6) *terraform apply* to run the .tf file.

















