---
title: Create a resource group using the Azure libraries for Python
description: Use the resource management library in the Azure SDK for Python to create a resource group from Python code.
ms.date: 12/13/2022
ms.topic: conceptual
ms.custom: devx-track-python, py-fresh-zinc
---

# Example: Use the Azure libraries to create a resource group

This example demonstrates how to use the Azure SDK management libraries in a Python script to create a resource group. (The [Equivalent Azure CLI command](#for-reference-equivalent-azure-cli-command) is given later in this article. If you prefer to use the Azure portal, see [Create resource groups](/azure/azure-resource-manager/management/manage-resource-groups-portal).)

All the commands in this article work the same in Linux/macOS bash and Windows command shells unless noted.

## 1: Set up your local development environment

If you haven't already, set up an environment where you can run this code. Here are some options:

[!INCLUDE [create_environment_options](../../includes/create-environment-options.md)]

## 2: Install the Azure library packages

Create a file named *requirements.txt* with the following contents:

:::code language="txt" source="~/../python-sdk-docs-examples/resource_group/requirements.txt":::

Be sure to use these versions of the libraries. Using older versions will result in errors such as "'AzureCliCredential' object has no attribute 'signed_session'."

In a terminal or command prompt with the virtual environment activated, install the requirements:

```cmd
pip install -r requirements.txt
```

## 3: Write code to create a resource group

Create a Python file named *provision_rg.py* with the following code. The comments explain the details:

:::code language="python" source="~/../python-sdk-docs-examples/resource_group/provision_rg.py":::

[!INCLUDE [cli-auth-note](../../includes/cli-auth-note.md)]

### Reference links for classes used in the code

* [AzureCliCredential (azure.identity)](/python/api/azure-identity/azure.identity.azureclicredential)
* [ResourceManagementClient (azure.mgmt.resource)](/python/api/azure-mgmt-resource/azure.mgmt.resource.resourcemanagementclient)

## 4: Run the script

```cmd
python provision_rg.py
```

## 5: Verify the resource group

You can verify that the group exists through the Azure portal or the Azure CLI.

* Azure portal: open the [Azure portal](https://portal.azure.com), select **Resource groups**, and check that the group is listed. If you've already had the portal open, use the **Refresh** command to update the list.

* Azure CLI: use the [az group show](/cli/azure/group#az-group-show) command:

    ```azurecli
    az group show -n PythonAzureExample-rg
    ```

## 6: Clean up resources

```azurecli
az group delete -n PythonAzureExample-rg  --no-wait
```

Run the [az group delete](/cli/azure/group#az-group-delete) command if you don't need to keep the resource group created in this example. Resource groups don't incur any ongoing charges in your subscription, but it's a good practice to clean up any group that you aren't actively using. The `--no-wait` argument allows the command to return immediately instead of waiting for the operation to finish.

You can also use the [`ResourceManagementClient.resource_groups.begin_delete`](/python/api/azure-mgmt-resource/azure.mgmt.resource.resources.v2021_04_01.operations.resourcegroupsoperations#azure-mgmt-resource-resources-v2021-04-01-operations-resourcegroupsoperations-begin-delete) method to delete a resource group from code.

### For reference: equivalent Azure CLI command

The following Azure CLI [az group create](/cli/azure/group#az-group-create) command creates a resource group with tags just like the Python script:

:::code language="azurecli" source="~/../python-sdk-docs-examples/resource_group/provision.cmd":::

## See also

* [Example: List resource groups in a subscription](azure-sdk-example-list-resource-groups.md)
* [Example: Create Azure Storage](azure-sdk-example-storage.md)
* [Example: Use Azure Storage](azure-sdk-example-storage-use.md)
* [Example: Create a web app and deploy code](azure-sdk-example-web-app.md)
* [Example: Create and query a database](azure-sdk-example-database.md)
* [Example: Create a virtual machine](azure-sdk-example-virtual-machines.md)
* [Use Azure Managed Disks with virtual machines](azure-sdk-samples-managed-disks.md)
* [Complete a short survey about the Azure SDK for Python](https://microsoft.qualtrics.com/jfe/form/SV_bNFX0HECjzPWMiG?Q_CHL=docs)
