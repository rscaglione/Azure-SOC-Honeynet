# Building a SOC + Honeynet in Azure (Live Traffic)
<!-- ![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg) -->
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/7dae6161-c8e1-4330-81f0-506c3f4cffab)


## Introduction

In this project, I set up a small security system in Microsoft's Azure cloud platform. I gathered information about potential cyber threats from different sources and organized it in a central place called a Log Analytics workspace. Then, I used a tool called Microsoft Sentinel to create maps that show how cyber attacks happen, set up alerts to warn us about potential issues, and documented any incidents that occurred.

To make sure our system was working well, I first checked how secure it was in a test environment for a day. After identifying areas where it could be better, I added extra safeguards to make it tougher for cyber threats. Then, I checked again for another day to see if the improvements worked. The information and results I'll share include various measurements related to security.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<!-- ![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg) -->
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/7f1c8699-fdec-42f4-8191-84a04b6237f9)






## Architecture After Hardening / Security Controls
<!-- ![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg) -->
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/c3fa5ef4-c69e-4ce9-bb71-f58f9e124430)


The structure of the small honeynet in Azure comprises the following elements:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" measurements, everything was set up and accessible from the internet. The Virtual Machines and other resources had minimal protection, and there was no need for private access.

In the "AFTER" measurements, I improved security. I restricted access to the Virtual Machines by only allowing traffic from my admin workstation. Additionally, I enhanced protection for other resources by using their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
