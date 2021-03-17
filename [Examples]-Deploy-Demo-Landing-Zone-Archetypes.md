## Overview

This page describes how to deploy Enterprise-scale with a starter configuration based mainly on module defaults, including the additional Management Groups used for demonstrating the Enterprise-scale Landing Zone archetypes:

- Corp
- Online
- SAP

These demo Landing Zone archetypes provides a good way to learn about archetypes within the Enterprise-scale architecture but should not be used for production workloads.

> NOTE: Although only `root_parent_id` is required, we recommend setting `root_id` and `root_name` to something more meaningful. Changing `root_id` will result in the entire deployment to be re-provisioned.

## Example Root Module

To keep things simple, the root module for this example is based on a single file:

- `main.tf`

For production deployments, we recommend splitting your root module into multiple files to make the code easier to maintain when extending your configuration.

**File: `main.tf`**

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

# Get the current client configuration from the AzureRM provider.
# This is used to populate the root_parent_id variable with the
# current Tenant ID used as the ID for the "Tenant Root Group"
# Management Group.

data "azurerm_client_config" "current" {}

# Use variables to customise the deployment

variable "root_id" {
  type    = string
  default = "es"
}

variable "root_name" {
  type    = string
  default = "Enterprise-Scale"
}

# Declare the Terraform Module for Cloud Adoption Framework
# Enterprise-scale and provide a base configuration.

module "enterprise_scale" {
  source  = "Azure/caf-enterprise-scale/azurerm"
  version = "0.1.1"

  root_parent_id = data.azurerm_client_config.current.tenant_id
  root_id        = var.root_id
  root_name      = var.root_name

  deploy_demo_landing_zones = true

}
```