**Portal**

Click: Create Resource

Select: Resource Group (search for 'resource')

*Resource Group*: newport_demo

*Region*: mandatory choice (depends on active policies etc.)

*Tags*: Owner, State, Purpose


**Powershell command**
Click: *Open Cloud Shell*

If asked to configure a storage account for intermediate data, please accept and continue.

Select: 
Once the promt is ready

New-AzResourceGroup -Name "<ResourceGroupName>" -Location "<Region>" -Tag @{Owner="<your e-mail>"; State="Active"; Purpose="Education"}*
