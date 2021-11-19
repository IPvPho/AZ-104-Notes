[//]: <> (AZ-104 Notes | Michael Teske | Pluralsight)

# ***Manage Subscriptions and Governance***
---
## **Manage Subscriptions**
---

- You can move resources between subscriptions.
- You can transfer subscriptions between different tenants
- **A single tenant can have multiple subscriptions**

> #### *Types of Subscriptions:*
>
> - Free Trial
> - Support Plan
> - MSDN
> - Visual Studio
> - Pay-As-You-Go
> - Enterprise Agreement (EA)

#### *Management Group Hierarchy*

![Management Group Hierarchy](https://docs.microsoft.com/en-us/azure/architecture/cloud-adoption/_images/governance/mid-market-resource-organization.png)

#### *Configure Cost Management*

>*Azure Cost Management Blade:*
>
> - Analyze costs and tends using **Cost Analysis**
> - **Cost Alerts** can be generated to alert when a threshold you define is met.
> - Apply **Budgets** to apply cost thresholds and limits to control your Azure spend.
> - **Recommendations** displays ways to control costs through identifying trends in your usage.

#### *Apply Resource Tags*

> - Used to organize resources and management hierarchy
> - Tags can be applied to any resource
> - Each tag consist of a name and value pair
> - Must have write access to Microsoft.Resources/tags
> - Tags are NOT inherited from Parents by default
> - Applying tags from PS or AZ CLi will overwrite existing tags by default

![Tagging Decision Guide](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/_images/decision-guides/decision-guide-resource-tagging.png)

---
## **Managing Governance**
---

#### *Azure Subscription Resources:*

- Azure Management Groups 
- Azure Policy


 #### **Azure Management Groups:**
 
> - Used to efficiently manage access, policies and compliance
> - Provides a level of scope over subscriptions
> - Subscriptions within a group inherit policies applied to the group


#### **Root Management Groups**

> - Each directory has a single top-level group called the "Root"
> - Allows for global policies and RBAC assignments at the directory level
> - AD Global Admin needs to elevate to User Access Administrator role
> - Root management group cannot be moved or deleted
> - Nobody is given default access to RMG, have to be given elevated privileges

#### **Azure Policy**

> - Used to create, assign and manage policies in Azure
> - Enforce rules to ensure your resources remain compliant
> - Focuses on resource properties for both new deployments and existing
> - It does not apply remediation to resources that are not compliant


#### **Policy Concepts**

> - A **Policy Definition** is a rule
> - An **Assignment** is an application of an initiative or a policy to a specific scope
> - An **Initiative** is a collection of policy definitions

---
#### **Azure Policy Creation-PowerShell**

```PowerShell
# Get a reference to the resource group that is the scope of the assignment

$rg = Get-AzResourceGroup -Name '<resourceGroupName>'

# Get a reference to the built-in policy definition to assign

$definition = Get-AzPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Audit Vms that do not use managed disks'}

# Create the policy assignment with the built-in definition against your resource group

New-AzPolicyAssignment -Name 'audit-vm-manageddisks' -DisplayName 'Audit VMs without managed disks Assignment' -Scope $rg.ResourceId -PolicyDefinition $definition

```
---
#### *Resource Locks*

> - Each resource can have a lock applied
> - Lock Types include:
>   - *Read-only*
>   - *Delete*
> - Can apply to all resources and resource groups
> - Can be inherited from parent scopes
>   - For both existing and new resources
> - Applies to all users and roles

#### *Applying Resource Locks:*

PowerShell  

```PowerShell
> New-AzResourceLock -LockLevel CanNotDelete -LockName LockSite -ResourceName examplesite
```

Azure CLI

```Bash
> az lock create --name LockGroup --lock-type CanNotDelete --resource-group exampleresourcegroup
```

---
### *Creating and Managing Resource Groups*

> - Resource groups are containers that hold related Azure resources
> - Resources can be moved from one resource group to another if that is supported by that resource
> - Moving resources does not change the location/region where it was originally created
> - Deleting a resource group deletes all resources in that resource group
>  - All resources must have an associated Resource Group


PowerShell
```PowerShell
> New-AzResourceGroup -name example-rg -location eastus2
```

Azure CLI
```Bash
> az group create --name example-rg --location eastus2
```

