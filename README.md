# Endava Azure DevOps Workshop

## Prerequisites
* Azure Account (You can use the 30-day free trial, Visual Studio Professional, etc.)
* _EndavaWorkshop.zip_ from this repository.

## Preparing the Working Environment

1. Login to your [Azure Account](https://portal.azure.com)
2. Go to [Azure DevOps](https://dev.azure.com) and select "Start Free", as follows: 
![Azure DevOps Start Page!](/assets/azure_devops_1.png "Azure DevOps Start Page")
3. Create an organization (if you don't already have one) and name it as you like (It should be a unique name).
![Azure DevOps Create Organization!](/assets/azure_devops_2.png "Azure DevOps Create Organization")
4. Go to the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/?enableextractor=true) and login with the same Microsoft account. _Follow that specific link since it has the query parameter "enableextractor=true" which is necessary to enable the usage of custom templates_.
5. Select the organization you just created, choose a project name and then click on the 'Choose template' button. 
![Azure DevOps Create Project](/assets/azure_devops_3.0.png "Azure DevOps Create Project")
6. In the new window, go to the 'Private' tab. Next, choose GiHub as the source for the template. Then, copy and paste this RAW URL ``https://raw.githubusercontent.com/davismar98/AzureDevOpsWorkshop/master/EndavaWorkshop.zip``. Finally, click on submit.
![Azure DevOps Create Project](/assets/azure_devops_3.1.png "Azure DevOps Create Project")
7. Click on 'Create Project' and wait until it finishes the creation.
![Azure DevOps Create Project](/assets/azure_devops_4.png "Azure DevOps Create Project")
8. When you get the 'Congratulations! Your project is successfully provisioned.' message, you can go back to your Azure DevOps using the blue button. 
![Azure DevOps Create Project!](/assets/azure_devops_5.png "Azure DevOps Create Project")
You should be able to see now the newly created project. 
![Azure DevOps Create Project!](/assets/azure_devops_6.png "Azure DevOps Create Project")

---
## Configure you Azure DevOps project
