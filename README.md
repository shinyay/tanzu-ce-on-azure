![tce-logo](https://tanzucommunityedition.io/img/TCE-logo.svg)

# Getting Started with Tanzu Community Edition on Azure

Tanzu Community Edition is a fully-featured, easy to manage, Kubernetes platform for learners and users.

- [GitHub Repository](https://github.com/vmware-tanzu/community-edition/)

## Description

## Demo

## Features

- feature:1
- feature:2

## Requirement

## Usage

## Installation

### Tanzu CLI

- Prerequisites
  - RAM: 6 GB
  - CPU: 2
  - Docker Desktop for Mac; Version <= 4.2.0
  - Kubectl

Download the binary

```shell
curl -LO https://github.com/vmware-tanzu/community-edition/releases/download/v0.12.0/tce-darwin-amd64-v0.12.0.tar.gz
```

Expand the binary

```shell
tar xvfz tce-darwin-amd64-v0.12.0.tar.gz
```

Install the binary

```shell
./tce-darwin-amd64-v0.12.0/install.sh
```

#### Uninstall the Tanzu CLI

For MacOS

```shell
~/Library/Application Support/tce/uninstall.sh
```

### Azure CLI

For MacOS

Install

```shell
brew update && brew install azure-cli
```

Upgrade

```shell
az upgrade
```

Uninstall

```shell
brew uninstall azure-cli
```

### Register Tanzu Community Edition as a Microsoft Azure Client App

Confirm your Tenant ID

- [Tenant ID](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
  - `Azure Active Directory` > `Your Azure Org` > `Properties` > `Tenant ID`

Regisger Application

- `Azure Active Directory` > `App registrations` > `New registration`

Enter a display name for the app, such as `shinyay-tce`

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

[shinyay](https://github.com/shinyay)
- twitter: https://twitter.com/yanashin18618
