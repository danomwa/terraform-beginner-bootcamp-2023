# Terraform Beginner Bootcamp 2023

### Semantic Versioning :mage:

This project is going to utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)
Given a version number **MAJOR.MINOR.PATCH**, increment the:
 The general format:
 
 **MAJOR.MINOR.PATH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the Terraform CLI

### Considerations with the Teffaform CLI changes
The Teffaform CLI installation instructions have changed due to gpg keyring changes. So we needed to reffer to the lates install CLI instructions via Teffaorm Documentation and change the scripting for install. 

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution 

This project is built against Ubuntu.
Please consider checking your Linux Distribution and change according to you your distribution needs

[How to check OS Version in Linux](
    https://www.cyberciti.biz.faq/
    how-to-check-os-version-in-linux-command-line/
)
### Refactoring into Bash Scripts

While fixing the Terraform CLI gpg depreciation issues, we noticed that the bash script steps were a considerable amoount more code. So we decided to create a bash script to install the Terraform CLI.

This bash script is located here: [./bin/install_terrafor_cli.sh](./bin/install_terraform_cli.sh)

- This will keep the Gitpod Task File tidy.
- This will allow us an easier to debug and execute manually Terraform CLI install
- This will allow better portability for other projects that need to install Terraform CLI 

#### Shebang Considerations

A Shebang (pronounced Sha-bang) tells the bash script what program that will interpret the script eg. `#!/bin/bash`

ChatGPT recommended this format for bash: `#!/usr/bin/env bash`

- for portability for different OS distributions
- will search t eh user's PATH for the bash executable 

#### Executions Considerations
When executiong the bash script we can use the `./` shorthand notation to execute the bash script.

e.g `./bin/install_terraform_cli`

If we are using a script in .gitpod.ym we need to pint the script to a program to interpret it.

eg. `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations
in order to make our bash scripts executable we need to change linux permission for the fix to be dxecutable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```

alternatively:
```sh
chmod 744 ./bin/install_terraform.co
```

### Gitpod Lifecycle (Before, Inin, Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace

### Working with Env Vars

We can list out all Environment Variables (Env Vars) using the `env` command

We can filter specific env vars using grep eg. `env | grep AWS`

#### Setting and Unsetting Env Vars

In the terminal we can set using `export HELLO='world'`

We casn set an env var temporarilly when just running a command 

```sh
HELLO='world' ./bin/pring_message
```

Within a bash script we can set env var without writing export eg 

```sh
#!/usr/bin/ev bash

Hello ='world'

echo $HELLO
```

#### Printing Vars

We can print an env var using echo eg. `echo $HELLO`

#### Scping of Env Vars

When you open a new bash terminals in VSCode it will not be aware of env vars that you have set in another window.

If you want to Env Vars to persist across all future bash terminals that are open you need to set env vars in your bash profile. eng. `.bash_provile`

#### Persisting Env Vars in Gitpod

We can persist env vars into gitpd by storing them in Gitpod Secrets Storage.

```
gp env HEELO='world'
```

All future workspaces launched will set the env vars for all bash terminals opende in those workspaces.

You can also set env vars in the `.gitpod.yml` but this can only contain non sensitive info

### AWS CLI Installation

AWS CLI is installed for the project via the bash script [`./bin/install_aws_cli`](./bin/install_aws_cli)

[Getting Started Install (AWS CLI)](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

We can check if our AWS credentials is configured correctly by running the following AWS CLI command: 
```sh
aws sts get-caller-identity
```

If it is successful you should see a json payload return that looks like this:

```json
{
    "UserId": "AIDA3PW6XBS7R5KC5OGXJ",
    "Account": "789667318975",
    "Arn": "arn:aws:iam::789667318975:user/terraform-beginner-bootcamp"
}
```

We'll need to gnerate AWS CLI credetials from IAM users in order to the user AWS CLI

## Terraform Bassics

### Terraform Registry

Terraform sources their providers and modules from the Terraform registry which is located at [registry terraform.io](https://registry.terraform.io/)

- **Providers** is an interface to APIs that will allow you to create resources in terraform.
- **Modules** are a way to make large amount of terraformcode modular, portabe and sharable.

[Random Terraform Provider](https://registry.terraform.io/providers/hashicorp/random)

### Terraform Console

We can see a list of all the Terraform commands by simply typing `terraform`

#### Terraform Init

At the start of a new terraform project we will run `terraform init` to download the binaries for the terraform proiders that we'll use for this project

#### Terraform Plan
`terrafrom plan`

This will generate out a changeset, about the state of our infrastrucure and what will be changed.

We can output this changeset ie. "plan" to be passed to an apply, but often you can just ignore ourputting.

#### Terrafrom Apply
`terrafrom apply`

This will run a plan and pass the changeset to be executed by terraform. Apply should prompt yes or no.

If we want to automatically approve an apply we can provide the auto approve flag eg. `terraform apply --auto-approve`

### Teraform Lock Files

`.terraform.lock.hcl` contains the locked versioning for the provicersor modules that should be used with this project.

The Terraform Lock File **should be committed** to you Version Control System (VSC) eg. Github

### Terraform State Files

`.terraform.tfstate` contains information about the current state of your infrastructure.

This file **should not be commited** to your VCS.

This file can contain sensitive data.

If you lose this file, you lose knowing the state of your infrastrucutre

`.terraform.tfstate.backup` is the previous state files state.

### Terraform Directory

`.terraform` direcroty contains binaries of terraform providers.
