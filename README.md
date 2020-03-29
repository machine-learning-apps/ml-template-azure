# ML Ops with GitHub Actions and AML

<p align="center">
  <img src="docs/images/aml.png" height="80"/>
  <img src="https://i.ya-webdesign.com/images/a-plus-png-2.png" alt="plus" height="40"/>
  <img src="docs/images/actions.png" alt="Azure Machine Learning + Actions" height="80"/>
</p>

This template can be used for easily setting up a machine learning project with automated training and deployment using [GitHub Actions](https://github.com/features/actions) and [Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/).

## Contents

| File/folder       | Description                                |
|-------------------|--------------------------------------------|
| `src`             | Sample source code.                        |
| `.github/workflows`| Workflow for automated ML training and deployment  |
| `.ml/azure`       | configuration files for azure              |
| `CONTRIBUTING.md` | Guidelines for contributing to the templates. |
| `README.md`       | This README file.                          |
| `LICENSE`         | The license for the sample.                |

## What is MLOps?

<p align="center">
  <img src="docs/images/ml-lifecycle.png" alt="Azure Machine Learning Lifecycle" height="250"/>
</p>

MLOps empowers data scientists and machine learning engineers to bring together their knowledge and skills to simplify the process of going from model development to release/deployment. ML Ops enables you to track, version, test, certify and reuse assets in every part of the machine learning lifecycle and provides orchestration services to streamline managing this lifecycle. This allows practitioners to automate the end to end machine Learning lifecycle to frequently update models, test new models, and continuously roll out new ML models alongside your other applications and services.

This repository enables Data Scientists to focus on the training and deployment code of their machine learning project (`src` folder of this repository). Once new code is checked into the `src` folder of the master branch of this repository the GitHub workflow is triggered and open source Azure Machine Learning actions are used to automatically manage the training through to deployment phases.

## Azure Machine Learning Actions

The template uses the following open source Azure certified Actions:
- Creation of or attachment to an AML Workspace with [azure/aml-workspace](https://github.com/Azure/aml-workspace)
- Managing Azure compute resources with [azure/aml-compute](https://github.com/Azure/aml-compute): 
- Managing Azure Machine Learning experimentation and pipeline runs with [azure/aml-run](https://github.com/Azure/aml-run)
- Model Registration in Azure Machine Learning [azure/aml-registermodel](https://github.com/Azure/aml-registermodel)
- Deployment to Azure Container Instances or Azure Kubernetes Service with [azure/aml-deploy](https://github.com/Azure/aml-deploy)

## Prerequisites

The following prerequisites are required to make this repository work:
- Azure subscription
- Contributor access to the Azure subscription
- Access to the [GitHub Actions](https://github.com/features/actions)

If you don’t have an Azure subscription, create a free account before you begin. Try the [free or paid version of Azure Machine Learning](https://aka.ms/AMLFree) today.

## Getting Started

To get started with the template simply create a repo based off this template to get started.

### Setting up the required secrets

In order to provide actions with the correct credentials for managing AML resources
1. Setup the Azure CLI tool following the [instructions](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) from Azure.
2. Next, open the secrets tab in the settings page of your repository. Add a new secret called **AZURE_CREDENTIALS** and paste the output of `az ad sp create-for-rbac --name <your-sp-name> --role contributor --scopes /subscriptions/<your-subscriptionId>/resourceGroups/<your-rg> --sdk-auth` as the value of secret variable. The JSON should include the following keys: 'tenantId', 'clientId', 'clientSecret' and 'subscriptionId'.

### Modify the code

You will need to modify the code in the <a href="/src">`src` folder</a> with your python code that will train your model. Where required, modify the environment yaml so that the training and deployment environments will have the correct packages for your training and deployment.

### Push your changes to master

Upon pushing the changes to master, actions will kick off your deployment run. Check the actions tab to view if your actions have successfully run. 

### Viewing your AML resources

The log outputs of your action will provide URLs for you to view the resources that have been created in AML.

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
