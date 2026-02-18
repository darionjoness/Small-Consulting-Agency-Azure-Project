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

## Add NSG Rules for Web Tier

```
az network nsg rule create --resource-group rg-contoso-dev-eastus-001 --nsg-name nsg-web-dev --name Allow-HTTP --priority 100 --direction Inbound --access Allow --protocol Tcp --source-address-prefixes Internet --source-port-ranges "*" --destination-address-prefixes "*" --destination-port-ranges 80
az network nsg rule create --resource-group rg-contoso-dev-eastus-001 --nsg-name nsg-web-dev --name Allow-HTTPS --priority 110 --direction Inbound --access Allow --protocol Tcp --source-address-prefixes Internet --source-port-ranges "*" --destination-address-prefixes "*" --destination-port-ranges 443
```

## Add NSG Rules for App Tier

```
az network nsg rule create --resource-group rg-contoso-dev-eastus-001 --nsg-name nsg-app-dev --name Allow-HTTPS-Web-Tier --priority 100 --direction Inbound --access Allow --protocol Tcp --source-address-prefixes 10.0.1.0/24 --source-port-ranges "*" --destination-address-prefixes "*" --destination-port-ranges 443
```

## Add NSG Rules for Data Tier

```
az network nsg rule create --resource-group rg-contoso-dev-eastus-001 --nsg-name nsg-data-dev --name Allow-HTTPS-App-Tier --priority 100 --direction Inbound --access Allow --protocol Tcp --source-address-prefixes 10.0.2.0/24 --source-port-ranges "*" --destination-address-prefixes "*" --destination-port-ranges 443
```
## Associate NSGs with Subnets

```
az network vnet subnet update --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --name snet-web --network-security-group nsg-web-dev
az network vnet subnet update --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --name snet-app --network-security-group nsg-app-dev
az network vnet subnet update --resource-group rg-contoso-dev-eastus-001 --vnet-name vnet-contoso-dev --name snet-data --network-security-group nsg-data-dev
```
## Create Private DNS Zone and link to Vnet

```
az network private-dns zone create --resource-group rg-contoso-dev-eastus-001 --name contoso.local --tags Environment=Development
az network private-dns link vnet create --resource-group rg-contoso-dev-eastus-001 --zone-name contoso.local --name link-vnet-contoso --virtual-network vnet-contoso-dev --registration-enabled true --tags Environment=Development
```

