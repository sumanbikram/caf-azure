## What is an archetype?

Archetypes are used in the Enterprise-scale architecture to describe the Landing Zone configuration using a template-driven approach. The archetype is what fundamentally transforms ***Management Groups*** and ***Subscriptions*** into ***Landing Zones***.

An archetype defines which Azure Policy and Access control (IAM) settings are needed to secure and configure the Landing Zones with everything needed for safe handover to the Landing Zone owner. This covers critical platform controls and configuration items, such as:

- Consistent role-based access control (RBAC) settings
- Guardrails for security settings
- Guardrails for common workload configurations (e.g. SAP, AKS, WVD, etc.)
- Automate provisioning of critical platform resources such as monitoring and networking solutions in each Landing Zone

This approach provides improved autonomy for application teams, whilst ensuring security policies and standards are enforced.

## Working with archetype definitions and the custom library

The `archetype_definition` is a simple template file written in JSON or YAML. The default archetype definitions can be found in the [built-in module library][TFAES-Library], but custom archetype definitions can also be added to a custom library in the root module. The archetype definition is associated to the scope (i.e. Management Group) by specifying the `archetype_id` within the ***Landing Zone*** configuration object.

Both the built-in and custom libraries are also used to store ARM based templates for the Policy Assignments, Policy Definitions, Policy Set Definitions (Initiatives) and Role Definitions. Role Assignments are an exception as these are defined as part of the `archetype_config` instead.

To use a custom library, simply create a folder in your root module (e.g. `/lib`) and tell the module about it using the `library_path` variable (e.g. `library_path = "${path.root}/lib"`). Save your custom templates in the custom library location and as long as they are valid templates for the resource type and match the following naming conventions, the module will automatically import and use them:

| Resource Type | File Name Pattern |
| ------------- | ----------------- |
| Archetype Definitions  | `archetype_definition_*.{json,yml,yaml}`  |
| Policy Assignments     | `policy_assignment_*.{json,yml,yaml}`     |
| Policy Definitions     | `policy_definition_*.{json,yml,yaml}`     |
| Policy Set Definitions | `policy_set_definition_*.{json,yml,yaml}` |
| Role Definitions       | `role_definition_*.{json,yml,yaml}`       |

> The decision to store Policy Assignments, Policy Definitions, Policy Set Definitions (Initiatives) and Role Definitions as native ARM was based on a couple of factors:
>
>- Policies in Terraform require you to understand how to write significant sections of the resource configuration in the native ARM format, and then convert this to a JSON string within Terraform resource.
>- This makes copying these items between ARM templates and Terraform much easier.
>- Terraform doesn't support importing data objects from native Terraform file formats (`.hcl`, `.tf` or `.tfvar`) so we had to use an alternative to be able to support the custom library model for extensibility and customisation.<br>**PRO TIP:** The module also supports YAML for these files as long as they match the ARM schema, although we don't know why you would want to do that!
>

This template driven approach is designed to simplify the process of defining an archetype and forms the foundations for how the module is able to provide feature-rich defaults, whilst also allowing a great degree of extensibility and customisation through the input variables instead of having to fork and modify the module.

The `archetype_definition` template contains lists of the Policy Assignments, Policy Definitions, Policy Set Definitions (Initiatives) and Role Definitions you want to create when assigning the archetype to a Management Group. It also includes the ability to set default values for parameters associated with Policy Assignments, and set default Role Assignments.

To keep the `archetype_definition` template as lean as possible, we simply declare the value of the `name` field from the resource templates (by type). The exception is Role Definitions which must have a GUID for the `name` field, so we use the `roleName` value from `properties` instead.

As long as you follows these patterns, you can create your own archetype definitions to start advanced customisation of your Enterprise-scale deployment.

This template-based approach was chosen to make the desired-state easier to understand, simplify the process of managing configuration and versioning, reduce code duplication (DRY), and to improve consistency in complex environments.

### Example archetype definition

```json
{
    "archetype_id": {
        "policy_assignments": [
          // list of Policy Assignment names
        ],
        "policy_definitions": [
          // list of Policy Definition names
        ],
        "policy_set_definitions": [
          // list of Policy Set Definition names
        ],
        "role_definitions": [
          // list of Role Definition names
        ],
        "archetype_config": {
            "parameters": {
              // map of parameter objects, grouped by Policy Assignment name
            },
            "access_control": {
              // map of Role Assignments to create, grouped by Role Definition name
            }
        }
    }
}
```

### Using the `default_empty` archetype definition

The default library includes a `default_empty` archetype definition which is useful when defining Management Groups which only require Role Assignments, or are being used for logical segregation of Landing Zones under a parent arcehtype. You can assign this to any Landing Zone definition, using the `archetype_config` > `archetype_id` value as per the following `custom_landing_zones` example:

```hcl
  custom_landing_zones = {
    example-landing-zone-id = {
      display_name               = "Example Landing Zone"
      parent_management_group_id = "tf-landing-zones"
      subscription_ids           = []
      archetype_config = {
        archetype_id = "default_empty"
        parameters   = {}
        access_control = {}
      }
    }
  }
```

This is equivalent to creating a standard Management Group without creating any custom Policy Assignments, Policy Definitions, Policy Set Definitions (Initiatives) or Role Definitions.

Role Assignments can be created using the `archetype_config` > `access_control` object within the `custom_landing_zones` instance.

> Note that you still need to provide a full and valid Landing Zone object as per the example above.
