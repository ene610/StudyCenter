# Introduction

Azure AI services provides multiple layers of security that you should consider when implementing a solution.

After completing this module, you'll learn how to:

- Consider authentication for Azure AI services.
- Manage network security for Azure AI services.

# Consider authentication

By default, access to Azure AI services resources is restricted by using subscription keys. Management of access to these keys is a primary consideration for security.

## Regenerate keys

You should regenerate keys regularly to protect against the risk of keys being shared with or accessed by unauthorized users. You can regenerate keys using the Azure portal, or using the `az cognitiveservices account keys regenerate` Azure command-line interface (CLI) command.

Each AI service is provided with two keys, enabling you to regenerate keys without service interruption. To accomplish this:

1. If you're using both keys in production, change your code so that only one key is in use. For example, configure all production applications to use key 1.
2. Regenerate key 2.
3. Switch all production applications to use the newly regenerated key 2.
4. Regenerate key 1
5. Finally, update your production code to use the new key 1.

For example, to regenerate keys in the Azure portal, you can do the following:

1. In the Azure portal, go to your resource's Keys and Endpoint pane.
2. Then select **Regenerate Key1** or select **Regenerate Key2**, depending on which one you want to regenerate at the time.

## Protect keys with Azure Key Vault

Azure Key Vault is an Azure service in which you can securely store secrets (such as passwords and keys). Access to the key vault is granted to _security principals_, which you can think of user identities that are authenticated using Microsoft Entra ID. Administrators can assign a security principal to an application (in which case it is known as a _service principal_) to define a _managed identity_ for the application. The application can then use this identity to access the key vault and retrieve a secret to which it has access. Controlling access to the secret in this way minimizes the risk of it being compromised by being hard-coded in an application or saved in a configuration file.

You can store the subscription keys for an AI services resource in Azure Key Vault, and assign a managed identity to client applications that need to use the service. The applications can then retrieve the key as needed from the key vault, without risk of exposing it to unauthorized users.

![Diagram showing Azure AI services credentials retrieved from Azure Key Vault.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/azure-key-vault.png)

## Token-based authentication

When using the REST interface, some AI services support (or even _require_) token-based authentication. In these cases, the subscription key is presented in an initial request to obtain an authentication token, which has a valid period of 10 minutes. Subsequent requests must present the token to validate that the caller has been authenticated.

Tip

When using an SDK, the calls to obtain and present a token are handled for you by the SDK.

## Microsoft Entra ID authentication

Azure AI services supports Microsoft Entra ID authentication, enabling you to grant access to specific service principals or managed identities for apps and services running in Azure.

Note

For more information about authentication options for AI services, see the [AI services documentation](https://learn.microsoft.com/en-us/azure/ai-services/authentication).

There are different ways you can authenticate against Azure AI services using Microsoft Entra ID, including:

### Authenticate using service principals

The overall process to authenticate against Azure AI services using service principals is as follows:

#### Create a custom subdomain

You can create a custom subdomain in different ways including through the Azure portal, Azure CLI, or PowerShell.

For example, you can create a subdomain using PowerShell in the Azure Cloud Shell. To do this, you select your subscription using the following command:

PowerShell

```
Set-AzContext -SubscriptionName <Your-Subscription-Name>
```

Then, you create your Azure AI services resource specifying a custom subdomain by running the following:

PowerShell

```
$account = New-AzCognitiveServicesAccount -ResourceGroupName <your-resource-group-name> -name <your-account-name> -Type <your-account-type> -SkuName <your-sku-type> -Location <your-region> -CustomSubdomainName <your-unique-subdomain-name>
```

Once created, your subdomain name will be returned in the response.

#### Assign a role to a service principal

You've created an Azure AI resource that is linked with a custom subdomain. Next, you assign a role to a service principal.

To start, you'll need to register an application. To do this, you run the following command:

PowerShell

```
$SecureStringPassword = ConvertTo-SecureString -String <your-password> -AsPlainText -Force

$app = New-AzureADApplication -DisplayName <your-app-display-name> -IdentifierUris <your-app-uris> -PasswordCredentials $SecureStringPassword
```

This creates the application resource.

Then you use the **New-AzADServicePrincipal** command to create a service principal and provide your application's ID:

PowerShell

```
New-AzADServicePrincipal -ApplicationId <app-id>
```

Finally, you assign the **Cognitive Services Users** role to your service principal by running:

PowerShell

```
New-AzRoleAssignment -ObjectId <your-service-principal-object-id> -Scope <account-id> -RoleDefinitionName "Cognitive Services User"
```

### Authenticate using managed identities

Managed identities come in two types:

- **System-assigned managed identity**: A managed identity is created and linked to a specific resource, such as a virtual machine that needs to access Azure AI services. When the resource is deleted, the identity is deleted as well.
- **User-assigned managed identity**: The managed identity is created to be useable by multiple resources instead of being tied to one. It exists independently of any single resource.

You can assign each type of managed identity to a resource either during creation of the resource, or after it has already been created.

For example, suppose you have a virtual machine in Azure that you intend to use for daily access to Azure AI services. To enable a system-assigned identity for this virtual machine, first you make sure your Azure account has the [Virtual Machine Contributor role](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles). Then you can run the following command using Azure CLI in the Azure Cloud Shell terminal:

Azure CLI

```
az vm identity assign -g <my-resource-group> -n <my-vm>
```

Then you can grant access to Azure AI services in the Azure portal using the following:

1. Go to the Azure AI services resource you want to grant the virtual machine's managed identity access.
    
2. In the overview panel, select **Access control (IAM)**.
    
3. Select **Add**, and then select **Add role assignment**.
    
4. In the Role tab, select **Cognitive Services Contributor**.
    
    [![A screenshot showing the Add role assignment tab.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/select-contributor-role-small.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/select-contributor-role.png#lightbox)
    
5. In the Members tab, for the Assign access to, select **Managed identity**. Then, select **+ Select members**.
    
    [![A screenshot showing the Select managed identities pane.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/select-managed-identity-small.png)](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/select-managed-identity.png#lightbox)
    
6. Ensure that your subscription is selected in the Subscription dropdown. And for Managed identity, select **Virtual machine**.
    
7. Select your virtual machine in the list, and select **Select**.
    
8. Finally, select **Review + assign** to review, and then **Review + assign** again to finish.
    

Note

For more details on how to configure managed identities including user-managed identities, see [Configure managed identities for Azure resource on Azure VM using Azure CLI](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm)

# Implement network security

Network security is an important measure to ensure unauthorized users can't reach the services that you are protecting. Limiting what users can see is always a great idea, since they can’t compromise what they can’t see.

## Apply network access restrictions

By default, Azure AI services are accessible from all networks. Some individual AI services resources (such as **Azure AI Face service**, **Azure AI Vision**, and others) can be configured to restrict access to specific network addresses - either public Internet addresses or addresses on virtual networks.

![Diagram showing a network configuration for an AI service, restricting access to a range of IP addresses.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/secure-ai-services/media/network-access.png)

With network restrictions enabled, a client trying to connect from an IP address that isn't allowed will receive an **Access Denied** error.

For more information about configuring network access for AI services, see the [AI services documentation](https://learn.microsoft.com/en-us/azure/ai-services/cognitive-services-virtual-networks).

