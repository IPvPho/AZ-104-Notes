[Title]: <> (AZ-104 Notes | TimWarner | PluralSight)

# ***Managing Azure AD Objects***
---
## **Azure AD User Types**
---
### *Cloud Identities*

> - Local Azure Ad
> - External Azure AD

### *Hybrid Identities*

> - Directory-Synchronized *(Local AD Tenant blended with Azure AD)*

### *Guest Identities*

> - Azure Ad B2B Collaboration
> - External Identities

![Azure AD B2B Collaboration](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/media/redemption-experience/invitation-redemption-flow.png)

### *Creating Azure AD User - PowerShell*

> Install-Module -Name AzureAD
> Connect-AzureAD
>
> \$PasswordProfile = New-Object -TypeName
> Microsoft.Open.AzureAD.Model.PasswordProfile
> \$PasswordProfile.Password = "P@ssw0rd8!"
> \$PasswordProfile.EnforcedChangePasswordPolicy = $true
>
> New-AzureADUser -DisplayName "Chris Randall" -PasswordProfile \$PasswordProfile `
> -UserPrincipalName "chris.randall@cdw.com" -AccountEnabled $true

### *Creating Azure AD User - CLI*

> az ad user create --display-name "Chris Randall" \
>    --password "P@$$w0rd13!" --user-principal-name "chris.randall@cdw.com" \
>    --force-change-password-next-login --output-table

### *Azure AD Groups*

> **Security**
> **Microsoft 365**
> **Owners**
> **Memberships**
> > *Assigned Membership*
> > *Dynamic Membership*
> 
> **Group-Assigned Roles & Licenses**

### *Create Azure AD Group - PowerShell*

> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" `
>   -MailEnabled $false -SecurityEnabled \$true -MailNickName "Marketing"
> 
> Add-AzureADGroupMember -ObjectId "xxxxxx-xxxxxx-xxxxxx-xxxxx-xxxxx" `
>   -RefObjectId "yyyyy-yyyyyy-yyyyy-yyyyy-yyyyyy"

### *Create Azure AD Group - CLI*

> az add group create --display0name Sales --mail-nickname Sales
> az ad group member check --group Sales --member-id "xxxxx-xxxxx"
> az ad group member add --group Sales --member-id "xxxxx-xxxxx"

---
## **Administrative Units**
---
> - Azure AD user and group container analogous to Organizational Unit (OU) in local Active Directory
> - Logically organize your Azure AD users and groups
> - Delegate administrative permissions
>    - Password Resets
>    - Enforces least-privilege administration


