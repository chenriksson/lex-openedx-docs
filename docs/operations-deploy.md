#Deploying Open edX on Azure

##Requirements
* [Azure subscription](https://azure.microsoft.com/en-us/pricing/purchase-options/)
* [Git](http://www.git-scm.com/download/win)

##Azure Resource Manager (ARM) Templates

###Developer Stack

Developer environment installed on single Ubuntu VM. Running Open edX Dogwood.

* [Deploy](https://azure.microsoft.com/en-us/documentation/templates/openedx-devstack-ubuntu/)
* [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/openedx-devstack-ubuntu)
* [Open edX Docs](https://openedx.atlassian.net/wiki/display/OpenOPS/Running+Devstack)
  
###Full Stack

Production-like environment installed on single Ubuntu VM. Running Open edX Dogwood.

* [Deploy](https://azure.microsoft.com/en-us/documentation/templates/openedx-fullstack-ubuntu/)
* [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/openedx-fullstack-ubuntu)
* [Open edX Docs](https://openedx.atlassian.net/wiki/display/OpenOPS/Running+Fullstack)
  
###Scalable

Production-like environment installed on multiple Ubuntu VMs. Running Open edX Cypress, but migration to Dogwood (and Marketplace) is in progress.

* [Deploy](https://github.com/chenriksson/openedx-azure-scalable)
* [Open edX Docs](https://openedx.atlassian.net/wiki/display/OpenOPS/Running+Fullstack)

*Note: Scalable has a few [issues](https://github.com/appsembler/openedx-azure-scalable/issues) to be aware of.*
  
##Deploying from the Azure Portal

1. Click on one of the ARM template links above.

2. Click the 'Deploy to Azure' button.

  *This opens the Azure portal. Once you are logged in, you should see a 'Custom deployment' blade.*

3. (Optional) Make any template changes. Not recommended, as this could break deployment.

    *i.e., Change Open edX version [variables('openedxVersion')] or Ubuntu version [variables('osImageSKU')]*

4. Enter deployment settings and parameters. Click 'OK' to save.
  
  * **Resource group** - Select 'New'. Resource group name must be unique.
  
  * **Resource group location** - Azure region where template should be deployed.
  
  * **AdminUserName** - Administrator user for SSH access to the VM(s).
  
  * **AdminPassword** - Administrator password for SSH access to the VM(s).
  
  * **DnsLabelPrefix** - DNS prefix for the deployment. Must be unique.
  
  * **VmSize** - Azure VM size. Verify that the size you select is available in the selected 'Resource group location'.
  
     * *See: Azure [Services by Region](https://azure.microsoft.com/en-us/regions/#services)*
    
     * *See: Azure [Linux VM Sizes](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-sizes/)* 

5. Review the legal terms and click 'Create' to deploy.

  *Deployment should finish quickly (1-10 minutes), but Open edX installation may take an hour or longer.*

6. If deployment fails, see [troubleshooting](operations-deploy-troubleshoot.md)

##Post-Deployment

1. Setup [SSH keys](../tutorials/ssh.md) (Scalable template only)

  By default, Open edX installation disables SSH password authentication. To avoid losing access you must setup SSH key access after deployment and before Open edX installation completes.
  
  If you lose access to the VM(s), see: https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess
  
  *Password authentication remains enabled for devstack and fullstack templates, but you can opt to disable it yourself.*

2. Verify [SSH access](../tutorials/ssh.md) to the VM(s)

  *Devstack and fullstack use the default SSH port of 22. Scalable uses port 2222 for app0 VM, 2223 for app1 VM, etc.*

3. (Optional) Monitor the installation log for progress.

  SSH into the VM (app0 VM for scalable) and run the following:
  
    ```sudo tail -f /var/log/azure/openedx-install.log```
 