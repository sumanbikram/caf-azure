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
1. The following template types will need checking for references to policies and roles as listed in the [Changes](#Changes) section below:
   1. Archetype Definitions
   1. Policy Assignments
   1. Policy Set Definitions
1. The list of Policy Assignments deployed by the archetype definitions included with this module have been updated to reflect the Enterprise-scale reference architecture. Please review these before updating your environment to prevent unexpected issues.

## Resource changes

The following changes have been made within the module which may cause issues when using custom archetype definitions:

- All policy and role names have been updated to reflect the names used within the reference [Azure/Enterprise-Scale][Azure/Enterprise-Scale] repository. This means the `ES-` prefix has been removed, and some names have been changed (see lists below).
- All policies and roles are referenced by the `name` field. Previously we referenced the `properties.displayName` field. Please ensure any custom policy and role templates are updated to ensure the correct name is present in the `name` field. This change allows you to set a more user-friendly display name for these resources.
- The following archetype definitions have been updated (details in the [Archetype Definitions](#Archetype-Definitions) section below):
    - es_root
    - es_landing_zones
    - es_management

| Resource Type | Removals | Additions | Notes |
| :--- | :--- | :--- | :--- |
| azurerm_policy_assignment | ES-Allowed-Locations | Allow-Resource-Locations | |
| azurerm_policy_assignment | ES-Allowed-RSG-Locations | Allow-RSG-Locations | |
| azurerm_policy_assignment | ES-Deny-AppGW-No-WAF | Deny-AppGW-Without-WAF | |
| azurerm_policy_assignment | | Deny-http-Ingress-AKS" | (new) |
| azurerm_policy_assignment | ES-Deny-VMIPForwarding | Deny-IP-Forwarding | |
| azurerm_policy_assignment | | Deny-Priv-Containers-AKS | (new) |
| azurerm_policy_assignment | | Deny-Priv-Escalation-AKS | (new) |
| azurerm_policy_assignment | ES-Deny-RDPFromInternet | Deny-RDP-From-Internet | |
| azurerm_policy_assignment | ES-Deny-ResourceTypes | Deny-Resource-Types | |
| azurerm_policy_assignment | | Deny-Storage-http | (new) |
| azurerm_policy_assignment | ES-Deny-SubnetWithoutNsg | Deny-Subnet-Without-Nsg | |
| azurerm_policy_assignment | | Deploy-AKS-Policy | (new) |
| azurerm_policy_assignment | ES-Deploy-ASC-Standard | Deploy-ASC-Defender | |
| azurerm_policy_assignment | ES-Deploy-ASC-Monitoring | Deploy-ASC-Monitoring | |
| azurerm_policy_assignment | | Deploy-AzActivity-Log | (new) |
| azurerm_policy_assignment | | Deploy-Log-Analytics | (new) |
| azurerm_policy_assignment | | Deploy-LX-Arc-Monitoring | (new) |
| azurerm_policy_assignment | | Deploy-Resource-Diag | (new) |
| azurerm_policy_assignment | | Deploy-SQL-DB-Auditing | (new) |
| azurerm_policy_assignment | | Deploy-SQL-Security | (new) |
| azurerm_policy_assignment | | Deploy-VM-Backup | (new) |
| azurerm_policy_assignment | | Deploy-VM-Monitoring | (new) |
| azurerm_policy_assignment | | Deploy-VMSS-Monitoring | (new) |
| azurerm_policy_assignment | | Deploy-WS-Arc-Monitoring | (new) |
| azurerm_policy_definition | ES-Append-KV-SoftDelete | Append-KV-SoftDelete | |
| azurerm_policy_definition | ES-Deny-AA-child-resources | Deny-AA-child-resources | |
| azurerm_policy_definition | ES-Deny-AppGW-Without-WAF | Deny-AppGW-Without-WAF | |
| azurerm_policy_definition | ES-Deny-ERPeering | | (moved to built-in) |
| azurerm_policy_definition | ES-Deny-Private-DNS-Zones | Deny-Private-DNS-Zones | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-Aks | Deny-PublicEndpoint-Aks | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-CosmosDB | Deny-PublicEndpoint-CosmosDB | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-KeyVault | Deny-PublicEndpoint-KeyVault | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-MariaDB | Deny-PublicEndpoint-MariaDB | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-MySQL | Deny-PublicEndpoint-MySQL | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-PostgreSql | Deny-PublicEndpoint-PostgreSql | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-Sql | Deny-PublicEndpoint-Sql | |
| azurerm_policy_definition | ES-Deny-PublicEndpoint-Storage | Deny-PublicEndpoint-Storage | |
| azurerm_policy_definition | ES-Deny-PublicIP | Deny-PublicIP | |
| azurerm_policy_definition | | Deny-RDP-From-Internet | (new) |
| azurerm_policy_definition | ES-Deny-Subnets-Without-NSG | Deny-Subnet-Without-Nsg | |
| azurerm_policy_definition | ES-Deny-Subnets-Without-UDR | Deny-Subnet-Without-Udr | |
| azurerm_policy_definition | | Deny-VNET-Peer-Cross-Sub | (new) |
| azurerm_policy_definition | | Deny-VNet-Peering | (new) |
| azurerm_policy_definition | ES-Deploy-ASC-ContinuousExportToWorkspace | | (moved to built-in) |
| azurerm_policy_definition | ES-Deploy-ASC-Standard | Deploy-ASC-Standard | |
| azurerm_policy_definition | | Deploy-Budget | (new) |
| azurerm_policy_definition | ES-Deploy-AzureBackup-on-VMs | | (moved to built-in) |
| azurerm_policy_definition | ES-Deploy-DDoSProtection | Deploy-DDoSProtection | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-AA | Deploy-Diagnostics-AA | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ACI | Deploy-Diagnostics-ACI | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ACR | Deploy-Diagnostics-ACR | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ActivityLog | Deploy-Diagnostics-ActivityLog | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-AKS | Deploy-Diagnostics-AKS | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-AnalysisService | Deploy-Diagnostics-AnalysisService | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-APIMgmt | Deploy-Diagnostics-APIMgmt | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ApplicationGateway | Deploy-Diagnostics-ApplicationGateway | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-Batch | Deploy-Diagnostics-Batch | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-CDNEndpoints | Deploy-Diagnostics-CDNEndpoints | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-CognitiveServices | Deploy-Diagnostics-CognitiveServices | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-CosmosDB | Deploy-Diagnostics-CosmosDB | |
| azurerm_policy_definition | | Deploy-Diagnostics-Databricks | (new) |
| azurerm_policy_definition | ES-Deploy-Diagnostics-DataFactory | Deploy-Diagnostics-DataFactory | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-DataLakeStore | Deploy-Diagnostics-DataLakeStore | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-DLAnalytics | Deploy-Diagnostics-DLAnalytics | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-EventGridSub | Deploy-Diagnostics-EventGridSub | |
| azurerm_policy_definition | | Deploy-Diagnostics-EventGridSystemTopic | (new) |
| azurerm_policy_definition | ES-Deploy-Diagnostics-EventGridTopic | Deploy-Diagnostics-EventGridTopic | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-EventHub | Deploy-Diagnostics-EventHub | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ExpressRoute | Deploy-Diagnostics-ExpressRoute | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-Firewall | Deploy-Diagnostics-Firewall | |
| azurerm_policy_definition | | Deploy-Diagnostics-FrontDoor | (new) |
| azurerm_policy_definition | | Deploy-Diagnostics-Function | (new) |
| azurerm_policy_definition | ES-Deploy-Diagnostics-HDInsight | Deploy-Diagnostics-HDInsight | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-iotHub | Deploy-Diagnostics-iotHub | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-KeyVault | Deploy-Diagnostics-KeyVault | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-LoadBalancer | Deploy-Diagnostics-LoadBalancer | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-LogicAppsISE | Deploy-Diagnostics-LogicAppsISE | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-LogicAppsWF | Deploy-Diagnostics-LogicAppsWF | |
| azurerm_policy_definition | | Deploy-Diagnostics-MariaDB | (new) |
| azurerm_policy_definition | ES-Deploy-Diagnostics-MlWorkspace | Deploy-Diagnostics-MlWorkspace | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-MySQL | Deploy-Diagnostics-MySQL | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-NetworkSecurityGroups | Deploy-Diagnostics-NetworkSecurityGroups | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-NIC | Deploy-Diagnostics-NIC | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-PostgreSQL | Deploy-Diagnostics-PostgreSQL | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-PowerBIEmbedded | Deploy-Diagnostics-PowerBIEmbedded | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-PublicIP | Deploy-Diagnostics-PublicIP | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-RecoveryVault | Deploy-Diagnostics-RecoveryVault | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-RedisCache | Deploy-Diagnostics-RedisCache | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-Relay | Deploy-Diagnostics-Relay | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-SearchServices | Deploy-Diagnostics-SearchServices | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-ServiceBus | Deploy-Diagnostics-ServiceBus | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-SignalR | Deploy-Diagnostics-SignalR | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-SQLDBs | Deploy-Diagnostics-SQLDBs | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-SQLElasticPools | Deploy-Diagnostics-SQLElasticPools | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-SQLMI | Deploy-Diagnostics-SQLMI | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-StreamAnalytics | Deploy-Diagnostics-StreamAnalytics | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-TimeSeriesInsights | Deploy-Diagnostics-TimeSeriesInsights | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-TrafficManager | Deploy-Diagnostics-TrafficManager | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-VirtualNetwork | Deploy-Diagnostics-VirtualNetwork | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-VM | Deploy-Diagnostics-VM | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-VMSS | Deploy-Diagnostics-VMSS | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-VNetGW | Deploy-Diagnostics-VNetGW | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-WebServerFarm | Deploy-Diagnostics-WebServerFarm | |
| azurerm_policy_definition | ES-Deploy-Diagnostics-Website | Deploy-Diagnostics-Website | |
| azurerm_policy_definition | | Deploy-Diagnostics-WVDAppGroup | (new) |
| azurerm_policy_definition | | Deploy-Diagnostics-WVDHostPools | (new) |
| azurerm_policy_definition | | Deploy-Diagnostics-WVDWorkspace | (new) |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-File-PrivateEndpoint | Deploy-DNSZoneGroup-For-File-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | |
| azurerm_policy_definition | ES-Deploy-FirewallPolicy | Deploy-FirewallPolicy | |
| azurerm_policy_definition | ES-Deploy-HUB | Deploy-HUB | |
| azurerm_policy_definition | ES-Deploy-LA-Config | Deploy-LA-Config | |
| azurerm_policy_definition | ES-Deploy-LogAnalytics | Deploy-Log-Analytics | |
| azurerm_policy_definition | ES-Deploy-Nsg-FlowLogs | Deploy-Nsg-FlowLogs-to-LA | |
| azurerm_policy_definition | ES-Deploy-Sql-AuditingSettings | Deploy-Sql-AuditingSettings | |
| azurerm_policy_definition | ES-Deploy-Sql-SecurityAlertPolicies | Deploy-Sql-SecurityAlertPolicies | |
| azurerm_policy_definition | ES-Deploy-Sql-Tde | Deploy-Sql-Tde | |
| azurerm_policy_definition | ES-Deploy-Sql-VulnerabilityAssessments | Deploy-Sql-vulnerabilityAssessments | |
| azurerm_policy_definition | ES-Deploy-vHUB | Deploy-vHUB | |
| azurerm_policy_definition | | Deploy-VNET-HubSpoke | (new) |
| azurerm_policy_definition | ES-Deploy-vNet | Deploy-vNet | |
| azurerm_policy_definition | ES-Deploy-vWAN | Deploy-vWAN | |
| azurerm_policy_definition | ES-Deploy-Windows-DomainJoin | Deploy-Windows-DomainJoin | |
| azurerm_policy_set_definition | ES-Deny-Public-Endpoints-for-PaaS-Services | Deny-PublicEndpoints | |
| azurerm_policy_set_definition | ES-Deploy-Diagnostics-LogAnalytics | Deploy-Diag-LogAnalytics | |
| azurerm_policy_set_definition | ES-Deploy-Sql-Security | Deploy-Sql-Security | |
| azurerm_role_definition | ES-Network-Subnet-Contributor | Network-Subnet-Contributor | |

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