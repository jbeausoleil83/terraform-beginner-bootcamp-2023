# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This Project utilize Semantic versioning for its tagging
[semver.org](https://semver.org/)


The general format:
 **MAJOR.MINOR.PATCH**, eg. `1.0.1` 

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes
Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.
## Install the Terraform CLI

### Consideration with the Terraform CLI changes
The Terraform CLI Installation Instruction have changed due to gpg keyring changes. So we need refer to the latest install CLI instructions via Trraform Documentation and Change the scripting for install. 

[Install Terrafor cli](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### Considerations for Linux Distribution

This project is built against Ubuntu.
Please consider checking your Linux Distribution and change accordingly to distribution needs.

[How to check OS Version in Linux](
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS Version:
```
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```
### Refactoring into Bash Script

While fixing the Terraform CLI gpg deprecation issues we notice that bash scripts steps were a considerable amount more code. So we decided to create a bash script to install the Terraform CLI.

This bash script is located here: [./bin/install_terraform_cli](./bin/install_terraform_cli)
- This will keep the Gitpod Task File([.gitpod.yml](.gitpod.yml)) tidy.
- This allow us an easier to debug and execute manually Terraform CLI install
- This will allow better portability for other projects that need to install Terraform CLI.


https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/

https://en.wikipedia.org/wiki/Shebang_(Unix)
### Shebang
A Shebang (pronounced Sha-bang) tells the bash script what program that interpret the script. eg.`#!/bin/bash`


ChatGPT recommended this format for bash:
`#!/usr/bin/env bash`
- for portability for different OS distributions
- will search the user's PATH for the bash executable



## Execution Consideration
When executing the bash script we can the `./`shorthand notification to execute the bash script.

https://en.wikipedia.org/wiki/Shebang_(Unix)
eg. `./bin/install_terraform_cli`

If we are using in .gitpod.yml we need to point the script to a program to interpret it.

eg. `source ./bin/install_terraform_cli`

### Linux Permission Considerations

In order to make our bash scripts executable we need tochange linux permission for the fix to be excutable at the user mode.
```sh
chmod u+x ./bin/install_terraform_cli
```


alternatively:

```sh
chmod 744 ./bin/install_terraform_cli
```

https://en.wikipedia.org/wiki/Chmod

### Github Lifecycle (Before,Init,Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

#!/bin/bash


https://www.gitpod.io/docs/configure/workspaces/tasks