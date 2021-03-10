## Overview

This page describes how to deploy Enterprise-scale with a custom configuration, including guidance on how to customise the Management Group hierarchy.

In this example, we take a default configuration and make the following changes:

- Create a new custom archetype definition named `customer_online` which will create two Policy Assignments, `Deny-Resource-Locations` and `Deny-RSG-Locations` at the associated scope with a set of pre-configured default parameter values.
- Add a new Management Group for standard workloads using the `customer_online` archetype definition:
  - Management Group ID: `es-online-example-1`
  - Management Group Name: `ES Online Example 1`
  - Parent Management Group ID: `es-landing-zones`
  - Allowed location list: *default*
- Add a new Management Group for geo-restricted workloads using the `customer_online` archetype definition:
  - Management Group ID: `es-online-example-2`
  - Management Group Name: `ES Online Example 2`
  - Parent Management Group ID: `es-landing-zones`
  - Allowed location list: `["eastus"]`

> NOTE: Although only `root_parent_id` is required, we recommend setting `root_id` and `root_name` to something more meaningful. Changing `root_id` will result in the entire deployment to be re-provisioned.

## Example Root Module

To make the code easier to maintain when extending your configuration, we recommend splitting the root module into multiple files. For the purpose of this example, we use the following:

- `lib/archetype_definition_customer_online.json`
- `main.tf`
- `terraform.tf`
- `variables.tf`

**File: `terraform.tf`**

The `terraform.tf` file is used to set the provider configuration, including pinning to a specific version (or range of versions) for the AzureRM Provider. For production use, we recommend pinning to a specific version, and not using ranges.

```hcl
# Configure Terraform to set the required AzureRM provider
# version and features{} block.

terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = ">= 2.34.0"
    }
  }
}

provider "azurerm" {
  features {}
}
```

**File: `variables.tf`**

The `variables.tf` file is used to declare a couple of example variables which are used to customise deployment of this root module. Defaults are provided for simplicity, but these should be replaced or over-ridden with values suitable for your environment.

```hcl
# Use variables to customise the deployment

variable "root_id" {
  type    = string
  default = "es"
}

variable "root_name" {
  type    = string
  default = "Enterprise-Scale"
}
```

**File: `main.tf`**

The `main.tf` file contains the `azurerm_client_config` resource, which is used to determine the Tenant ID from your user connection to Azure. This is used to ensure the deployment will target your `Tenant Root Group` by default.

It also contains the module declaration for this module, containing a number of customisations as needed to meet the specification defined in the overview above.

To allow the declaration of custom templates, you must create a custom library folder within the root module and include the path to this folder using the `library_path` variable within the module configuration.

> NOTE: For more information regarding configuration of this module, please refer to the [Module Variables](./%5BUser-Guide%5D-Module-Variables) documentation.

```shell
# Get the current client configuration from the AzureRM provider.
# This is used to populate the root_parent_id variable with the
# current Tenant ID used as the ID for the "Tenant Root Group"
# Management Group.

data "azurerm_client_config" "current" {}

# Declare the Terraform Module for Cloud Adoption Framework
# Enterprise-scale and provide a base configuration.

module "enterprise_scale" {
  source  = "Azure/caf-enterprise-scale/azurerm"
  version = "0.1.0"

  root_parent_id = data.azurerm_client_config.current.tenant_id
  root_id        = var.root_id
  root_name      = var.root_name
  library_path   = "${path.root}/lib"

  custom_landing_zones = {
    "${var.root_id}-online-example-1" = {
      display_name               = "${upper(var.root_id)} Online Example 1"
      parent_management_group_id = "${var.root_id}-landing-zones"
      subscription_ids           = []
      archetype_config = {
        archetype_id   = "customer_online"
        parameters     = {}
        access_control = {}
      }
    }
    "${var.root_id}-online-example-2" = {
      display_name               = "${upper(var.root_id)} Online Example 2"
      parent_management_group_id = "${var.root_id}-landing-zones"
      subscription_ids           = []
      archetype_config = {
        archetype_id   = "customer_online"
        parameters     = {
          Deny-Resource-Locations = {
            listOfAllowedLocations = jsonencode([
              "eastus",
            ])
          }
          Deny-RSG-Locations = {
            listOfAllowedLocations = jsonencode([
              "eastus",
            ])
          }
        }
        access_control = {}
      }
    }
  }

}
```

**File: `lib/archetype_definition_customer_online.json`**

The `lib/archetype_definition_customer_online.json` file contains a custom "archetype definition". This is a custom JSON format used specifically by the Terraform Module for Cloud Adoption Framework Enterprise-scale.

In this example, we are using this archetype definition to create an archetype called `customer_online`. This archetype definition includes the creation of Policy Assignments for `Deny-Resource-Locations` and `Deny-RSG-Locations`, with default values pre-defined in the archetype definition template.

For more details about working with archetype definitions, please refer to the [archetype definition user guide](./%5BUser-Guide%5D-Archetype-Definitions).

```json
{
    "customer_online": {
        "policy_assignments": [
            "Deny-Resource-Locations",
            "Deny-RSG-Locations"
        ],
        "policy_definitions": [],
        "policy_set_definitions": [],
        "role_definitions": [],
        "archetype_config": {
            "parameters": {
                "Deny-Resource-Locations": {
                    "listOfAllowedLocations": [
                        "eastus",
                        "eastus2",
                        "westus",
                        "northcentralus",
                        "southcentralus"
                    ]
                },
                "Deny-RSG-Locations": {
                    "listOfAllowedLocations": [
                        "eastus",
                        "eastus2",
                        "westus",
                        "northcentralus",
                        "southcentralus"
                    ]
                }
            },
            "access_control": {}
        }
    }
}
```