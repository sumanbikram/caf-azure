## Overview

[**root_parent_id**][this_page] `string` (required)

Represents an existing Management Group, under which the Enterprise-scale resource hierarchy will be deployed.
Usually this will be the Tenant Root Group, which is the default Management Group referenced by the Tenant ID.

## Default value

None

## Validation

The `root_parent_id` value must be a valid Management Group ID matching the following RegEx:  
`^[a-zA-Z0-9-_\(\)\.]{1,36}$`

## Usage

For a typical deployment, this will be the Tenant ID.

**Example:**

```hcl
  root_parent_id = "9dd91fa3-6367-43be-a321-27c56b855e88"
```

> Tip: In our examples we get the Tenant ID dynamically using [azurerm_client_config](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/client_config) data source.

[//]: # "************************"
[//]: # "INSERT LINK LABELS BELOW"
[//]: # "************************"
[this_page]: # "Link for the current page."
