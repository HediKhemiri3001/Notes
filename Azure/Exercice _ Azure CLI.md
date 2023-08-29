# Introduction:
Az CLI has the same functionality as Azure PowerShell.

## Sample commands:
As you do more Azure development, you can end up with several resource groups. If you have several items in the group list, you can filter the return values by adding a `--query` option. Try the following command:
Azure CLI

`az group list --query "[?name == '$RESOURCE_GROUP']"`

The query is formatted using JMESPath, which is a standard query language for JSON requests. You can learn more about this powerful filter language at http://jmespath.org/. We also cover queries in more depth in the Manage VMs with the Azure CLI module.

### App service:
The app service is a built in azure service that offers resources needed for the deployment of a Web app, and plans in appservice are tailored pricing points that are customizable to fit with your app's needs, we create these using: 
`az appservice plan create --name $AZURE_APP_PLAN --resource-group $RESOURCE_GROUP --location $AZURE_REGION --sku FREE`
We can see that you specify what resource group you cant the service to be in, the location and the pricing option. To see more pricin options run `az appservice plan create --help` .

### Web	App: 
After creating a plan for our web app, create the web app in the service plan.
The web app service is a further abstraction over the deployment and creation of a simple VM, where the configuration of the web server and installation of necessary software is rid of.
To create a webapp we run : 
`az webapp create --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --plan $AZURE_APP_PLAN`

After creating a web app, azure provides a way to integrate your codebase directly into the newly created website from code hubs such as github, for this we can run a command like :
`az webapp deployment source config --name $AZURE_WEB_APP --resource-group $RESOURCE_GROUP --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration`