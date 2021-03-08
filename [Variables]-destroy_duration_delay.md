## Overview

Description: OPTIONAL: Used to tune terraform deploy when faced with errors caused by API caching or eventual consistency. Sets a custom delay period after destruction of the specified resource type.

Default:
```
{
  azurerm_management_group      = "0s"
  azurerm_policy_assignment     = "0s"
  azurerm_policy_definition     = "0s"
  azurerm_policy_set_definition = "0s"
  azurerm_role_assignment       = "0s"
  azurerm_role_definition       = "0s"
}
```

## Usage
_coming soon_