## Overview

> This page has been published in preparation for the next release, 0.1.0, which will introduce a number of changes which will result in the redeployment of many resources managed by this module.
>
> THIS PAGE IS STILL A WORK IN PROGRESS!

As part of upgrade from release 0.0.8 to 0.1.0, the [Terraform Module for Cloud Adoption Framework Enterprise-scale][terraform-registry-caf-enterprise-scale] has undergone a significant update to the included `Policy Assignments`, `Policy Definitions` and `Policy Set Definitions`.

This update was needed to bring this module up to date with the latest reference architecture published in the [Azure/Enterprise-Scale][Azure/Enterprise-Scale] repository.

## Required actions

Anyone using this module should be aware of the following when planning to upgrade from release 0.0.8 to 0.1.0:

1. Due to the extent of updates, all policies and roles provided as part of this module will be redeployed. Please carefully review the output of `terraform plan` to ensure there are no issues with any custom configuration within your root module.
1. If you are using custom templates, you will need to verify references to policies and roles defined within this module.
1. The following template types will need checking for references to policies and roles as listed in the [Changes](#changes) section below:
   1. Archetype Definitions
   1. Policy Assignments
   1. Policy Set Definitions
1. The list of Policy Assignments deployed by the archetype definitions included with this module have been updated to reflect the Enterprise-scale reference architecture. Please review these before updating your environment to prevent unexpected issues.

## Resource changes

The following changes have been made within the module which may cause issues when using custom archetype definitions:

- All policy and role names have been updated to reflect the names used within the reference [Azure/Enterprise-Scale][Azure/Enterprise-Scale] repository. This means the `ES-` prefix has been removed, and some names have been changed (see lists below).
- All policies and roles are referenced by the `name` field. Previously we referenced the `properties.displayName` field. Please ensure any custom policy and role templates are updated to ensure the correct name is present in the `name` field. This change allows you to set a more user-friendly display name for these resources.
- The following archetype definitions have been updated (details in the [Archetype Definitions](#archetype-definitions-changes) section below):
    - es_root
    - es_landing_zones
    - es_management

### `azurerm_policy_assignment`

| Resource Name (v0.0.8) | Resource Name (v0.1.0) | Notes |
| :--- | :--- | :--- |
| ES-Allowed-Locations | Allow-Resource-Locations | |
| ES-Allowed-RSG-Locations | Allow-RSG-Locations | |
| ES-Deny-AppGW-No-WAF | Deny-AppGW-Without-WAF | |
| | Deny-http-Ingress-AKS" | (new) |
| ES-Deny-VMIPForwarding | Deny-IP-Forwarding | |
| | Deny-Priv-Containers-AKS | (new) |
| | Deny-Priv-Escalation-AKS | (new) |
| ES-Deny-RDPFromInternet | Deny-RDP-From-Internet | |
| ES-Deny-ResourceTypes | Deny-Resource-Types | |
| | Deny-Storage-http | (new) |
| ES-Deny-SubnetWithoutNsg | Deny-Subnet-Without-Nsg | |
| | Deploy-AKS-Policy | (new) |
| ES-Deploy-ASC-Standard | Deploy-ASC-Defender | |
| ES-Deploy-ASC-Monitoring | Deploy-ASC-Monitoring | |
| | Deploy-AzActivity-Log | (new) |
| | Deploy-Log-Analytics | (new) |
| | Deploy-LX-Arc-Monitoring | (new) |
| | Deploy-Resource-Diag | (new) |
| | Deploy-SQL-DB-Auditing | (new) |
| | Deploy-SQL-Security | (new) |
| | Deploy-VM-Backup | (new) |
| | Deploy-VM-Monitoring | (new) |
| | Deploy-VMSS-Monitoring | (new) |
| | Deploy-WS-Arc-Monitoring | (new) |

### `azurerm_policy_definition`

| Resource Name (v0.0.8) | Resource Name (v0.1.0) | Notes |
| :--- | :--- | :--- |
| ES-Append-KV-SoftDelete | Append-KV-SoftDelete | |
| ES-Deny-AA-child-resources | Deny-AA-child-resources | |
| ES-Deny-AppGW-Without-WAF | Deny-AppGW-Without-WAF | |
| ES-Deny-ERPeering | | (moved to built-in) |
| ES-Deny-Private-DNS-Zones | Deny-Private-DNS-Zones | |
| ES-Deny-PublicEndpoint-Aks | Deny-PublicEndpoint-Aks | |
| ES-Deny-PublicEndpoint-CosmosDB | Deny-PublicEndpoint-CosmosDB | |
| ES-Deny-PublicEndpoint-KeyVault | Deny-PublicEndpoint-KeyVault | |
| ES-Deny-PublicEndpoint-MariaDB | Deny-PublicEndpoint-MariaDB | |
| ES-Deny-PublicEndpoint-MySQL | Deny-PublicEndpoint-MySQL | |
| ES-Deny-PublicEndpoint-PostgreSql | Deny-PublicEndpoint-PostgreSql | |
| ES-Deny-PublicEndpoint-Sql | Deny-PublicEndpoint-Sql | |
| ES-Deny-PublicEndpoint-Storage | Deny-PublicEndpoint-Storage | |
| ES-Deny-PublicIP | Deny-PublicIP | |
| | Deny-RDP-From-Internet | (new) |
| ES-Deny-Subnets-Without-NSG | Deny-Subnet-Without-Nsg | |
| ES-Deny-Subnets-Without-UDR | Deny-Subnet-Without-Udr | |
| | Deny-VNET-Peer-Cross-Sub | (new) |
| | Deny-VNet-Peering | (new) |
| ES-Deploy-ASC-ContinuousExportToWorkspace | | (moved to built-in) |
| ES-Deploy-ASC-Standard | Deploy-ASC-Standard | |
| | Deploy-Budget | (new) |
| ES-Deploy-AzureBackup-on-VMs | | (moved to built-in) |
| ES-Deploy-DDoSProtection | Deploy-DDoSProtection | |
| ES-Deploy-Diagnostics-AA | Deploy-Diagnostics-AA | |
| ES-Deploy-Diagnostics-ACI | Deploy-Diagnostics-ACI | |
| ES-Deploy-Diagnostics-ACR | Deploy-Diagnostics-ACR | |
| ES-Deploy-Diagnostics-ActivityLog | Deploy-Diagnostics-ActivityLog | |
| ES-Deploy-Diagnostics-AKS | Deploy-Diagnostics-AKS | |
| ES-Deploy-Diagnostics-AnalysisService | Deploy-Diagnostics-AnalysisService | |
| ES-Deploy-Diagnostics-APIMgmt | Deploy-Diagnostics-APIMgmt | |
| ES-Deploy-Diagnostics-ApplicationGateway | Deploy-Diagnostics-ApplicationGateway | |
| ES-Deploy-Diagnostics-Batch | Deploy-Diagnostics-Batch | |
| ES-Deploy-Diagnostics-CDNEndpoints | Deploy-Diagnostics-CDNEndpoints | |
| ES-Deploy-Diagnostics-CognitiveServices | Deploy-Diagnostics-CognitiveServices | |
| ES-Deploy-Diagnostics-CosmosDB | Deploy-Diagnostics-CosmosDB | |
| | Deploy-Diagnostics-Databricks | (new) |
| ES-Deploy-Diagnostics-DataFactory | Deploy-Diagnostics-DataFactory | |
| ES-Deploy-Diagnostics-DataLakeStore | Deploy-Diagnostics-DataLakeStore | |
| ES-Deploy-Diagnostics-DLAnalytics | Deploy-Diagnostics-DLAnalytics | |
| ES-Deploy-Diagnostics-EventGridSub | Deploy-Diagnostics-EventGridSub | |
| | Deploy-Diagnostics-EventGridSystemTopic | (new) |
| ES-Deploy-Diagnostics-EventGridTopic | Deploy-Diagnostics-EventGridTopic | |
| ES-Deploy-Diagnostics-EventHub | Deploy-Diagnostics-EventHub | |
| ES-Deploy-Diagnostics-ExpressRoute | Deploy-Diagnostics-ExpressRoute | |
| ES-Deploy-Diagnostics-Firewall | Deploy-Diagnostics-Firewall | |
| | Deploy-Diagnostics-FrontDoor | (new) |
| | Deploy-Diagnostics-Function | (new) |
| ES-Deploy-Diagnostics-HDInsight | Deploy-Diagnostics-HDInsight | |
| ES-Deploy-Diagnostics-iotHub | Deploy-Diagnostics-iotHub | |
| ES-Deploy-Diagnostics-KeyVault | Deploy-Diagnostics-KeyVault | |
| ES-Deploy-Diagnostics-LoadBalancer | Deploy-Diagnostics-LoadBalancer | |
| ES-Deploy-Diagnostics-LogicAppsISE | Deploy-Diagnostics-LogicAppsISE | |
| ES-Deploy-Diagnostics-LogicAppsWF | Deploy-Diagnostics-LogicAppsWF | |
| | Deploy-Diagnostics-MariaDB | (new) |
| ES-Deploy-Diagnostics-MlWorkspace | Deploy-Diagnostics-MlWorkspace | |
| ES-Deploy-Diagnostics-MySQL | Deploy-Diagnostics-MySQL | |
| ES-Deploy-Diagnostics-NetworkSecurityGroups | Deploy-Diagnostics-NetworkSecurityGroups | |
| ES-Deploy-Diagnostics-NIC | Deploy-Diagnostics-NIC | |
| ES-Deploy-Diagnostics-PostgreSQL | Deploy-Diagnostics-PostgreSQL | |
| ES-Deploy-Diagnostics-PowerBIEmbedded | Deploy-Diagnostics-PowerBIEmbedded | |
| ES-Deploy-Diagnostics-PublicIP | Deploy-Diagnostics-PublicIP | |
| ES-Deploy-Diagnostics-RecoveryVault | Deploy-Diagnostics-RecoveryVault | |
| ES-Deploy-Diagnostics-RedisCache | Deploy-Diagnostics-RedisCache | |
| ES-Deploy-Diagnostics-Relay | Deploy-Diagnostics-Relay | |
| ES-Deploy-Diagnostics-SearchServices | Deploy-Diagnostics-SearchServices | |
| ES-Deploy-Diagnostics-ServiceBus | Deploy-Diagnostics-ServiceBus | |
| ES-Deploy-Diagnostics-SignalR | Deploy-Diagnostics-SignalR | |
| ES-Deploy-Diagnostics-SQLDBs | Deploy-Diagnostics-SQLDBs | |
| ES-Deploy-Diagnostics-SQLElasticPools | Deploy-Diagnostics-SQLElasticPools | |
| ES-Deploy-Diagnostics-SQLMI | Deploy-Diagnostics-SQLMI | |
| ES-Deploy-Diagnostics-StreamAnalytics | Deploy-Diagnostics-StreamAnalytics | |
| ES-Deploy-Diagnostics-TimeSeriesInsights | Deploy-Diagnostics-TimeSeriesInsights | |
| ES-Deploy-Diagnostics-TrafficManager | Deploy-Diagnostics-TrafficManager | |
| ES-Deploy-Diagnostics-VirtualNetwork | Deploy-Diagnostics-VirtualNetwork | |
| ES-Deploy-Diagnostics-VM | Deploy-Diagnostics-VM | |
| ES-Deploy-Diagnostics-VMSS | Deploy-Diagnostics-VMSS | |
| ES-Deploy-Diagnostics-VNetGW | Deploy-Diagnostics-VNetGW | |
| ES-Deploy-Diagnostics-WebServerFarm | Deploy-Diagnostics-WebServerFarm | |
| ES-Deploy-Diagnostics-Website | Deploy-Diagnostics-Website | |
| | Deploy-Diagnostics-WVDAppGroup | (new) |
| | Deploy-Diagnostics-WVDHostPools | (new) |
| | Deploy-Diagnostics-WVDWorkspace | (new) |
| ES-Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | |
| ES-Deploy-DNSZoneGroup-For-File-PrivateEndpoint | Deploy-DNSZoneGroup-For-File-PrivateEndpoint | |
| ES-Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | |
| ES-Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | |
| ES-Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | |
| ES-Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | |
| ES-Deploy-FirewallPolicy | Deploy-FirewallPolicy | |
| ES-Deploy-HUB | Deploy-HUB | |
| ES-Deploy-LA-Config | Deploy-LA-Config | |
| ES-Deploy-LogAnalytics | Deploy-Log-Analytics | |
| ES-Deploy-Nsg-FlowLogs | Deploy-Nsg-FlowLogs-to-LA | |
| ES-Deploy-Sql-AuditingSettings | Deploy-Sql-AuditingSettings | |
| ES-Deploy-Sql-SecurityAlertPolicies | Deploy-Sql-SecurityAlertPolicies | |
| ES-Deploy-Sql-Tde | Deploy-Sql-Tde | |
| ES-Deploy-Sql-VulnerabilityAssessments | Deploy-Sql-vulnerabilityAssessments | |
| ES-Deploy-vHUB | Deploy-vHUB | |
| | Deploy-VNET-HubSpoke | (new) |
| ES-Deploy-vNet | Deploy-vNet | |
| ES-Deploy-vWAN | Deploy-vWAN | |
| ES-Deploy-Windows-DomainJoin | Deploy-Windows-DomainJoin | |

### `azurerm_policy_set_definition`

| Resource Name (v0.0.8) | Resource Name (v0.1.0) | Notes |
| :--- | :--- | :--- |
| ES-Deny-Public-Endpoints-for-PaaS-Services | Deny-PublicEndpoints | |
| ES-Deploy-Diagnostics-LogAnalytics | Deploy-Diag-LogAnalytics | |
| ES-Deploy-Sql-Security | Deploy-Sql-Security | |

### `azurerm_role_definition`

| Resource Name (v0.0.8) | Resource Name (v0.1.0) | Notes |
| :--- | :--- | :--- |
| ES-Network-Subnet-Contributor | Network-Subnet-Contributor | |

## Archetype definitions changes

To reflect the updated policies, and ensure policies are assigned according to the foundation implementation of Enterprise-scale, the following updates were made to the archetype definitions:

### es_root
_details coming soon_

### es_landing_zones
_details coming soon_

### es_management
_details coming soon_

## Will this happen again?

Unfortunately this question is hard to answer, but our intent is to keep future updates to policies in smaller increments so the impact will be smaller.

To help with this, we have automated the process used to keep the policies in sync, allowing us to quickly and easily manage future updates.

## Next steps

Take a look at the latest [User Guide](./User-Guide) documentation and our [Examples](./Examples) to understand the latest module configuration options, and review your implementation against the changes documented on this page.

 [//]: # (************************)
 [//]: # (INSERT LINK LABELS BELOW)
 [//]: # (************************)

[terraform-registry-caf-enterprise-scale]: https://registry.terraform.io/modules/Azure/caf-enterprise-scale/azurerm/latest "Terraform Registry: Terraform Module for Cloud Adoption Framework Enterprise-scale"
[Azure/Enterprise-Scale]: https://github.com/Azure/Enterprise-Scale 