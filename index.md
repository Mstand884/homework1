# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this tutorial, you'll learn how to:

* Install Terraform
* Create and destroy your first Terraform resources

## Prerequisites

Install [Docker](https://www.docker.com/products/docker-desktop)

## Step 1: Install Terraform

To use Terraform, you'll need to install it. To install Terraform using the manual method, find the [appropriate package](https://www.terraform.io/downloads.html) for your system and download it as a zip archive. For this tutorial, we'll be using the Mac or Linux package. This [tutorial](https://learn.hashicorp.com/terraform/getting-started/install) shows how to install Terraform on a different operating system.

After downloading Terraform, unzip the package. Terraform runs as a single binary named `terraform`. Any other files in the package can be safely removed and Terraform will still function. Finally, make sure that the `terraform` binary is available on your `PATH`. This process will differ depending on your [operating system](https://learn.hashicorp.com/terraform/getting-started/install).

Have your terminal print a colon-separated list of locations in your `PATH`.

```$ echo $PATH
```
Move the terraform binary to one of the listed locations. The below command assumes that the binary is currently in your downloads folder and that your PATH includes /usr/local/bin, but you can customize it if your locations are different.

```$ mv ~/Downloads/terraform /usr/local/bin/terraform
```

## Step 2: Verify installation

To verify the installation worked, open a new terminal session to view Terraform's available subcommands.

```$ terraform -help
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.
##...
```
Add any subcommand to `terraform -help` to learn more about what it does and available options.

```terraform -help plan
```

## Step 3: Quick start tutorial

With Terraform installed, you can provision an NGINX server in less than a minute using Docker on Mac, Windows, or Linux.

If you have already installed Docker from the Prerequisites section of this tutorial, you can start Docker Desktop.

```$ open -a Docker
```

Create a directory named `terraform-docker-demo`.

```$ mkdir terraform-docker-demo && cd $_
```

Paste the following Terraform configuration into a file and name it main.tf.

```resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}
```

Initialize Terraform with the `init` command. The AWS provider will be installed.

```shell
$ terraform init
```

Check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take a few minutes to run and will display a message indicating that the resource was created.

![resource created](images/terraform-docker-nginx.png)

To stop the container, run terraform destroy.

```shell
$ terraform destroy
```

A message at the bottom of the output will ask for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.

## Next Steps

To create your first infrastructure in the cloud with Terraform, continue to the [Build Infrastructure guide](https://learn.hashicorp.com/terraform/getting-started/build).
