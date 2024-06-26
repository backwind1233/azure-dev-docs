---
ms.custom: devx-track-js, devx-track-azurecli
ms.topic: include
ms.date: 08/08/2022
---


### Create an Azure Database for PostgreSQL server resource with Azure CLI

Use the following Azure CLI [az postgres server create](/cli/azure/postgres/server#az-postgres-server-create) command in the [Azure Cloud Shell](https://shell.azure.com) to create a new PostgreSQL server resource for your database. 

```azurecli
az postgres server create \
    --subscription YOUR-SUBSCRIPTION-ID-OR-NAME \
    --resource-group YOUR-RESOURCE-GROUP \
    --location eastus \
    --name YOURRESOURCENAME \
    --admin-user YOUR-ADMIN-USER \
    --ssl-enforcement Disabled \
    --enable-public-network Enabled 
```

This command may take a couple of minutes to complete and creates a publicly available resource in the `eastus` region. 

The response includes your server's configuration details including: 
* Autogenerated password for the admin account
* Connection string

Before you can connect to the server, you need to configure your firewall rules to allow your client IP address through. 

### Add a firewall rule for your client IP address to PostgreSQL resource

By default, the firewall rules aren't configured. You should add your client IP address so your client connection to the server with JavaScript is successful.

Use the following Azure CLI [az postgres server firewall-rule create](/cli/azure/postgres/server#az-postgres-server-firewall-rule-create) command in the [Azure Cloud Shell](https://shell.azure.com) to create a new firewall rule for your database. 


```azurecli
az postgres server firewall-rule create \
    --subscription YOUR-SUBSCRIPTION-ID-OR-NAME \
    --resource-group YOUR-RESOURCE-GROUP \
    --server YOURRESOURCENAME \
    --name AllowMyIP \
    --start-ip-address 123.123.123.123 \
    --end-ip-address 123.123.123.123
```

If you don't know your client IP address, use one of these methods:
* Use the Azure portal to view and change your firewall rules, which include adding your detected client IP
* Run your Node.js code, the error about your firewall rules violation includes your client IP address

While you can add the full range of internet addresses as a firewall rule, 0.0.0.0-255.255.255.255, this leaves your server open to attacks. 

### Create a PostgreSQL database on the server with Azure CLI

Use the following Azure CLI [az postgres db create](/cli/azure/postgres/db#az-postgres-db-create) command in the [Azure Cloud Shell](https://shell.azure.com) to create a new PostgreSQL database on your server. 

```azurecli
az postgres db create \
    --subscription YOUR-SUBSCRIPTION-ID-OR-NAME \
    --resource-group YOUR-RESOURCE-GROUP \
    --server-name YOURRESOURCENAME \
    --name YOURDATABASENAME
```

### Get the PostgreSQL connection string with Azure CLI

Retrieve the PostgreSQL connection string for this instance with the [az postgres server show-connection-string](/cli/azure/postgres/server#az-postgres-server-show-connection-string) command:

```azurecli
az postgres server show-connection-string \
    --subscription YOUR-SUBSCRIPTION-ID-OR-NAME \
    --server-name YOURRESOURCENAME
```

This returns the connection strings for the popular languages as a JSON object. You need to replace `{database}`, `{username}`, and `{password}` with your own values before using the connection string. Replace `YOURRESOURCENAME` with your resource name.
