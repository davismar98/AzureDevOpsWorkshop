# Endava Azure DevOps Workshop

## Prerequisites
* Azure Account (You can use the 30-day free trial, Visual Studio Professional, etc.)
* _EndavaWorkshop.zip_ from this repository.

## Preparing the Working Environment

1. Login to your [Azure Account](https://portal.azure.com)
2. Go to [Azure DevOps](https://dev.azure.com) and select "Start Free", as follows: 
![Azure DevOps Start Page!](/assets/azure_devops_1.png "Azure DevOps Start Page")
3. Create an organization (if you don't already have one) and name it as you like. [insert image]
4. Go to the [Azure DevOps Demo Generator](https://|azuredevopsdemogenerator.azurewebsites.net/environment/createproject) and login with your account.
5. Select the organization you just created, choose a project name and then click on the 'Choose template' button. Make sure you select the PartsUnlimited-YAML template. Lastly, click on 'Create Project' and wait until it finishes the creation.
6. When you get the 'Congratulations! Your project is successfully provisioned.' message, you can go back to your Azure DevOps tab and reload the page. You should see the newly created project. 

---
## Setting up service connection in Azure DevOps

1. Move to you Azure Portal and select the Terminal in the top right corner. (If this is the first time you use the terminal, you may be asked to create a storage account). Make sure it is in PowerShell mode.

2. Create a Service Principal using the next command: 
``az ad sp create-for-rbac --name http://DevOpsWorkshop`` ![Creation of the SP!](/assets/service_principal.PNG "Creation of the SP")
``az login --service-principal -u <APP_ID> --password <PWD> --tenant <TENANT_ID>``
3. Make a note with the following values because we will be using them later.
* _appID (also referred to as Service Principal Client ID)_
* _password (also referred to as Service Principal Key)_
* _tenant_ (Tenant ID)

4. Create an Azure Service Endpoint in Azure DevOps by clicking on *Project settings* icon at the bottom left of the dashboard panel. Select *Pipelines > Services connections* and then click on *New Service connection*. Now, click on *Azure Resource Manager* from the drop down list. 


---
## Creation of the Infrastructure

1. In the Azure Portal, create a [Web App + SQL](https://portal.azure.com/#create/Microsoft.WebSiteSQLDatabase)

2. Since the name must be unique, you may find it easiest to incorporate your name.
3. Create a new resource group and call it 'EndavaWorkshop'
4. Select 'App Service Plan/Location' and then click on 'Create new'. You can use the same name as you App if you want. Choose a Location available. The pricing tier can be left as default (S1 Standard).
5. Select 'SQL Database' and then click on 'Create a new database'. Name the database 'partsunlimited'. Next, select Target Server and the click on 'Create a new server'; give it a name (again, you can use the same as you App), choose admin credentials and location. After that, you can clik con Select to save the server. Finally, click again on Select to save all database settings.