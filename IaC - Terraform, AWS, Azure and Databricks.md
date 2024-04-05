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

Basically, we can create our own images to automate the creation of Docker containers. Instead of creating an empty container and inserting resources later, we can, through the Dockerfile, write a series of commands that will be applied automatically when we create a new container with that customized Image. Dockerfile is widely used to create Images with pre-configured commands and resources for containers. Any changes involving the Dockerfile or its parameters will require a new *docker build* to add the changes made.

One example was during the course when we created a container with the AWS CLI automatically installed because of the Dockerfile.

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

### provider {}

When we "apply" a .tf file, the first command it will look for will be *"provider"*. What this command does, basically, is go to the Registry (*https://registry.terraform.io/*) and look for that connector that was requested and download it to be used. It is the connector that will take all the configurations described in the file and provision the requested resources. Terraform can be combined with over 4000 services across its providers.

"A provider in Terraform is a plugin that enables interaction with an API. This includes Cloud providers and Software-as-a-service providers. The providers are specified in the Terraform configuration code. They tell Terraform which services it needs to interact with. "

"Providers are a logical abstraction of an upstream API. They are responsible for understanding API interactions and exposing resources."

### resource {}

This command will specify which resources and their parameters will be automated within the platform indicated in *provider*.

### Basic Terraform Workflow - What is the Process for using Terraform for IaC?

The core Terraform workflow has three steps:

Write - Author infrastructure as code. A very important step because this is where you write exactly what you want to be provisioned, in .tf files;
Plan - Preview changes before applying;
Apply - Provision reproducible infrastructure.

Before step 1, it is good to define exactly which providers, resources and parameters will be used, this includes checking plug-ins, resources, authentications, flowcharts, etc.

*https://developer.hashicorp.com/terraform/intro/core-workflow*

### variable ()

This command will set variables in .tf file that can be used in the script. We can define the values of these variables in the file itself, pass them through parameters when using the *terraform plan/apply/destroy* commands, with the *-var* parameter or in variable definitions (*.tfvars*) files, either specified on the command line or automatically loaded.

```terraform
# .tf file

variable "instance_type" {
  description = ""
}

variable "name" {
  description = ""
}

provider "aws" {
  region  = "us-east-2"  
}

resource "aws_instance" "example" {
  ami           = "ami-0a0d9cf81c479446a"  # AMI na AWS
  instance_type = var.instance_type

  tags = {
    Name = var.name
  }
}
```

```
terraform apply -var 'instance_type=t2.micro' -var 'name=new-example-terraform'
```
#### *main.tf*, *terraform.tf* and *variables.tfvars*

Perhaps the best option for defining variables, .tfvars is a *variable definitions file*, which is a file that follows the same HCL standard, but where only variables and their values are described, in the key-value type. To use this type of configuration, we pass the .tfvars file through the *-var-file* parameter when using *terraform plan/apply*.

```terraform
# .tfvars file

instance_type = "t2.micro"
name = "new-example-terraform"
```

```
terraform apply -var-file="example.tfvars"
```

Another approach we can use is to have 3 files for our structure, a *main.tf* that will have the module's main configurations, a *terraform.tf* with the declaration of the variables used in the process and a *variables.tfvars* with the initialization of those variables.

```terraform
# main.tf file

provider "aws" {
  region  = "us-east-2"  
}

resource "aws_instance" "example" {
  ami           = "ami-0a0d9cf81c479446a"  # AMI na AWS
  instance_type = var.instance_type

  tags = {
    Name = var.name
  }
}
```

```terraform
# terraform.tf file

variable "instance_type" {
  description = ""
}

variable "name" {
  description = ""
}
```

```terraform
# variables.tfvars file

instance_type = "t2.micro"
name = "new-example-terraform"
```

```
terraform plan
terraform apply
terraform destroy
```

This makes us to further separate the configurations in the module and allows for greater scalability, reuse and configuration flexibility.

*Ps: the files can have any name, but if we use **main**, **terraform** and **variables**, we do not need to use parameters when calling the terraform **plan/apply/destroy** commands in the terminal.*

*https://developer.hashicorp.com/terraform/language/values/variables*

### The basic flow for creating an IaC container with Terraform and AWS is:


1) Create a Docker container, whether with a custom image (dockerfile) or not. If a custom image is needed, *docker build* in the folder where the dockerfile is;
2) Install the aws cli in this container;
3) Using the *aws configure* command, we must authenticate our account in that container.

