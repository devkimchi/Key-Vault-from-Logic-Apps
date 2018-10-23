# Key Vault from Logic Apps #

This provides a sample code that [Azure Logic App can access to Key Vault using Managed Identity](https://docs.microsoft.com/en-us/azure/logic-apps/create-managed-service-identity).


## Getting Started ##

The ARM template consists of two resources &ndash; Logic App and Key Vault.


### Deployment through Azure Portal ###

Click the button below to deploy the ARM template through Azure Portal:

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdevkimchi%2FKey-Vault-from-Logic-Apps%2Fmaster%2Fazuredeploy.json" target="_blank">
  <img src="https://azuredeploy.net/deploybutton.png" />
</a>


### Deployment through Azure PowerShell ###

Alternatively, deploy it through Azure PowerShell.

1. Login to Azure Resource Manager through PowerShell.

    ```powershell
    Login-AzureRmAccount
    ```
1. Create a resource group.

    ```powershell
    New-AzureRmResourceGroup `
        -Name "[RESOURCE_GROUP_NAME]" `
        -Location "[LOCATION]"
    ```

1. Update `azuredeploy.parameters.json`.
1. Deploy the ARM template. Once deployed, it will return both Azure Functions application URL and ACI endpoint URL.

    ```powershell
    New-AzureRmResourceGroupDeployment `
        -Name RequestBin `
        -ResourceGroupName "[RESOURCE_GROUP_NAME]" `
        -TemplateFile "azuredeploy.json" `
        -TemplateParameterFile "azuredeploy.parameters.json" `
        -Verbose
    ```


### Key Vault Secret ###

1. Once both Azure resources are ready, [create a secret on the Key Vault instance](https://docs.microsoft.com/en-us/azure/key-vault/quick-create-portal#add-a-secret-to-key-vault).

1. Send an HTTP request to Azure Logic Apps to get the secret value. The request payload is:

    ```json
    {
      "name": "[KEY_VAULT_SECRET_NAME]"
    }
    ```

   If the payload is omitted, all list of secrets will be returned.


## Contribution ##

Your contributions are always welcome! All your work should be done in your forked repository. Once you finish your work with corresponding tests, please send us a pull request onto our `master` branch for review.


## License ##

This is released under [MIT License](http://opensource.org/licenses/MIT)

> The MIT License (MIT)
>
> Copyright (c) 2018 [Dev Kimchi](https://devkimchi.com)
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
