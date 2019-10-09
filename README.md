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
Now you should be able to see the newly created project. 
![Azure DevOps Create Project!](/assets/azure_devops_6.png "Azure DevOps Create Project")

---
## Configure your Azure DevOps project

### Enabling preview features

1. The first thing you need to do after opening the DevOps project is to enable some features in your profile settings.
To so, at the top right corner, click on the initials of your name (that is your profile), then click on the three dots pointed in the next screenshot and go to 'Preview features'.                         
![Azure DevOps enable features](/assets/azure_devops_10.png "Azure DevOps enable features")  
Make sure you have 'Multi-stage pipelines' and 'New service connections experience' enabled. You can proceed to close that window.                             
![Azure DevOps enable features](/assets/azure_devops_11.png "Azure DevOps enable features")
### Creating a service connection
2. Now, you need to create a service connection with your Azure account (so it is possible to deploy the resources). At the the bottom left corner, click on 'Project settings'.    
![Azure DevOps service connection](/assets/azure_devops_12.png "Azure DevOps service connection")     
Then, click on the blue button 'Create service connection' and a floating window will popup". There, select Azure Resource Manager and click on 'Next'.
![Azure DevOps service connection](/assets/azure_devops_13.png "Azure DevOps service connection")
Another window will appear. There, you should configure the connection using your Azure subscription. The connection name *must* be 'Azure', since that is the name used in the YAML pipeline. In 'Scope level' select 'Subscription', then using the dropdown menu, choose the active Azure subscription you want to use. Do not select any specific Resource Group. Finally, make sure you have checked the 'Allow all pipelines to use this connection' box. Click on OK.
![Azure DevOps service connection](/assets/azure_devops_14.png "Azure DevOps service connection")

### Configuring the CI/CD Pipeline

3. On the Azure DevOps site you will find a left panel with different modules. For now, we will concentrate on the 'Pipelines' section.
There already is a pipeline called 'PartsUnlimited'.
![Azure DevOps Pipelines](/assets/azure_devops_7.png "Azure DevOps Pipelines")
After you select the pipeline, you will see at the top right corner an 'Edit' button. Click on that.![Azure DevOps Pipelines](/assets/azure_devops_8.png "Azure DevOps Pipelines")

4. Now, an editable file called _azure-pipelines.yml_ will be opened. The only modification you *must* do is to replace the following variables with a unique name (we suggest appending your name at the end). If you don't do so, the pipeline will fail; this is because those variables are used to name the Azure resources to be deployed. Make sure not to use dashes or undescores, but feel free to use numbers, though. ![Azure DevOps Pipelines](/assets/azure_devops_9.png "Azure DevOps Pipelines")                       
Hit 'Save' and then 'Run'.
5. Now, you can see the pipeline running. There are 5 stages defined in the YAML file.
 ![Azure DevOps Pipelines](/assets/azure_devops_17.png "Azure DevOps Pipelines")
If you click on the pipeline, you will be able to see details for each stage.![Azure DevOps Pipelines](/assets/azure_devops_16.png "Azure DevOps Pipelines")
Also, if you click on any stage, it is possible to see the complete logs for every job.![Azure DevOps Pipelines](/assets/azure_devops_18.png "Azure DevOps Pipelines")
---
## Azure Portal - What has been created

* Go back to the Azure Portal and find the Resource Groups page. There, you should find a resource group with the name you provided when modifying the YAML (it might be something like 'ENDAVAWORKSHOP${YOURNAME}').![Azure Resource Groups](/assets/azure_devops_19.png "Azure Resource Groups")
When you click on the resource group, you will see all the resources deployed with the Pipeline. ![Azure Resources](/assets/azure_devops_20.png "Azure Resources")
### The resources:
* 1 App Service Plan (Standard tier, size Small). This is the computing power (Virtual Machines or servers) that will host the Web App.
* 1 App Service. PaaS for hosting websites. This hosts the production App.
* 2 Deployment slots. Live apps (based on the same App Service) with their own hostnames. One slot is for 'Development' and the other for 'Staging'.
* 3 SQL servers, each with their own SQL database. 
* 3 Application Insights for each environment. APM.

### Browsing the Web App.

Select the App Service Resource. In the overview tab, you can see a button 'Browse'. Click on it and a new tab will be opened. Also, you can see the URL to the left side.  ![Azure Web](/assets/azure_devops_21.png "Azure Web")
Wait a couple of seconds and you will see the Parts Unlimited site live. 
![Website live](/assets/azure_devops_22.png "Website live")

---
## Leveraging more Azure DevOps features

### Configuring Pre-deployment conditions
After the pipeline has successfully run, you will be able to see in the 'Environments' tab (under the _Pipelines_ section) three different environments, defined in the YAML file.  
![Environments](/assets/azure_devops_23.png "Environments")
Select the Production environment to see its run history. You can see more details by clicking on a specific Run. 
Since we want to add a manual pre-deploy approval, click con the three dots on the top right corner and then select 'Checks'.
![Environments](/assets/azure_devops_24.png "Environments")
There, you should see a blue button 'Create'. Click on it and a new floating window will show. In the 'Approvers' bar, type in your name and select it, then click on 'Create' down below.
Now, everytime a new deployment to the Production environment is triggered, you must manually approve it before it is executed (If there are more than one approver,  all the specified approvers must approve for the stage to proceed). 
![Environments](/assets/azure_devops_25.png "Environments")
Do the same for the QA environment. 

### Testing the CI/CD

There is one section we haven explored yet: Repos. There resides the source code for the .NET App (Parts Unlimited) we have been working with. 

Let's edit a line of code and see what happens. Follow the path ``PartsUnlimited-aspnet45/src/PartsUnlimitedWebsite/Views/Home/Index.cshtml``

Click on the 'Edit' button and modify the line 28 to '70%', for example (the idea is to make a noticeable change in the home page). Then, the 'Edit' in the button should have changed to 'Commit' instead. Commit the changes.
![Code](/assets/azure_devops_30.png "Code")

If you go back to the Pipelines section, a new run should be triggered automatically. Remember to approve the deployments to the QA and Production environments when asked. After the pipeline finishes running, the changes should be live. Reload the website page and profit.

### Boards

Azure DevOps also include built-in scrum boards and planning tools to help teams plan, track and discuss work. The project imported, has already been fed with plenty of work items so we can concentrate on how Boards can be used to define an efficient work-flow and to create some useful visualizations to monitor the project.
Let's take a look at the 'Boards' tab. 
![Boards](/assets/azure_devops_26.png "Boards")
In this kanban board, you will be able to drag-and-drop work items to different stages and statuses. You can click on each item to see further details and configure more options (priority, effort, state, description, etc.). You can also comment, follow the item to get notify of any update, among many other options.

For monitorying purposes, you can create insightful visualizations like the following, just by adding and configuring panels and widgets as you like.
![Dashboards](/assets/azure_devops_27.png "Dashboards")

To create or see dashboards, go to the 'Dashboards' tab under the 'Overview' section. You will get a message saying that you don't  have any widgets yet. Click on the 'Add a widget' blue button. Now, proced to draw-and-drop the widgets wherever you like. You can also use the 'Add' button below.

![Dashboards](/assets/azure_devops_28.png "Dashboards")

When you finish adding the new widgets, there might be some of them which require additional configuration. You must select them to open a new window where you can add more details. For example,the 'Chart for Work Items' panel needs attention. Click on it, then select one of the defined Queries and choose one 'Group by' option. Feel free to customize it as you desire.

![Dashboards](/assets/azure_devops_29.png "Dashboards")
