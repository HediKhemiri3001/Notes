# Introduction:
An ARM template is a JSON file that acts as the medium for IaC, it describes the configuration for a deplyment in a declarative way, meaning you just have to describe the state you want your deployment to be in, without having to go through the process of writing the imperative commmands to reach that state. an ARM template (Azure Resource Manager Template) is interpreted by Azure Resource Manager which handles everything for your deployment to reach that desired state.

# Benefits:
The benefits of ARM templates is being able to preserve them in a version control system, meaning each version of a codebase could have its specific template and so the deployment would be meant for that codebase and instant. It get rid of all manual labour and so makes CI/CD way easier to implement.
ARM templates are idempotent, which means you can deploy the same template many times and get the same resource types in the same state.
## Documentation on benefits :
Resource Manager orchestrates the deployment of the resources so they're created in the correct order. When possible, resources will also be created in parallel, so ARM template deployments finish faster than scripted deployments.

A mapping of the template processing procedure showing that there's only one call to process a template as opposed to several calls to process scripts.

Resource Manager also has built-in validation. It checks the template before starting the deployment to make sure the deployment will succeed.

If your deployments become more complex, you can break your ARM templates into smaller, reusable components. You can link these smaller templates together at deployment time. You can also nest templates inside other templates.

In the Azure portal, you can review your deployment history and get information about the state of the deployment. The portal displays values for all parameters and outputs.

You can also integrate your ARM templates into continuous integration and continuous deployment (CI/CD) tools like Azure Pipelines, which can automate your release pipelines for fast and reliable application and infrastructure updates. By using Azure DevOps and ARM template tasks, you can continuously build and deploy your projects.

# ARM File structure:
| Element | Description |
|----|-----|
| schema | A required section that defines the location of the JSON schema file that describes the structure of JSON data. The version number you use depends on the scope of the deployment and your JSON editor. |
| contentVersion | A required section that defines the version of your template (such as 1.0.0.0). You can use this value to document significant changes in your template to ensure you're deploying the right template. |
| apiProfile | An optional section that defines a collection of API versions for resource types. You can use this value to avoid having to specify API versions for each resource in the template. |
| parameters | An optional section where you define values that are provided during deployment. These values can be provided by a parameter file, by command-line parameters, or in the Azure portal. |
| variables | An optional section where you define values that are used to simplify template language expressions. |
| functions | An optional section where you can define user-defined functions that are available within the template. User-defined functions can simplify your template when complicated expressions are used repeatedly in your template. |
| resources | A required section that defines the actual items you want to deploy or update in a resource group or a subscription. |
| output | An optional section where you specify the values that will be returned at the end of the deployment. |

# Deploy a template:
To deploy a template using Azure CLI or Azure Powershell, we go by the following steps:
1. Sign in into Azure using `az login` or `Connect-AzAccount`
2. Define a resource group, we can create a new one or use an already existing one.
> To define a location default we can use for Azure CLI : `az configure --defaults location=<location>`
3. Start the template deployment, for this we use : 
```sh
templateFile="{provide-the-path-to-the-template-file}"
az deployment group create \
  --name blanktemplate \
  --resource-group myResourceGroup \
  --template-file $templateFile
```
or for Powershell :
```pwsh
$templateFile = "{provide-the-path-to-the-template-file}"
New-AzResourceGroupDeployment `
  -Name blanktemplate `
  -ResourceGroupName myResourceGroup `
  -TemplateFile $templateFile
```

# Adding resources to the template:
For this you need to know what is the resource provider and what is the resource type, for example, to add a storage account to the template, the type of the resource would be `"Microsoft.Storage/storageAccounts"`, the extensive list is listed [Here](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).
# Example template:
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {},
  "variables": {},
  "functions": [],
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-06-01",
      "name": "learntemplatestorage123",
      "location": "westus",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }
  ],
  "outputs": {}
}
```

# Exercice : Deploy an ARM template:
For this we created a new json file, opened it using VSCode, with the help of the ARM template snippets extension, we created the base skeleton of the template file, then deployed it as described above, and then added to it a storage account and created another deployment for the new storage account ressource.
# ARM template parameters:
ARM templates allow you to use parameters in deployments to make files reusable and eliminate the habit of hardcoding every thing, these parameters can be set from the command line or using parameter files. Use parameters for settings that vary according to the environment; for example, SKU, size, or capacity. 
Basic structure of a parameter object: 
```json
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [
      "<array-of-allowed-values>"
    ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the-parameter>"
    }
  }
}
```
The allowed types of parameters are:
 - string  
 - secureString : used mainly for credential strings
 - integers
 - boolean
 - object
 - secureObject : used mainly for critical information
 - array
Template parameters with secureString or secureObject types can't be read or harvested after the deployment of the resource.
When deploying a parameterized template file, we specify it as such: 
```sh
az deployment group create \
  --name testdeployment1 \
  --template-file $templateFile \
  --parameters storageAccountType=Standard_LRS
```
# ARM template outputs:
Outputs are used when you want to retrieve information after a deployment is succesful, for example retrieve the created endpoint address or something like that.
Basic output object:
```json
"outputs": {
  "<output-name>": {
    "condition?": "<boolean-value-whether-to-output-value>",
    "type": "<type-of-output-value>",
    "value?": "<output-value-expression>",
    "copy?": {
      "count": <number-of-iterations>,
      "input": <values-for-the-variable>
    }
  }
}
// ? indicates that its optional
```
Example : 
```json
"outputs": {
  "storageEndpoint": {
    "type": "object",
    "value": "[reference('learntemplatestorage123').primaryEndpoints]"
  }
}
//reference gets the runtime state of the specified resource
```



