## Create App Service Plan
```
az appservice plan create --name asp-contoso-dev --resource-group rg-contoso-dev-eastus-001 --sku S1 --is-linux --tags Environment=Development
```

## Create Web App
```
az webapp create --name app-contoso-web-123456 --resource-group rg-contoso-dev-eastus-001 --plan asp-contoso-dev --runtime Node:20-lts --tags Environment=Development Application=Website
```
