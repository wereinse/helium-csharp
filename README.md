# Managed Identity and Key Vault with ASP.NET Core

> Build an ASP.NET Core Web API using Managed Identity, Key Vault, and Cosmos DB that is designed to be deployed to Azure App Service or Azure Kubernetes Service (AKS) as a Docker container

![License](https://img.shields.io/badge/license-MIT-green.svg)
![Docker Image Build](https://github.com/retaildevcrews/helium-csharp/workflows/Docker%20Image%20Build/badge.svg)

This is an ASP.NET Core Web API reference application designed to "fork and code" with the following features:

- Securely build, deploy and run an Azure App Service (Web App for Containers) application
- Securely build, deploy and run an Azure Kubernetes Service (AKS) application
- Use Managed Identity to securely access resources
- Securely store secrets in Key Vault
- Securely build and deploy the Docker container from Azure Container Registry (ACR)
- Connect to and query Cosmos DB
- Automatically send telemetry and logs to Azure Monitor

> Instructions for setting up Key Vault, ACR, Azure Monitor and Cosmos DB are in the Helium [readme](https://github.com/retaildevcrews/helium)

## Prerequisites

- Bash shell (tested on Mac, Ubuntu, Windows with WSL2)
  - Will not work with WSL1
  - Docker commands will not work in Cloud Shell
- .NET Core SDK 3.1 ([download](https://dotnet.microsoft.com/download))
- Docker CLI ([download](https://docs.docker.com/install/))
- Azure CLI ([download](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest))
- Visual Studio Code (optional) ([download](https://code.visualstudio.com/download))

## Setup

- Fork this repo and clone to your local machine
- All instructions assume starting from the root of the repo

## CI-CD using GitHub Actions

Instructions for setting up (or turning off) CI-CD are [here](https://github.com/retaildevcrews/helium/blob/master/docs/CI-CD/GithubActions.md)

## Run the application locally

- The application requires Key Vault and Cosmos DB to be setup per the Helium [readme](https://github.com/retaildevcrews/helium)
- You can run the application locally by using Azure CLI cached credentials

### Validate az CLI works

```bash

# make sure you are logged into Azure
az account show

# if not log in
az login

```

### Run the app

```bash

# make sure you are in the root of the repo then
cd src/app
dotnet restore

# run in the background
# $He_Name is set to the name of your key vault during setup
# this will use Azure CLI cached credentials

dotnet run -- --keyvault-name $He_Name --auth-type CLI &

# test the application
# the application takes about 15 seconds to start

curl http://localhost:4120/healthz/ietf

# Stop the app
fg

# press ctl-c

```

## Build the release container using Docker

> For instructions on building the container with ACR, please see the Helium [readme](https://github.com/retaildevcrews/helium)

```bash

# make sure you are in the root of the repo
# build the image
docker build . -t helium-csharp

# run docker tag and docker push to push to your repo

```

## Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit [Microsoft Contributor License Agreement](https://cla.opensource.microsoft.com).

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
