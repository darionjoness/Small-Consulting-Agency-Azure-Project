## Create VNET

```
az network vnet create --resource-group rg-contoso-dev-eastus-001 --name vnet-contoso-dev --address-prefixes 10.0.0.0/16 --location eastus --tags Environment=Development
```
