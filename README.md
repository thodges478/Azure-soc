# Azure-soc
Building a SOC + Honeynet in azure 
Building a SOC + Honeynet in Azure (Live Traffic)

image

Introduction

In this project, I've developed a compact honeynet within the Microsoft Azure framework. This honeynet serves as a controlled environment to simulate potential cyber threats. It integrates with various sources to gather logs, channeling them into a dedicated Log Analytics workspace. Microsoft Sentinel, our chosen tool, leverages these logs to construct visual attack maps, activate alerts in response to potential threats, and establish a structured approach to handling security incidents.

To evaluate the effectiveness of our security measures, I've conducted a comparative analysis. Initially, I measured key security metrics over a 24-hour period within an intentionally vulnerable environment. Subsequently, after implementing a series of security controls to bolster the system's resilience, I conducted another 24-hour metric assessment. The metrics we will show are:

SecurityEvent (Windows Event Logs)
Syslog (Linux Event Logs)
SecurityAlert (Log Analytics Alerts Triggered)
SecurityIncident (Incidents created by Sentinel)
AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
Architecture Before Hardening / Security Controls

image

Architecture After Hardening / Security Controls

image

The architecture of the mini honeynet in Azure consists of the following components:

Virtual Network (VNet)
Network Security Group (NSG)
Virtual Machines (2 windows, 1 linux)
Log Analytics Workspace
Azure Key Vault
Azure Storage Account
Microsoft Sentinel
"BEFORE" metrics: All resources were deployed in a configuration that left them openly accessible via the internet. The Virtual Machines were configured with both their Network Security Groups and internal firewalls set to permissive settings. Additionally, all other deployed resources featured public endpoints that were visible to the internet, rendering the incorporation of Private Endpoints unnecessary.

"AFTER" metrics: Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

Attack Maps Before Hardening / Security Controls

NSG Allowed Inbound Malicious Flows image
Linux Syslog Auth Failures image
Windows RDP/SMB Auth Failures image

MSSQL-Auth-Fail image

Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours: Start Time 2023-08-29 14:40:42 Stop Time 2023-08-30 14:40:42

Metric	Count
SecurityEvent	574147
Syslog	1463
SecurityAlert	6
SecurityIncident	207
AzureNetworkAnalytics_CL	2599
Attack Maps After Hardening / Security Controls

All map queries returned no results due to zero instances of malicious activity for the 24 hour period after hardening.

Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls: Start Time 2023-08-30 19:29 Stop Time 2023-08-31 19:33

Metric	Count
SecurityEvent	10884
Syslog	1
SecurityAlert	0
SecurityIncident	0
AzureNetworkAnalytics_CL	0
Conclusion

In the context of this project, we established a compact honeynet infrastructure within the Microsoft Azure environment. This honeynet served as a controlled simulation space to detect and analyze potential cybersecurity threats. We aggregated logs from various sources, channeling them into a designated Log Analytics workspace. Employing Microsoft Sentinel, we harnessed these logs to proactively identify anomalous activities, triggering alerts and facilitating the orchestration of incident responses. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness
