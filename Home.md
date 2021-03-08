# Terraform Module for Cloud Adoption Framework Enterprise-scale

The [Terraform Module for Cloud Adoption Framework Enterprise-scale][terraform-registry-caf-enterprise-scale] provides an opinionated approach for delivering the core platform capabilities needed to start building Azure landing zones using Terraform. This module deploys the foundations of the [Cloud Adoption Framework enterprise-scale landing zone architecture][ESLZ-Architecture], with a focus on the central resource hierarchy and governance:

![Enterprise-scale Landing Zone Architecture][ESLZ-Architecture-Diagram]

The module provides a consistent approach for deploying the following components from the Enterprise-scale critical design areas:

- [Management Group and Subscription organisation][management-group-and-subscription-organization]
  - Create the Management Group resource hierarchy
  - Assign Subscriptions to Management Groups
  - Create custom Policy Assignments, Policy Definitions and Policy Set Definitions (Initiatives)
- [Identity and access management][identity-and-access-management]
  - Create custom Role Assignments and Role Definitions

The following resource types are deployed and managed by this module:

|     | Azure Resource | Terraform Resource |
| --- | -------------- | ------------------ |
| Management Groups      | [`Microsoft.Management/managementGroups`][arm_management_group]             | [`azurerm_management_group`][azurerm_management_group]           |
| Policy Assignments     | [`Microsoft.Authorization/policyAssignments`][arm_policy_assignment]        | [`azurerm_policy_assignment`][azurerm_policy_assignment]         |
| Policy Definitions     | [`Microsoft.Authorization/policyDefinitions`][arm_policy_definition]        | [`azurerm_policy_definition`][azurerm_policy_definition]         |
| Policy Set Definitions | [`Microsoft.Authorization/policySetDefinitions`][arm_policy_set_definition] | [`azurerm_policy_set_definition`][azurerm_policy_set_definition] |
| Role Assignments       | [`Microsoft.Authorization/roleAssignments`][arm_role_assignment]            | [`azurerm_role_assignment`][azurerm_role_assignment]             |
| Role Definitions       | [`Microsoft.Authorization/roleDefinitions`][arm_role_definition]            | [`azurerm_role_definition`][azurerm_role_definition]             |

## Next Steps

Check out the [User Guide](./User-Guide), or go straight to our [Examples](./Examples).

 [//]: # (*****************************)
 [//]: # (INSERT IMAGE REFERENCES BELOW)
 [//]: # (*****************************)

[ESLZ-Architecture-Diagram]: media/terraform-caf-enterprise-scale-overview.png "Cloud Adoption Framework Enterprise-scale Landing Zone architecture diagram."

 [//]: # (************************)
 [//]: # (INSERT LINK LABELS BELOW)
 [//]: # (************************)

[ESLZ-Architecture]: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/architecture "Enterprise-scale Reference Architecture"
[terraform-registry-caf-enterprise-scale]: https://registry.terraform.io/modules/Azure/caf-enterprise-scale/azurerm/latest "Terraform Registry: Terraform Module for Cloud Adoption Framework Enterprise-scale"
[management-group-and-subscription-organization]: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/management-group-and-subscription-organization "Cloud Adoption Framework: Management group and subscription organization"
[identity-and-access-management]: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/identity-and-access-management "Cloud Adoption Framework: Identity and access management"

[arm_management_group]:      https://docs.microsoft.com/en-us/azure/templates/microsoft.management/managementgroups
[arm_policy_assignment]:     https://docs.microsoft.com/en-us/azure/templates/microsoft.authorization/policyassignments
[arm_policy_definition]:     https://docs.microsoft.com/en-us/azure/templates/microsoft.authorization/policydefinitions
[arm_policy_set_definition]: https://docs.microsoft.com/en-us/azure/templates/microsoft.authorization/policysetdefinitions
[arm_role_assignment]:       https://docs.microsoft.com/en-us/azure/templates/microsoft.authorization/roleassignments
[arm_role_definition]:       https://docs.microsoft.com/en-us/azure/templates/microsoft.authorization/roledefinitions

[azurerm_management_group]:      https://www.terraform.io/docs/providers/azurerm/r/management_group.html
[azurerm_policy_assignment]:     https://www.terraform.io/docs/providers/azurerm/r/policy_assignment.html
[azurerm_policy_definition]:     https://www.terraform.io/docs/providers/azurerm/r/policy_definition.html
[azurerm_policy_set_definition]: https://www.terraform.io/docs/providers/azurerm/r/policy_set_definition.html
[azurerm_role_assignment]:       https://www.terraform.io/docs/providers/azurerm/r/role_assignment.html
[azurerm_role_definition]:       https://www.terraform.io/docs/providers/azurerm/r/role_definition.html
