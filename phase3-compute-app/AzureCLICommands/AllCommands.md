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

