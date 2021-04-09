## Overview

[**deploy_core_landing_zones**][this_page] `bool` (optional)

If set to true, will include the core Enterprise-scale Management Group hierarchy.

## Default value

`"true"`

## Validation

None

## Usage

Deploy the core Enterprise-scale Management Group resources.

**Example:**

```hcl
  deploy_core_landing_zones = false
```

> Important: If set to _false_ after initial deployment, will destroy all core Enterprise-scale Management Group resources.

[//]: # "************************"
[//]: # "INSERT LINK LABELS BELOW"
[//]: # "************************"
[this_page]: # "Link for the current page."
