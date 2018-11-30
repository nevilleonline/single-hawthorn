
STILL IN TEST PHASE

This template creates a single Ubuntu VM and deploys Open edX (Hawthorn) on it.

This Azure Resource Manager (ARM) template was created by a member of the community and not by Microsoft. Each ARM template is licensed to you under a licence agreement by its owner, not Microsoft. Microsoft is not responsible for ARM templates provided and licensed by community members and does not screen for security, compatibility or performance. Community ARM templates are not supported under any Microsoft support programme or service and are made available AS IS without warranty of any kind.
Parameters
Parameter Name 	Description
adminUsername 	Administrator username.
adminPassword 	Administrator password.
dnsLabelPrefix 	DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error.
vmSize 			Virtual machine size.
location 		Location for all resources.

Use the template
PowerShell

New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateUri https://raw.githubusercontent.com/nevilleonline/single-hawthorn/master/azuredeploy.json

Install and configure Azure PowerShell
Command line

azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/nevilleonline/single-hawthorn/master/azuredeploy.json


Open edX Fullstack on Azure

This is an Azure template to create an Ubuntu VM and provision the Open edX fullstack. Open edX fullstack is a single server configuration of all applications

You can learn more about Open edX and fullstack here:

    https://open.edx.org
    https://github.com/edx/edx-platform

This template will complete quickly, but the full Open edX install usually takes > 1 hour. 
To follow along with the progress, ssh into the VM and 

tail -f /var/log/azure/openedx-fullstack-install.log

Getting started with Open edX fullstack

After the install has successfully completed, Supervisor will automatically start LMS (the student facing site) on port 80 and Studio (the course authoing site) on port 18010. Both ports have already been made accessible, so you can simply visit them by opening a browser and navigating to:

    LMS: http://YOUR_INSTANCES_DNS_NAME.cloudapp.azure.com
    Studio: http://YOUR_INSTANCES_DNS_NAME.cloudapp.azure.com:18010

Customizing Open edX fullstack

Many Open edX features can be configured by creating and/or editing the file in /edx/app/edx_ansible/server-vars.yml.

After you have added your customizations, save your file, then run:

/edx/bin/update edx-platform YOUR_EDX_PLATFORMS_BRANCH_NAME

A sample server-vars.yml file has been added to this repo to change the site's title to: "Open edX on Azure."
Customizing Open edX's design

A method for changing the design of Open edX without forking the entire edx-platform repo has been developed by Stanford. You can read more about configuring an Open edX theme and can find the edx-theme repo.

For more info, check the Open edX Github Wiki on managing fullstack
