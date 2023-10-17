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