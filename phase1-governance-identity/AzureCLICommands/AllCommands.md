## Create Resource Groups

```
az group create --name rg-contoso-prod-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

az group create --name rg-contoso-dev-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1002 Project=Contoso-Setup

az group create --name rg-contoso-shared-eastus-001 --location eastus --tags Environment=Production Owner=test@contoso.com CostCenter=CC-1001 Project=Contoso-Setup

```
## Create Custom Role

