# ADO_KeyVault_Task

Use this Azure template  to download secrets, such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords from an Azure Key Vault instance. This is Node-based and works with agents on Linux, macOS, and Windows.

## Parameters

The pipeline requires the following parameters to be defined:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | ------------- | :-------------: | ------------- |
| armServiceConnection | Azure Resource Manager Service Connection | string |  | | Required |Select the service connection for the Azure subscription containing the Azure Key Vault instance, or create a new connection, Alias: **ConnectedServiceName**|
| KeyVaultName | name of Azure Key Vault | string | | | Required | Key Vault that contains the secrets to download.  |
| SecretsFilter  | Downloads secret names according to the entered value | string | * |  | Required | The value can be the default value to download all secrets from the selected key vault, or a comma-separated list of secret names. |
| RunAsPreJob | Make secrets available to whole job  | boolean | false | true / false | Optional | Runs the task before the job execution begins. Exposes secrets to all tasks in the job, not just tasks that follow this one. |
--------------------------------------------------------------------------------------------------------------------------------------------------

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.

## Use Cases

You can directly call a particular template as per the requirement. for example:

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: NashTech-Labs/ADOAzureKeyVault
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: ADO_KeyVault.yml.yml@Template
    parameters:
      azureSubscription: ${{parameters.armServiceConnection}} 
    KeyVaultName: <vault-name>
    SecretsFilter: 'key1,key2,key3'
    RunAsPreJob: false
       
```

* Note: Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.
