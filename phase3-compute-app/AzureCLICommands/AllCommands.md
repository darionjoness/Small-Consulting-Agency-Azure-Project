## Create App Service Plan
```
az appservice plan create --name asp-contoso-dev --resource-group rg-contoso-dev-eastus-001 --sku S1 --is-linux --tags Environment=Development
```

## Create Web App
```
az webapp create --name app-contoso-web-123456 --resource-group rg-contoso-dev-eastus-001 --plan asp-contoso-dev --runtime Node:20-lts --tags Environment=Development Application=Website
```
## Create Basic Node.js App

```
mkdir -p ~/simple-node-app
cd ~/simple-node-app
```
```
cat << 'EOF' > package.json
{
  "name": "simple-node-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  }
}
EOF
```
```
cat << 'EOF' > server.js
const http = require('http');
const port = process.env.PORT || 8080;

const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello from your Azure App Service! Your Node.js app is running successfully.');
});

server.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
EOF
```
## Zip File and Deploy
```
zip -r deploy.zip .
```
```
az webapp deployment source config-zip --name app-contoso-web-123456 --resource-group rg-contoso-dev-eastus-001 --src deploy.zip
```

## Create Staging Slot
```
az webapp deployment slot create --name app-contoso-web-123456 --resource-group rg-contoso-dev-eastus-001 --slot staging
```

## Enable HTTPS Only
```
az webapp update --resource-group rg-contoso-dev-eastus-001 --name app-contoso-web-123456 --set httpsOnly=true
```
## Create Autoscale Setting
```
az monitor autoscale create --resource-group rg-contoso-dev-eastus-001 --resource asp-contoso-dev --resource-type "Microsoft.Web/serverfarms" --name autoscale-cpu --min-count 1 --max-count 3 --count 1 --tags Environment=Development
```

## Add Scale In and Scale Out Rules
```
az monitor autoscale rule create --resource-group rg-contoso-dev-eastus-001 --autoscale-name autoscale-cpu --scale out 1 --condition "CpuPercentage > 70 avg 10m" --resource-type Microsoft.Web/serverfarms --resource asp-contoso-dev
az monitor autoscale rule create --resource-group rg-contoso-dev-eastus-001 --autoscale-name autoscale-cpu --scale in 1 --condition "CpuPercentage < 30 avg 10m" --resource-type Microsoft.Web/serverfarms --resource asp-contoso-dev
```
## Create Storage Account for Function App
```
az storage account create --resource-group rg-contoso-dev-eastus-001 --name stcontoso123456 --location eastus --sku Standard_LRS --tags Environment=Development
```
## Create Function App
```
az functionapp create --resource-group rg-contoso-dev-eastus-001 --consumption-plan-location eastus --name contoso-func-app-123 --storage-account stcontoso123456 --runtime python --runtime-version 3.10 --os-type linux --tags Environment=Development
```

