## Create Log Analytics Workspace
```
az monitor log-analytics workspace create --resource-group rg-contoso-dev-eastus-001 --name law-contoso --tags Environment=Development
```
## Create App Service Plan to Monitor
```
az appservice plan create --resource-group rg-contoso-dev-eastus-001 --name asp-contoso-monitor --sku B1 --is-linux --tags Environment=Development
```
## Create Web App to Monitor
```
az webapp create --resource-group rg-contoso-dev-eastus-001 --name app-contoso-monitor --plan asp-contoso-monitor --runtime "Node:20-lts" --tags Environment=Development
```
## Create Storage Account For Storage Availability
```
az storage account create --resource-group rg-contoso-dev-eastus-001 --name stcontosomonitor --sku Standard_LRS --kind StorageV2 --tags Environment=Development
```
## Diagnostic Settings
```

```


