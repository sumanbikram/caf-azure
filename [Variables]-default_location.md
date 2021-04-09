## Overview

[**default_location**][this_page] `string` (optional)

Set the Azure region in which region bound resources will be deployed.
As this is an optional variable, Enterprise-scale location is set by default to`"eastus"`

## Default value

`"eastus"`

## Validation

None

> Important: The default location must be a valid Azure region.

## Usage

Deploy the resources in your Azure region of choice.

**Example:**

```hcl
  default_location = "uksouth"
```

> Tip: Changing this value will cause all location bound resources to be recreated

[//]: # "************************"
[//]: # "INSERT LINK LABELS BELOW"
[//]: # "************************"
[this_page]: # "Link for the current page."
