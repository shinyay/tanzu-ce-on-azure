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

Record its Application (client) ID value, which is a GUID.

- [Application ID](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

Record Subscriotion ID

- [Subscription ID](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)

|ID|Command|
|--|-------|
|Tenant ID|az account list \| jq -r '.[].tenantId'|
|Subscription ID|az account list \| jq -r '.[].id'|
|Client ID|az ad app list --display-name shinyay-tce --only-show-errors \| jq -r '.[].appId'|
|Client Secret Value|az ad app credential reset --only-show-errors --id (az ad app list --display-name shinyay-tce --only-show-errors \| jq -r '.[].appId') \| jq -r '.password'|
|Client Secert ID|az ad app list --display-name shinyay-tce --only-show-errors \| jq -r '.[].passwordCredentials[].keyId'|

Assign a Role

- `Subscription` > `Access Control (IAM)`
- `Add role assignment`
  - `Owner` role
  - Leave Assign access to selection as `Azure AD user, group, or service principal`
  - Selected Members `shinyay-tce`

Add a Client Secret for Application

- `Azure Active Directory` > `App Registrations` > `shinyay-tce` > `Certificates & secret` > `Client secrets`

### Accept the Base Image License

To run management cluster VMs on Microsoft Azure, accept the license for their base Kubernetes version and machine OS.

```shell
set -x AZURE_TENANT_ID (az account list | jq -r '.[].tenantId')
set -x AZURE_CLIENT_ID (az ad app list --display-name shinyay-tce --only-show-errors | jq -r '.[].appId')
set -x AZURE_CLIENT_SECRET (az ad app credential reset --only-show-errors --id (az ad app list --display-name shinyay-tce --only-show-errors | jq -r '.[].appId') | jq -r '.password')
set -x AZURE_SUBSCRIPTION_ID (az account list | jq -r '.[].id')
```

```shell
az login --service-principal --username $AZURE_CLIENT_ID --password $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
```

Accept the license for **Kubernetes version 1.21 and the machine OS, Ubuntu 20.04**

```shell
az vm image terms accept --publisher vmware-inc --offer tkg-capi --plan k8s-1dot21dot5-ubuntu-2004 --subscription $AZURE_SUBSCRIPTION_ID
```

### Create an SSH Key Pair

```shell
ssh-keygen -t rsa -b 4096 -C "email@example.com"
```

Enter and repeat a password for the key pair

Add the private key to the SSH agent running on your machine

```shell
ssh-add ~/.ssh/id_rsa
```

### Deploy a Management Cluster to Azure

```shell
tanzu management-cluster create shinyay-tce-mgmt --file config.yaml -v 6
```

### Start the Installer in your Browser

Confirm the environment variables for the TCE Installation

```shell
echo "AZURE_TENANT_ID: $AZURE_TENANT_ID"
echo "AZURE_CLIENT_ID: $AZURE_CLIENT_ID"
echo "AZURE_CLIENT_SECRET: $AZURE_CLIENT_SECRET"
echo "AZURE_SUBSCRIPTION_ID: $AZURE_SUBSCRIPTION_ID"
echo "SSH_PUBLICK_KEY: $(cat ~/.ssh/id_rsa.pub)"
```

Run the installation ui

```shell
tanzu management-cluster create --ui
```

![installer](https://user-images.githubusercontent.com/3072734/169016196-434da479-8702-49b6-9ee4-bcea107da8cd.png)

#### Step 1: IaaS Provider

#### Step 2: Management Cluster Settings

#### Step 3: Metadata

#### Step 4: Kubernetes Network

#### Step 5: Identity Management

#### Step 6: OS Image

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

[shinyay](https://github.com/shinyay)
- twitter: https://twitter.com/yanashin18618
