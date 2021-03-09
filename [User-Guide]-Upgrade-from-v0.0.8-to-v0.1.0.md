> The following page has been published in preparation for the next release, 0.1.0, which will introduce a number of changes which will result in the redeployment of many resources managed by this module.
>
> THIS PAGE IS STILL A WORK IN PROGRESS!

## Overview

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

| Resource Type | Changes | | Notes |
| --- | --- | --- | --- |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Allowed-Locations | <span style="color:green">+</span> Allow-Resource-Locations | |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Allowed-RSG-Locations | <span style="color:green">+</span> Allow-RSG-Locations | |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deny-AppGW-No-WAF | <span style="color:green">+</span> Deny-AppGW-Without-WAF | |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deny-http-Ingress-AKS" | (new) |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deny-VMIPForwarding | <span style="color:green">+</span> Deny-IP-Forwarding | |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deny-Priv-Containers-AKS | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deny-Priv-Escalation-AKS | (new) |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deny-RDPFromInternet | <span style="color:green">+</span> Deny-RDP-From-Internet | |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deny-ResourceTypes | <span style="color:green">+</span> Deny-Resource-Types | |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deny-Storage-http | (new) |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deny-SubnetWithoutNsg | <span style="color:green">+</span> Deny-Subnet-Without-Nsg | |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-AKS-Policy | (new) |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deploy-ASC-Standard | <span style="color:green">+</span> Deploy-ASC-Defender | |
| azurerm_policy_assignment | <span style="color:red">-</span> ES-Deploy-ASC-Monitoring | <span style="color:green">+</span> Deploy-ASC-Monitoring | |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-AzActivity-Log | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-Log-Analytics | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-LX-Arc-Monitoring | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-Resource-Diag | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-SQL-DB-Auditing | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-SQL-Security | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-VM-Backup | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-VM-Monitoring | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-VMSS-Monitoring | (new) |
| azurerm_policy_assignment | | <span style="color:green">+</span> Deploy-WS-Arc-Monitoring | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Append-KV-SoftDelete | <span style="color:green">+</span> Append-KV-SoftDelete | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-AA-child-resources | <span style="color:green">+</span> Deny-AA-child-resources | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-AppGW-Without-WAF | <span style="color:green">+</span> Deny-AppGW-Without-WAF | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-ERPeering | | (moved to built-in) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-Private-DNS-Zones | <span style="color:green">+</span> Deny-Private-DNS-Zones | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-Aks | <span style="color:green">+</span> Deny-PublicEndpoint-Aks | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-CosmosDB | <span style="color:green">+</span> Deny-PublicEndpoint-CosmosDB | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-KeyVault | <span style="color:green">+</span> Deny-PublicEndpoint-KeyVault | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-MariaDB | <span style="color:green">+</span> Deny-PublicEndpoint-MariaDB | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-MySQL | <span style="color:green">+</span> Deny-PublicEndpoint-MySQL | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-PostgreSql | <span style="color:green">+</span> Deny-PublicEndpoint-PostgreSql | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-Sql | <span style="color:green">+</span> Deny-PublicEndpoint-Sql | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicEndpoint-Storage | <span style="color:green">+</span> Deny-PublicEndpoint-Storage | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-PublicIP | <span style="color:green">+</span> Deny-PublicIP | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deny-RDP-From-Internet | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-Subnets-Without-NSG | <span style="color:green">+</span> Deny-Subnet-Without-Nsg | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deny-Subnets-Without-UDR | <span style="color:green">+</span> Deny-Subnet-Without-Udr | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deny-VNET-Peer-Cross-Sub | (new) |
| azurerm_policy_definition | | <span style="color:green">+</span> Deny-VNet-Peering | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-ASC-ContinuousExportToWorkspace | | (moved to built-in) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-ASC-Standard | <span style="color:green">+</span> Deploy-ASC-Standard | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Budget | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-AzureBackup-on-VMs | | (moved to built-in) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DDoSProtection | <span style="color:green">+</span> Deploy-DDoSProtection | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-AA | <span style="color:green">+</span> Deploy-Diagnostics-AA | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ACI | <span style="color:green">+</span> Deploy-Diagnostics-ACI | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ACR | <span style="color:green">+</span> Deploy-Diagnostics-ACR | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ActivityLog | <span style="color:green">+</span> Deploy-Diagnostics-ActivityLog | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-AKS | <span style="color:green">+</span> Deploy-Diagnostics-AKS | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-AnalysisService | <span style="color:green">+</span> Deploy-Diagnostics-AnalysisService | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-APIMgmt | <span style="color:green">+</span> Deploy-Diagnostics-APIMgmt | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ApplicationGateway | <span style="color:green">+</span> Deploy-Diagnostics-ApplicationGateway | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-Batch | <span style="color:green">+</span> Deploy-Diagnostics-Batch | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-CDNEndpoints | <span style="color:green">+</span> Deploy-Diagnostics-CDNEndpoints | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-CognitiveServices | <span style="color:green">+</span> Deploy-Diagnostics-CognitiveServices | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-CosmosDB | <span style="color:green">+</span> Deploy-Diagnostics-CosmosDB | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-Databricks | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-DataFactory | <span style="color:green">+</span> Deploy-Diagnostics-DataFactory | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-DataLakeStore | <span style="color:green">+</span> Deploy-Diagnostics-DataLakeStore | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-DLAnalytics | <span style="color:green">+</span> Deploy-Diagnostics-DLAnalytics | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-EventGridSub | <span style="color:green">+</span> Deploy-Diagnostics-EventGridSub | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-EventGridSystemTopic | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-EventGridTopic | <span style="color:green">+</span> Deploy-Diagnostics-EventGridTopic | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-EventHub | <span style="color:green">+</span> Deploy-Diagnostics-EventHub | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ExpressRoute | <span style="color:green">+</span> Deploy-Diagnostics-ExpressRoute | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-Firewall | <span style="color:green">+</span> Deploy-Diagnostics-Firewall | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-FrontDoor | (new) |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-Function | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-HDInsight | <span style="color:green">+</span> Deploy-Diagnostics-HDInsight | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-iotHub | <span style="color:green">+</span> Deploy-Diagnostics-iotHub | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-KeyVault | <span style="color:green">+</span> Deploy-Diagnostics-KeyVault | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-LoadBalancer | <span style="color:green">+</span> Deploy-Diagnostics-LoadBalancer | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-LogicAppsISE | <span style="color:green">+</span> Deploy-Diagnostics-LogicAppsISE | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-LogicAppsWF | <span style="color:green">+</span> Deploy-Diagnostics-LogicAppsWF | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-MariaDB | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-MlWorkspace | <span style="color:green">+</span> Deploy-Diagnostics-MlWorkspace | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-MySQL | <span style="color:green">+</span> Deploy-Diagnostics-MySQL | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-NetworkSecurityGroups | <span style="color:green">+</span> Deploy-Diagnostics-NetworkSecurityGroups | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-NIC | <span style="color:green">+</span> Deploy-Diagnostics-NIC | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-PostgreSQL | <span style="color:green">+</span> Deploy-Diagnostics-PostgreSQL | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-PowerBIEmbedded | <span style="color:green">+</span> Deploy-Diagnostics-PowerBIEmbedded | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-PublicIP | <span style="color:green">+</span> Deploy-Diagnostics-PublicIP | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-RecoveryVault | <span style="color:green">+</span> Deploy-Diagnostics-RecoveryVault | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-RedisCache | <span style="color:green">+</span> Deploy-Diagnostics-RedisCache | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-Relay | <span style="color:green">+</span> Deploy-Diagnostics-Relay | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-SearchServices | <span style="color:green">+</span> Deploy-Diagnostics-SearchServices | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-ServiceBus | <span style="color:green">+</span> Deploy-Diagnostics-ServiceBus | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-SignalR | <span style="color:green">+</span> Deploy-Diagnostics-SignalR | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-SQLDBs | <span style="color:green">+</span> Deploy-Diagnostics-SQLDBs | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-SQLElasticPools | <span style="color:green">+</span> Deploy-Diagnostics-SQLElasticPools | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-SQLMI | <span style="color:green">+</span> Deploy-Diagnostics-SQLMI | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-StreamAnalytics | <span style="color:green">+</span> Deploy-Diagnostics-StreamAnalytics | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-TimeSeriesInsights | <span style="color:green">+</span> Deploy-Diagnostics-TimeSeriesInsights | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-TrafficManager | <span style="color:green">+</span> Deploy-Diagnostics-TrafficManager | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-VirtualNetwork | <span style="color:green">+</span> Deploy-Diagnostics-VirtualNetwork | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-VM | <span style="color:green">+</span> Deploy-Diagnostics-VM | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-VMSS | <span style="color:green">+</span> Deploy-Diagnostics-VMSS | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-VNetGW | <span style="color:green">+</span> Deploy-Diagnostics-VNetGW | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-WebServerFarm | <span style="color:green">+</span> Deploy-Diagnostics-WebServerFarm | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-Website | <span style="color:green">+</span> Deploy-Diagnostics-Website | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-WVDAppGroup | (new) |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-WVDHostPools | (new) |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-Diagnostics-WVDWorkspace | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-Blob-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-File-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-File-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-KeyVault-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-Queue-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-Sql-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | <span style="color:green">+</span> Deploy-DNSZoneGroup-For-Table-PrivateEndpoint | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-FirewallPolicy | <span style="color:green">+</span> Deploy-FirewallPolicy | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-HUB | <span style="color:green">+</span> Deploy-HUB | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-LA-Config | <span style="color:green">+</span> Deploy-LA-Config | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-LogAnalytics | <span style="color:green">+</span> Deploy-Log-Analytics | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Nsg-FlowLogs | <span style="color:green">+</span> Deploy-Nsg-FlowLogs-to-LA | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Sql-AuditingSettings | <span style="color:green">+</span> Deploy-Sql-AuditingSettings | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Sql-SecurityAlertPolicies | <span style="color:green">+</span> Deploy-Sql-SecurityAlertPolicies | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Sql-Tde | <span style="color:green">+</span> Deploy-Sql-Tde | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Sql-VulnerabilityAssessments | <span style="color:green">+</span> Deploy-Sql-vulnerabilityAssessments | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-vHUB | <span style="color:green">+</span> Deploy-vHUB | |
| azurerm_policy_definition | | <span style="color:green">+</span> Deploy-VNET-HubSpoke | (new) |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-vNet | <span style="color:green">+</span> Deploy-vNet | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-vWAN | <span style="color:green">+</span> Deploy-vWAN | |
| azurerm_policy_definition | <span style="color:red">-</span> ES-Deploy-Windows-DomainJoin | <span style="color:green">+</span> Deploy-Windows-DomainJoin | |
| azurerm_policy_set_definition | <span style="color:red">-</span> ES-Deny-Public-Endpoints-for-PaaS-Services | <span style="color:green">+</span> Deny-PublicEndpoints | |
| azurerm_policy_set_definition | <span style="color:red">-</span> ES-Deploy-Diagnostics-LogAnalytics | <span style="color:green">+</span> Deploy-Diag-LogAnalytics | |
| azurerm_policy_set_definition | <span style="color:red">-</span> ES-Deploy-Sql-Security | <span style="color:green">+</span> Deploy-Sql-Security | |
| azurerm_role_definition | <span style="color:red">-</span> ES-Network-Subnet-Contributor | <span style="color:green">+</span> Network-Subnet-Contributor | |

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