# ML Ops with GitHub Actions and Azure Machine Learning

<p align="center">
  <img src="docs/images/aml.png" height="80"/>
  <img src="https://i.ya-webdesign.com/images/a-plus-png-2.png" alt="plus" height="40"/>
  <img src="docs/images/actions.png" alt="Azure Machine Learning + Actions" height="80"/>
</p>

This template can be used for easily setting up a data science or machine learning project with automated training and deployment using [GitHub Actions](https://github.com/features/actions) and [Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/). For a more comprehensive version of this automated pipeline, see the [aml-template](https://github.com/Azure/aml-template) repository.

## Contents

| File/folder          | Description                                |
| -------------------- | ------------------------------------------ |
| `code`               | Sample data science source code that will be submitted to Azure Machine Learning to train and deploy machine learning models. |
| `.cloud/.azure`      | Configuration files for the Azure Machine Learning GitHub Actions. Please visit the repositories of the respective actions and read the documentation for more details. |
| `.github/workflows`  | Folder for GitHub workflows. The `train_deploy.yml` sample workflow shows you how your can use the Azure Machine Learning GitHub Actions to automate the machine learning process. |
| `docs`               | Resources for this README.                 |
| `CODE_OF_CONDUCT.md` | Microsoft Open Source Code of Conduct.     |
| `LICENSE`            | The license for the sample.                |
| `README.md`          | This README file.                          |
| `SECURITY.md`        | Microsoft Security README.                 |

## What is MLOps?

<p align="center">
  <img src="docs/images/ml-lifecycle.png" alt="Azure Machine Learning Lifecycle" height="250"/>
</p>

MLOps empowers data scientists and machine learning engineers to bring together their knowledge and skills to simplify the process of going from model development to release/deployment. ML Ops enables you to track, version, test, certify and reuse assets in every part of the machine learning lifecycle and provides orchestration services to streamline managing this lifecycle. This allows practitioners to automate the end to end machine Learning lifecycle to frequently update models, test new models, and continuously roll out new ML models alongside your other applications and services.

This repository enables Data Scientists to focus on the training and deployment code of their machine learning project (`code` folder of this repository). Once new code is checked into the `code` folder of the master branch of this repository the GitHub workflow is triggered and open source Azure Machine Learning actions are used to automatically manage the training through to deployment phases.

## Azure Machine Learning GitHub Actions

The template uses the following open source Azure certified Actions:
- Creation of or attachment to an AML Workspace with [azure/aml-workspace](https://github.com/Azure/aml-workspace)
- Managing Azure compute resources with [azure/aml-compute](https://github.com/Azure/aml-compute): 
- Managing Azure Machine Learning experimentation and pipeline runs with [azure/aml-run](https://github.com/Azure/aml-run)
- Model Registration in Azure Machine Learning with [azure/aml-registermodel](https://github.com/Azure/aml-registermodel) and
- Deployment to Azure Container Instances or Azure Kubernetes Service with [azure/aml-deploy](https://github.com/Azure/aml-deploy)

## Getting started

### 1. Prerequisites

The following prerequisites are required to make this repository work:
- Azure subscription
- Contributor access to the Azure subscription
- Access to [GitHub Actions](https://github.com/features/actions)

If you don’t have an Azure subscription, create a free account before you begin. Try the [free or paid version of Azure Machine Learning](https://aka.ms/AMLFree) today.

### 2. Create repository

To get started with ML Ops, simply create a new repo based off this template, by clicking on the green "Use this template" button:

<p align="center">
  <img src="https://help.github.com/assets/images/help/repository/use-this-template-button.png" alt="GitHub Template repository" height="150"/>
</p>

### 3. Setting up the required secrets

Install the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) on your computer or use the Cloud CLI and execute the following command to generate the required credentials:

```sh
# Replace {service-principal-name}, {subscription-id} and {resource-group} with your Azure subscription id and resource group name and any name for your service principle
az ad sp create-for-rbac --name {service-principal-name} \
                         --role contributor \
                         --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                         --sdk-auth
```

This will generate the following JSON output:

```sh
{
  "clientId": "<GUID>",
  "clientSecret": "<GUID>",
  "subscriptionId": "<GUID>",
  "tenantId": "<GUID>",
  (...)
}
```

Add this JSON output as [a secret](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets#creating-encrypted-secrets) with the name `AZURE_CREDENTIALS` in your GitHub repository.

### 4. Define your workspace parameters

You have to modify the parameters in the <a href="/.cloud/.azure/workspace.json">`/.cloud/.azure/workspace.json"` file</a>, so that the GitHub Actions create or connect to the desired Azure Machine Learning workspace. Please use the same value for the `resource_group` parameter that you have used when generating the azure credentials. Change the `name` parameter to the name of your workspace, if you have already created one or choose any name, if you want the Action to create a new workpace in that resource group. You can also delete the parameter, if you want the action to use the default value, which is the repository name. 

### 5. Modify the code

You will need to modify the code in the <a href="/code">`code` folder</a> with your python code that will train your model. Where required, modify the environment yaml so that the training and deployment environments will have the correct packages for your training and deployment.

Upon pushing the changes, actions will kick off your training and deployment run. Check the actions tab to view if your actions have successfully run. 

### 6. Viewing your AML resources and runs

The log outputs of your action will provide URLs for you to view the resources that have been created in AML. Alternatively, you can visit the [Machine Learning Studio](https://ml.azure.com/) to view the progress of your runs, etc.

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