After that, the container is ready. Then we can work with Terraform automation.

4) In the container that was created, in the folder where the .tf file is, *terraform init* to prepare that file and the environment for running Terraform/HCL;
5) *terraform apply* to run the .tf file.

### Terraform Commands

**terraform *init***:

This command will prepare the environment where it was executed to interpret the .tf file. It starts by initializing the back-end, downloading the necessary provider plugins and creating a *.terraform.lock.hcl* file that records the parameters and exact versions of the providers passed in that solution, so that everyone on the same team/project is on the same page.

"Terraform has created a lock file .terraform.lock.hcl to record the provider selections it made above. Include this file in your version control repository so that Terraform can guarantee to make the same selections by default when you run "terraform init" in the future."

Basically, the *init* command will prepare the lock and state - .terraform folder that is created after executing the command - files. It will initialize the repository so that it can connect to a specific provider.

**terraform *plan***:

This command creates a "plan", that is, a .txt that contains the binaries of all the parameters that will be used in that .tf file. The advantage of this is that we can execute the plan later, with all those settings that were saved there, including on other machines.

**terraform *apply***:

This command will finally connect to the provider, perform the necessary authentication and execute that .tf file and apply all the resources configured in this solution.

**terraform *destroy***:

Used to completely destroy any resources that were created in the module.

### Terraform modules

Terraform modules are a way to organize and create reusable code. They allow you to encapsulate resources, variables, and other configurations in a unit that can be easily shared and referenced across multiple Terraform projects. It is basically dividing the solution into templates that can be reused and shared in IaC projects, in addition to easier maintenance.

The objective is to have secondary templates (called Child Modules) that will modularize the *declaration of instances and their attributes*, as variables. These templates can contain .tf files such as main.tf (resource) outputs.tf (output variables) and variables (input variables):

```terraform
# main.tf (in a Child Module)

resource "aws_instance" "example_instance" {
  count         = var.instance_count
  ami           = var.ami_id
  instance_type = var.instance_type
}
```

```terraform
# variables.tf

variable "instance_count" {
  type = number
}

variable "ami_id" {
  type = string
}

variable "instance_type" {
  type = string
}
```

```terraform
# outputs.tf

output "instance_ids" {
  value = aws_instance.example_instance.*.id
}

```

