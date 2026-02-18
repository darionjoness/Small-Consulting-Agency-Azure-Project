## Create Resource Groups

```
az group create --name rg-contoso-prod-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

az group create --name rg-contoso-dev-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1002 Project=Contoso-Setup

az group create --name rg-contoso-shared-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

```
## Create Custom Role

```
{ "Name": "VM Restart + Read Only", "Id": null, "IsCustom": true, "Description": "Allows users to restart virtual machines and view all resources.", "Actions": [ "*/read", "Microsoft.Compute/virtualMachines/restart/action" ], "NotActions": [], "DataActions": [], "NotDataActions": [], "AssignableScopes": [ "/subscriptions/971823fd-6d9e-4342-945e-70b0f7f54766" ] }
```
```
az role definition create --role-definition @vm-restart-read.json
```
