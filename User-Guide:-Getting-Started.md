To get started with this module, please take note of the following usage notes:

1. This module requires a minimum `azurerm` provider version of `2.31.1` to support correct operation with Policy Set Definitions. We also recommend using Terraform version `0.13.3` or greater. New releases may contain features which require the minimum versions to be increased, but changes will be clearly documented in the release notes, user guide, and readme.

2. This module has a single mandatory variable `root_parent_id` which is used to set the parent ID to use as the root for deployment. All other variables are optional but can be used to customise your deployment.

3. We recommend providing the `root_parent_id` value needed by the module using one of the following options:
    - Explicitly using an input variable in your root module, with the value specified via command-line using `-var 'root_parent_id={{ tenant_id }}'` or your preferred method of specifying variables at runtime.
    - Implicitly using the `azurerm_client_config` data resource in your root module to extract the `tenant_id` value from the current logged in user context (_see our [examples](./Examples)_).

      > **NOTE:** Using the `azurerm_subscription` data resource to provide a `tenant_id` value from the current context for `root_parent_id` should be avoided. This has been observed to generate a warning that Terraform cannot determine the number of resources to create during the `plan` stage. Terraform will ask to run `terraform apply -target=resource` against the `azurerm_subscription` data resource. This is due to the `root_parent_id` being used within the module to generate values which are used as `keys` within the `for-each` loops for resource creation. To avoid this error, please use one of the recommended methods above.

4. As of version `0.0.8` this module now supports the creation of Role Assignments for any valid Policy Assignment deployed using the module. This feature enumerates the appropriate role(s) needed by the assigned Policy Definition or Policy Set Definition and creates the necessary Role Assignments for the auto-generated Managed Identity at the same scope as the Policy Assignment. This capability provides feature parity with the Azure Portal experience when creating Policy Assignments using the `DeployIfNotExists` or `Modify` effects. If the Policy Assignment needs to interact with resources not under the same scope as the Policy Assignment, you will need to create additional Role Assignments at the appropriate scope.

## Next steps

Learn how to use the [Module Variables](User-Guide%3A-Module-Variables) to customise the module configuration.