Note that we only have a generalized template for creating EC2 instances on AWS (it isn't even necessary to define a provider), as well as its variable declaration. **We don't have initialization/assignment of values**. This is a module.

And in the root folder, we define which module we want to call (through the *source* command), passing the necessary variables. **Here we have initialization/assignment of values**.

```terraform
# main.tf (in a Root Module) consumindo 2 módulos em uma só chamada

module "example_ec2_instances" {
  
  source = "./modules/ec2-instances" # main.tf / output.tf / variables.tf 

  instance_count = 3
  ami_id         = "ami-0a0d9cf81c479446a"
  instance_type  = "t2.micro"
}

module "example_s3_bucket" {

  source = "./modules/s3-bucket"

  bucket_name = "nome exclusivo 3243446"
}
```

Basically, the Child Modules will specify the IaC's that can be used and their parameters (variables, outputs, etc.) while the Root Modules will create the Infrastructure described in these Child Modules, searching for the sources and passing the necessary values.

*https://developer.hashicorp.com/terraform/language/modules*

### terraform.tfstate

This file, which follows a JSON representation, is crucial for the operation of Terraform and ***describes the current state of the infrastructure being managed***. The *terraform.tfstate* file contains information about resources that were created, modified, or removed using Terraform. It stores details such as resource IDs, the specific attributes of each resource, some metadata used and other information needed by Terraform to manage your infrastructure effectively.

When commands such as *apply* or *destroy* are executed, Terraform consults the current *.tfstate* (the current settings) of the solution and from there, identifies which changes will need to be implemented to achieve the new desired state.

The state can be used in 2 ways: **local**, which is Terraform storing the file locally in the solution's own working folder, or **remote**, storing it in some type of cloud provider (such as Amazon S3 or Terraform Cloud), which can be shared between people and systems and with blocks to avoid conflicts.

It is worth noting that this file may contain sensitive application information, so it should not be used in any way.

*https://developer.hashicorp.com/terraform/language/state*

### Terraform provisioner

Not every type of structure can be allocated and/or manipulated directly through IaC, in a declarative way. But even so, with **terraform provisioner**, we can fix this problem and **configure resources externally**.

The purpose of the tool is to allow the configuration of resources through **external** scripts, when it is not possible to configure resources with the default terraform settings. Provisioners can be used to model specific actions on the local machine or on a remote machine in order to prepare servers or other infrastructure objects for service.

When we use provisioners, we are leaving the context of Terraform codes and adding complexity and uncertainty to the use of the tool. Therefore, Terraform discourages the excessive use of provisioners because they can harm the portability, scalability, reliability and state management of the platform, because they run in a different, external "world" without any control from Terraform.

#### There are 3 different types of provisioners in terraform:

#### ***Local Provisioner***:

*"The local-exec provisioner invokes a local executable after a resource is created. This invokes a process on the machine running Terraform, **not on the resource**"*.

With this, we can run any scripts in the machine where Terraform is running (in the OS context), but in a way completely isolated from the scope of Terraform. In other words, terraform doesn't control or influence **anything** executed in this call.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    command = "echo ${self.private_ip} >> private_ips.txt"
  }
}
```

Because the provisioner is completely isolated, terraform cannot guarantee that it is in an operable state, even if the resource has already been fully provisioned.

#### ***File Provisioner***:

With the *file* provisioner, we can copies files or directories from the local machine to a remote machine.

```terraform
resource "aws_instance" "web" {
  # ...

  # Copies the myapp.conf file to /etc/myapp.conf
  provisioner "file" {
    source      = "conf/myapp.conf"
    destination = "/etc/myapp.conf"
  }

  # Copies the configs.d folder to /etc/configs.d
  provisioner "file" {
    source      = "conf/configs.d"
    destination = "/etc"
  }

}
```

*https://developer.hashicorp.com/terraform/language/resources/provisioners/syntax*

#### ***Remote Provisioner***:

With the Remote Provisioner, we can run a command on a remote machine over SSH or WinRM. 

The remote-exec provisioner invokes a script on a remote resource after it is created. But to do this, it is necessary to configure some parameters using the *connection* command. The connection can be made through both *ssh* and *winrm* methods.

```terraform
resource "aws_instance" "web" {
  # ...

  # Establishes connection to be used by all
  # generic remote provisioners (i.e. file/remote-exec)
  connection {
    type     = "ssh"
    user     = "root"
    password = var.root_password
    host     = self.public_ip
  }

  provisioner "remote-exec" {
    inline = [
      "puppet apply",
      "consul join ${aws_instance.web.private_ip}",
    ]
  }
}
```

The need to configure a connection when using remote-exec is because Terraform needs information such as the IP address, username, SSH key, or password to establish a direct connection and send commands to the remote machine.

### Creation-Time and Destroy-Time provisioners

The moment in which provisioners are executed can be divided into two ways, they are:

1) **Creation-Time**:
As its name suggests, it refers to any script that must be executed immediately after creating a resource for the first time. For example, when it is necessary to start a service or configure a database as soon as an EC2 instance is created.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    when    = destroy
    command = "echo 'Destroy-time provisioner'"
  }
}
```

*By default, provisioners run when the resource they are defined within is created. Creation-time provisioners are only run during creation, not during updating or any other lifecycle. They are meant as a means to perform bootstrapping of a system*.

2) **Destroy-Time**:
This concept refers to actions you want to take immediately before destroying a resource. For example, you may need to wipe data or disable services before removing an EC2 instance. To do this, we can use the *when* parameter inside the provisioner configuration.

```terraform
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    when    = destroy
    command = "echo 'Destroy-time provisioner'"
  }
}
```













