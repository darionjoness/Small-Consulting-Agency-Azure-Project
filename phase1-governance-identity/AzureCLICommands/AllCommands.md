## Create Resource Groups

```
az group create --name rg-contoso-prod-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

az group create --name rg-contoso-dev-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1002 Project=Contoso-Setup

az group create --name rg-contoso-shared-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

```
## Create Custom Role

```
{ "Name": "VM Restart + Read Only", "Id": null, "IsCustom": true, "Description": "Allows users to restart virtual machines and view all resources.", "Actions": [ "*/read", "Microsoft.Compute/virtualMachines/restart/action" ], "NotActions": [], "DataActions": [], "NotDataActions": [], "AssignableScopes": [ "/subscriptions/MY_SUBSCRIPTION_ID" ] }
```
```
az role definition create --role-definition @vm-restart-read.json
```

## Create and Assign Policy

```
"if": { "allOf": [ { "field": "type", "notIn": [ "Microsoft.Network/networkSecurityGroups/securityRules", "Microsoft.Resources/deployments" ] }, { "anyOf": [ { "field": "tags.environment", "exists": "false" }, { "field": "tags.environment", "equals": "" } ] } ] }, "then": { "effect": "deny"```
```
```
az policy definition create --name require-environment-tag --rules require-environment-tag.json --description "Require environment tag on all resources" --mode All
az policy assignment create --name requirement-environment-tag --policy require-environment-tag --scope "subscriptions/971823fd-6d9e-4342-945e-70b0f7f54766"
```


