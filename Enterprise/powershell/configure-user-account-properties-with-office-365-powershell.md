---
title: "Configure user account properties with Office 365 PowerShell"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- DecEntMigration
- O365ITProTrain
- Ent_Office_Other
- PowerShell
- apr17entnews
ms.assetid: 30813f8d-b08d-444b-98c1-53df7c29b4d7
description: "Summary: Use Office 365 PowerShell to configure properties of individual or multiple user accounts in your Office 365 tenant."
---

# Configure user account properties with Office 365 PowerShell

 **Summary:** Use Office 365 PowerShell to configure properties of individual or multiple user accounts in your Office 365 tenant.
  
Although you can use the Office 365 Admin center to configure properties for the user accounts of your Office 365 tenant, you can also use Office 365 PowerShell and do some things that the Office 365 Admin center cannot.
  
## Before you begin

The procedures in this topic require you to connect to Office 365 PowerShell. For instructions, see [Connect to Office 365 PowerShell](connect-to-office-365-powershell.md).
  
## Change properties for a specific user account

To configure properties for a specific user account, you use the [Set-MsolUser](https://msdn.microsoft.com/library/azure/dn194136.aspx) cmdlet and specify the properties to set or change. This example command changes Belinda Newman's usage location to France:
  
```
Set-MsolUser -UserPrincipalName "BelindaN@litwareinc.onmicosoft.com" -UsageLocation "FR"
```

You identify the account with the **-UserPrincipalName** parameter and set or change specific properties with additional parameters. Here is a list of the most common parameters.
  
- -City "\<city name>"
    
- -Country "\<country name>"
    
- -Department "\<department name>"
    
- -DisplayName "\<full user name>"
    
- -Fax "\<fax number>"
    
- -FirstName "\<user first name>"
    
- -LastName "\<user last name>"
    
- -MobilePhone "\<mobile phone number>"
    
- -Office "\<office location>"
    
- -PhoneNumber "\<office phone number>"
    
- -PostalCode "\<postal code>"
    
- -PreferredLanguage "\<language>"
    
- -State "\<state name>"
    
- -StreetAddress "\<street address>"
    
- -Title "\<title name>"
    
- -UsageLocation "\<2-character country or region code>"
    
    This is the ISO 3166-1 alpha-2 (A2) two-letter country or region code.
    
See [Set-MsolUser](https://msdn.microsoft.com/library/azure/dn194136.aspx) for additional parameters.
  
To see the User Principal Names of all your users, run the following command.
  
```
Get-MSolUser | Sort-Object UserPrincipalName | Select-Object UserPrincipalName | More
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-MsolUser** ) and send it to the next command ( **|** ).
    
- Sort the list of User Principal Names alphabetically ( **Sort-Object UserPrincipalName** ) and send it to the next command ( **|** ).
    
- Display just the User Principal Name property for each account ( **Select-Object UserPrincipalName** ).
    
- Display them one screen at a time ( **More** ).
    
This command will list all of your accounts. If you want to display the User Principal Name for an account based on its display name (first and last name), fill in the **$userName** variable below (removing the \< and > characters), and then run the following commands:
  
```
$userName="<Display name>"
Write-Host (Get-MsolUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

This example displays the User Principal Name for the user named Caleb Sills.
  
```
$userName="Caleb Sills"
Write-Host (Get-MsolUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

By using a **$upn** variable, you can make changes to individual accounts based on their display name. Here is an example of setting Belinda Newman's usage location to France, but specifying her display name rather than her User Principal Name:
  
```
$userName="<Display name>"
$upn=(Get-MsolUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
Set-MsolUser -UserPrincipalName $upn -UsageLocation "FR"
```

## Change properties for all user accounts

To change properties for all users, you can use the combination of the **Get-MsolUser** and **Set-MsolUser** cmdlets. The following example changes the usage location for all users to France:
  
```
Get-MsolUser | Set-MsolUser -UsageLocation "FR"
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-MsolUser** ) and send it to the next command ( **|** ).
    
- Set the user location to France ( **Set-MsolUser -UsageLocation "FR"** ).
    
## Change properties for a specific set of user accounts

To change properties for a specific set of user account, you can use the combination of the **Get-MsolUser**, **Where-Object**, and **Set-MsolUser** cmdlets. The following example changes the usage location for all the users in the Accounting department to France:
  
```
Get-MsolUser | Where-Object {$_.Department -eq "Accounting"} | Set-MsolUser -UsageLocation "FR"
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-MsolUser** ) and send it to the next command ( **|** ).
    
- Find all of the user accounts that have their Department property set to "Accounting" ( **Where-Object {$_.Department -eq "Accounting"}** ) and send the resulting information to the next command ( **|** ).
    
- Set the user location to France ( **Set-MsolUser -UsageLocation "FR"** ).
    
- Display them one screen at a time ( **More** ).
    
## Use the Azure Active Directory V2 PowerShell module to configure user account properties

To configure properties for user accounts with the Azure Active Directory V2 PowerShell module, you use the [Set-AzureADUser](https://docs.microsoft.com/powershell/module/azuread/set-azureaduser?view=azureadps-2.0) cmdlet and specify the properties to set or change. But first, you must connect to your subscription. For the instructions, see [Connect with the Azure Active Directory V2 PowerShell module](https://go.microsoft.com/fwlink/?linkid=842218).
  
### Change properties for a specific user account

This example command changes Belinda Newman's usage location to France:
  
```
Set-AzureADUser -ObjectID "BelindaN@litwareinc.onmicosoft.com" -UsageLocation "FR"
```

You identify the account with the **-ObjectID** parameter and set or change specific properties with additional parameters. Here is a list of the most common parameters.
  
- -Department "\<department name>"
    
- -DisplayName "\<full user name>"
    
- -FacsimilieTelephoneNumber "\<fax number>"
    
- -GivenName "\<user first name>"
    
- -Surname "\<user last name>"
    
- -Mobile "\<mobile phone number>"
    
- -JobTitle "\<job title>"
    
- -PreferredLanguage "\<language>"
    
- -StreetAddress "\<street address>"
    
- -City "\<city name>"
    
- -State "\<state name>"
    
- -PostalCode "\<postal code>"
    
- -Country "\<country name>"
    
- -TelephoneNumber "\<office phone number>"
    
- -UsageLocation "\<2-character country or region code>"
    
    This is the ISO 3166-1 alpha-2 (A2) two-letter country or region code.
    
See [Set-AzureADUser](https://docs.microsoft.com/powershell/module/azuread/set-azureaduser?view=azureadps-2.0) for additional parameters.
  
To display the User Principal Name for your user accounts, run the following command.
  
```
Get-AzureADUser | Sort-Object UserPrincipalName | Select-Object UserPrincipalName | More
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-AzureADUser** ) and send it to the next command ( **|** ).
    
- Sort the list of User Principal Names alphabetically ( **Sort-Object UserPrincipalName** ) and send it to the next command ( **|** ).
    
- Display just the User Principal Name property for each account ( **Select-Object UserPrincipalName** ).
- Display them one screen at a time ( **More** ).
    
This command will list all of your accounts. If you want to display the User Principal Name for an account based on its display name (first and last name), fill in the **$userName** variable below (removing the \< and > characters), and then run the following commands:
  
```
$userName="<Display name>"
Write-Host (Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

This example displays the User Principal Name for the user named Caleb Sills.
  
```
$userName="Caleb Sills"
Write-Host (Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

By using a **$upn** variable, you can make changes to individual accounts based on their display name. Here is an example of setting Belinda Newman's usage location to France, but specifying her display name rather than her User Principal Name:
  
```
$userName="Belinda Newman"
$upn=(Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
Set-AzureADUser -ObjectID $upn -UsageLocation "FR"
```

### Change properties for all user accounts

To change properties for all users, you can use the combination of the **Get-AzureADUser** and **Set-AzureADUser** cmdlets. The following example changes the usage location for all users to France:
  
```
Get-AzureADUser | Set-AzureADUser -UsageLocation "FR"
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-AzureADUser** ) and send it to the next command ( **|** ).
    
- Set the user location to France ( **Set-AzureADUser -UsageLocation "FR"** ).
    
### Change properties for a specific set of user accounts

To change properties for a specific set of user account, you can use the combination of the **Get-AzureADUser**, **Where**, and **Set-AzureADUser** cmdlets. The following example changes the usage location for all the users in the Accounting department to France:
  
```
Get-AzureADUser | Where-Object {$_.Department -eq "Accounting"} | Set-AzureADUser -UsageLocation "FR"
```

This command instructs Office 365 PowerShell to:
  
- Get all of the information on the user accounts ( **Get-AzureADUser** ) and send it to the next command ( **|** ).
    
- Find all of the user accounts that have their Department property set to "Accounting" ( **Where {$_.Department -eq "Accounting"}** ) and send the resulting information to the next command ( **|** ).
    
- Set the user location to France ( **Set-AzureADUser -UsageLocation "FR"** ).
    
## See also

#### 

[Manage user accounts and licenses with Office 365 PowerShell](manage-user-accounts-and-licenses-with-office-365-powershell.md)
  
[Manage Office 365 with Office 365 PowerShell](manage-office-365-with-office-365-powershell.md)
  
[Getting started with Office 365 PowerShell](getting-started-with-office-365-powershell.md)
