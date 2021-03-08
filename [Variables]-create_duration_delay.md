## Overview

[**create_duration_delay**][this_page] `map(string)`

Description: OPTIONAL: Used to tune terraform apply when faced with errors caused by API caching or eventual consistency. Sets a custom delay period after creation of the specified resource type.

Default:
```
{
  azurerm_management_group      = "30s"
  azurerm_policy_assignment     = "30s"
  azurerm_policy_definition     = "30s"
  azurerm_policy_set_definition = "30s"
  azurerm_role_assignment       = "0s"
  azurerm_role_definition       = "60s"
}
```

## Usage
_coming soon_

 [//]: # (************************)
 [//]: # (INSERT LINK LABELS BELOW)
 [//]: # (************************)

[this_page]: # "Link for the current page."