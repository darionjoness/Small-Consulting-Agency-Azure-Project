## Create VNET

```
az network vnet create --resource-group rg-contoso-dev-eastus-001 --name vnet-contoso-dev --address-prefixes 10.0.0.0/16 --location eastus --tags Environment=Development
```

## Create Subnets

```
az network vnet subnet create --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --address-prefixes 10.0.1.0/24 --name snet-web
az network vnet subnet create --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --address-prefixes 10.0.2.0/24 --name snet-app
az network vnet subnet create --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --address-prefixes 10.0.3.0/24 --name snet-data
az network vnet subnet create --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --address-prefixes 10.0.4.0/24 --name snet-endpoints
```
## Create NSGs

```
az network nsg create --resource-group rg-contoso-dev-eastus-001 --name nsg-web-dev --tags Environment=Production Tier=Web
az network nsg create --resource-group rg-contoso-dev-eastus-001 --name nsg-app-dev --tags Environment=Production Tier=App
az network nsg create --resource-group rg-contoso-dev-eastus-001 --name nsg-data-dev --tags Environment=Production Tier=Data
az network nsg create --resource-group rg-contoso-dev-eastus-001 --name nsg-endpoints-dev --tags Environment=Production Tier="Private Endpoints"
```
