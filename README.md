# Baseball Stats Application Azure App Services

This repo contains an Azure Resource Manager Template to deploy an Azure Web App, Function App, and Storage account to provide the infrastructure for the Sample Baseball Stats Application.

The application demonstrates displaying baseball player salary data stored in Azure Tables.

To get started, you will need to make sure you have an Azure Account and have Azure CLI installed on your machine.  The scripts in this repo were developed on a Windows machine with the Linux Subsystem installed (Ubuntu 18.04), but they could be run on any machine with Azure CLI installed.

Before running any of the commands to deploy these templates you will need to log into Azure using the following command:

```
az login
```

## App Service

### Resources
* App Service Plan
* Azure Web App
* Azure Function App
* Azure Web App

### Parameters

|Parameter Name|Type|Description|
|---|---|---|
|costCenter|string|The value for the cost center tag on each resource.|
|applicationName|string|Name of the Application.|
|storageAccountType|string|The type of Azure Storage Account to deploy. Allowed values are "Standard_LRS", "Standard_GRS", and "Premium_LRS"|
|appServicePlanSize|string|The size of the App Service Plan. Allowed values are "B1", "B2", "B3", "S1", "S2", and "S3".
|appServicePlanCapacity|int|Capacity (number of VMs) of the App Service Plan. Allowed values range from 1-10.|
|websiteGitHubRepoUrl|string|GitHub repo url for the website code.|
|websiteGitHubBranch|string|Branch in the GitHub repo to use for continuous deployment of the website code. Default value: master|
|apiGitHubRepoUrl|string|GitHub repo url for the api code.|
|apiGitHubBranch|string|Branch in the GitHub repo to use for continuous deployment of the api code. Default Value: master|


### App Service Deployment

To deploy the template, run a command similar to the following from the root of this repo:

```
./deploy.sh -i 'rawe - MSDN' -g 'BaseballStatsRG' -n 'BaseballStats' -l 'East US' -t ./template.json -p ./parameters.json
```


Notes: 
* This template adds a connection string as an AppSetting in the Function App to access Azure Storage.
* This template adds an entry into the CORS settings to allow the web app to call the function app using javascript.