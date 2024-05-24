# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/d5e409d4-9bb5-4933-bfaa-db6bdb9a8ea6)



## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/8b86c908-c4db-422e-85b5-0d7ad6d6fd5f)


## Architecture After Hardening / Security Controls
![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/8d2f8cee-6752-4967-8dfa-c7b82a257bd2)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
**NSG Allowed Inbound Malicious Flows** ![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/173ae1b0-7d6d-4882-89c6-63d725472555)

**Linux Syslog Auth Failures** ![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/5a4cc8d7-801c-4263-976a-f87717df4b0f)

**Windows RDP/SMB Auth Failures** ![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/522461a5-431d-4425-bc35-77b309613db1)

**MS SQL Server Auth Failures** ![image](https://github.com/erikhutson1/Cloud-SOC/assets/15833874/4f07474f-f3fb-4bfd-99fc-2c140c5546a1)



## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2024-05-21 16:35:46

Stop Time 2024-05-22 16:35:46

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 225542
| Syslog                   | 5202
| SecurityAlert            | 37
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 2311

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Start Time 

Stop Time	

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | TBD
| Syslog                   | TBD
| SecurityAlert            | TBD
| SecurityIncident         | TBD
| AzureNetworkAnalytics_CL | TBD

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
