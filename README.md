# ARM-templates
This is an example to deploy a storage account, databricks and synapse using one master template which will internally call other ARM templates. 
From within one Azure Resource Manager template, you can link to another template which enables you to decompose your deployment into a set of targeted, purpose-specific templates. 
You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template. 
The Resource Manager service must be able to access the linked template, which means you cannot specify a local file or a file that is only available on your local network for the linked template. You can only provide a URI value that includes either http or https. One option is to place your linked template in a storage account, and use the URI for that item, such as shown below.
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}

In this example we will use a public github repo, that will contain all the ARM templates for deployment.
Check the other files/folders from this directory :
1.	Databricks
2.	storage_account
3.	synapse_sql_pool
4.	maintemplate.json
Copy these files/folders to your github repository.
Check the maintemplate.json file. It is the master file that is calling the other ARM templates using their github URI. Change the Github URI links as required.

Steps to Deploy the downloaded template on Azure.
1.	az login
2.	az account set --subscription your-subscription-id
3.	az configure --defaults group=resource_grouo_name

4. templateFile="maintemplate.json"

5.	cd “/path of the directory containing ARM templates”


6.	#To Validate the deployment before creation
az deployment group validate --name LinkedTemplateDeployment --template-file $templateFile 

7.	#Deploy 
az deployment group create --name LinkedTemplateDeployment --template-file $templateFile 




