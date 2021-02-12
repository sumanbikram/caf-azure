The module can be customised using the following variables (_click on each for more details_):

| Variable Name | Description |
| --- | --- |
| [root_parent_id][root_parent_id] | **REQUIRED** The `root_parent_id` is used to specify where to set the root for all Landing Zone deployments. Usually the Tenant ID when deploying the standard Enterprise-scale reference architecture.
| [root_id][root_id] | If specified, will set a custom Name (ID) value for the Enterprise-scale \"root\" Management Group, and append this to the ID for all core Enterprise-scale Management Groups. |
| [root_name][root_name] | If specified, will set a custom Display Name value for the Enterprise-scale \"root\" Management Group. |
| [deploy_core_landing_zones][deploy_core_landing_zones] | If set to true, will include the core Enterprise-scale Management Group hierarchy. |
| [archetype_config_overrides][archetype_config_overrides] | If specified, will set custom Archetype configurations to the default Enterprise-scale Management Groups. |
| [subscription_id_overrides][subscription_id_overrides] | If specified, will be used to assign subscription_ids to the default Enterprise-scale Management Groups. |
| [deploy_demo_landing_zones][deploy_demo_landing_zones] | If set to true, will include the demo \"Landing Zone\" Management Groups. |
| [custom_landing_zones][custom_landing_zones] | If specified, will deploy additional Management Groups alongside Enterprise-scale core Management Groups. |
| [library_path][library_path] | If specified, sets the path to a custom library folder for archetype artefacts. |
| [template_file_variables][template_file_variables] | If specified, provides the ability to define custom template variables used when reading in template files from the library_path. |
| [default_location][default_location] | If specified, will use set the default location used for resource deployments where needed. |

A summary of these variables can also be found on the [Inputs][ESTF-Inputs] tab of the module entry in Terraform Registry.

## Next steps

Now you understand how to customize your deployment using the variables, check out our [Examples](./Examples).

 [//]: # (************************)
 [//]: # (INSERT LINK LABELS BELOW)
 [//]: # (************************)

[ESTF-Inputs]: https://registry.terraform.io/modules/Azure/caf-enterprise-scale/azurerm/latest?tab=inputs "Terraform Registry: Terraform Module for Cloud Adoption Framework Enterprise-scale - Inputs"
[root_parent_id]: ./Variables%3A-root_parent_id "Instructions for how to use the root_parent_id variable."
[root_id]: ./Variables%3A-root_id "Instructions for how to use the root_id variable."
[root_name]: ./Variables%3A-root_name "Instructions for how to use the root_name variable."
[deploy_core_landing_zones]: ./Variables%3A-deploy_core_landing_zones "Instructions for how to use the deploy_core_landing_zones variable."
[archetype_config_overrides]: ./Variables%3A-archetype_config_overrides "Instructions for how to use the archetype_config_overrides variable."
[subscription_id_overrides]: ./Variables%3A-subscription_id_overrides "Instructions for how to use the subscription_id_overrides variable."
[deploy_demo_landing_zones]: ./Variables%3A-deploy_demo_landing_zones "Instructions for how to use the deploy_demo_landing_zones variable."
[custom_landing_zones]: ./Variables%3A-custom_landing_zones "Instructions for how to use the custom_landing_zones variable."
[library_path]: ./Variables%3A-library_path "Instructions for how to use the library_path variable."
[template_file_variables]: ./Variables%3A-template_file_variables "Instructions for how to use the template_file_variables variable."
[default_location]: ./Variables%3A-default_location "Instructions for how to use the default_location variable."