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
## Create Web App Diagnostic Settings
```
az monitor diagnostic-settings create --name diag-webapp --resource $WEBAPP_ID --workspace $LAW_ID --logs '[{"category":"AppServiceHTTPLogs", "enabled":true}, {"category": "AppServiceConsoleLogs", "enabled":true}]' --metrics '[{"category": "AllMetrics","enabled":true}]'
```
## Create Storage Account Diagnostic Settings
```
az monitor diagnostic-settings create --name diag-storage-blob --resource $BLOB_ID --workspace $LAW_ID --metrics '[{"category":"Transaction","enabled":true}]'
```
## Create an Alert Rule if App Service CPU is above 70% for 5 minutes
```
az monitor metrics alert create --name alert-highcpu --resource-group rg-contoso-dev-eastus-001 --scopes $ASP_ID --condition "avg CpuPercentage > 70" --window-size 5m --severity 2 --description "App Service CPU above 70%"
```
## Create an Alert Rule on Web App if Http5xx errors go over 10 in a 5 minute window
```
az monitor metrics alert create --name alert-httperrors --resource-group rg-contoso-dev-eastus-001 --scopes $WEBAPP_ID --condition "total Http5xx > 10" --window-size 5m --severity 1 --description "High number of 5xx errors"
```
## Create an Alert Rule on Storage Account if avg availability is under 99% for 5m send a alert
```
az monitor metrics alert create --name alert-storage-availability --resource-group rg-contoso-dev-eastus-001 --scopes $STORAGE_ID --condition "avg Availability < 99" --window-size 5m --severity 1 --description "Storage availability below 99%"d
```
