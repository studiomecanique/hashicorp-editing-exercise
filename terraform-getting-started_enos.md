# Getting Started with Terraform

HashiCorp Terraform provides tools for defining and provisioning infrastructure as code (IaC). To create Terraform infrastructure, you define configuration files that represent infrastructure resources. Terraform applies configuration files to your deployment and manages the infrastructure resources they represent. 

This guide introduces the basic commands you need to create and deploy Terraform resources. 

## Prerequisites

- [Terraform.io](https://www.terraform.io/downloads.html)

## Create your working directory

Open the Terraform command-line interface (CLI) and create a working directory for your configuration. 

The following configuration code creates the `terraform-demo` working directory on the local machine:

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

## Create a Terraform configuration file

Terraform lets you define infrastructure in declarative configuration files. You write configuration files in HashiCorp Configuration Language (HCL) using the .tf or JSON.tf file format. Terraform loads the .tf files that you save to your working directory and manages the infrastructure you create. 

From the Terraform CLI, type the following

```shell
$ touch main.tf
```

Add the code to the configuration file you created. 

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

The configuration code includes a provider block that defines a "docker" provider. 

The code also includes declarative definitions for the following infrastructure resources: 

- a "docker_container" type resource named "nginx" 
- a "docker_image" type resource named "nginx"

The container resource will run the "training" instance of the NGINX open-source web server with ingress and egress on port 80. 

## Initialize your working directory

Before Terraform can apply the configuration, you need to initialize the configuration files in your working directory. We recommend that the working directory be set to the root directory of the configuration. 

You can use the [`terraform init`](https://www.terraform.io/docs/commands/init.html) command to initialize the directory. 

```shell
$ terraform init

```
Terraform installs infrastructure providers as plugin components. The plugin for the infrastructure provider you select&mdash;in this case, the AWS Provider (`aws`)&mdash;is downloaded and installed during the initialization process. 

Before continuing, be sure to resolve any errors that occur during the initialization process. 

## Provision your infrastructure

The infrastructure you specify in your configuration file is represented as Terraform resource objects. Use the [`terraform apply`](https://www.terraform.io/docs/commands/apply.html) command to apply the configuration file and provision the infrastructure.

```shell
$ terraform apply
```
Configuration changes can take a few minutes to complete. Terraform displays a notification message after a resource is successfully created.

## Destroy your infrastructure

To remove Terraform-managed infrastructure resources, use the [`terraform destroy`](https://www.terraform.io/docs/commands/destroy.html) command.

```shell
$ terraform destroy
```
You should receive a prompt asking you to confirm the command to destroy. Type `yes`, and press ENTER. 

Terraform destroys the infrastructure resource that you created earlier.

## Next steps

This guide has given you basic information on using HashiCorp Terraform to create and destroy infrastructure resources. You can find much more information by using the following links.

- To learn more about using Terraform, see [Learn to provision infrastructure with HashiCorp Terraform]( https://learn.hashicorp.com/terraform). 

- For detailed information on the Terraform configuration language, see [Configuration Language](https://www.terraform.io/docs/configuration/index.html). 

- For reference information on the commands of the Terraform command-line interface, see [Terraform CLI Documentation](https://www.terraform.io/docs/cli-index.html).

- For information about the Terraform community, including the community forum, bug trackers, and training, see [Community]( https://www.terraform.io/community.html).


