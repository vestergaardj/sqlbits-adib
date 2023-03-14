# RESOURCE GROUP 

**Portal**

Click: *Create Resource*
 
Select: *Resource Group* (search for 'resource')

*Resource Group*: newport_demo

*Region*: mandatory choice (depends on active policies etc.)

*Tags*: Owner, State, Purpose


## Powershell command
Click: *Open Cloud Shell*

If asked to configure a storage account for temporary/intermediate data, please accept and continue.

Once the promt is ready

*Type*: New-AzResourceGroup -Name "<ResourceGroupName>" -Location "<Region>" -Tag @{Owner="<your e-mail>"; State="Active"; Purpose="Education"}*
  
Hit return and your new resource group is being created.

To refresh (in Cloud Shell) type:

Get-AzResourceGroup -Name "<ResourceGroupName>"
  
If the resource group has been created, you will see a list of properties of the resource group.
Otherwise you will see an error message similar to: "Provided resource group does not exist" *check your spelling ;)*
  
---

# STORAGE ACCOUNT
  
**Create a Storage Account** 
  *(not used in the following steps, just here for understanding what happens underneath the hood)*
  
Click: Create Resource

Select: Storage Account (search for 'storage')

**Basic** 
 
Select / Create New: Choose existing *Resource Group* or create new
  
Storage Account Name: has to be between 3 and 24 characters or numbers, no blank spaces or special characters. And also, has to be unique across Azure (yes, world wide)

Select Region: Can be independant of the hosting resource group, but not my recommendation.
  
Choose: Standard (HDD) - *cannot be changed afterwards, only by moving data to a new storage account*

Redundency: Locally-redundant Storage (LRS)
  
**Advanced**

Leave everything as is, except:
  
Enable hierarchial namespace: 
 - Check: You want mean to deploy ADLS Gen2
 - Un-check: You mean to deploy regular blob storage
  
**Networking**
  
Leave as is
  
**Data protection**

Leave as is
  
**Encryption**
  
Leave as is
  
**Tags**
  
*Tags*: Owner, State, Purpose
  
**Review**
  
Click: *Create*
