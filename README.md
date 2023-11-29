# Creating a Security Operations Center (SOC) and Honeynet with Live Traffic in Azure
<!-- ![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg) -->
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/7dae6161-c8e1-4330-81f0-506c3f4cffab)


## Introduction

In this project, I set up a small security system in Microsoft's Azure cloud platform. I gathered information about potential cyber threats from different sources and organized it in the Log Analytics workspace. Then, I used Microsoft Sentinel to create maps that show how cyber attacks happen, set up alerts to warn about potential issues, and documented any incidents that occurred.

To make sure the system was working well, I first checked how secure it was in a test environment for a day. After identifying areas where it could be better, I added extra safeguards to make it more resilient against cyber threats. Then, I checked again for another day to see if the improvements worked. The information and results I'll share include various measurements related to security.

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


The components forming the foundation of the compact honeynet in Azure include:

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
<!-- ![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br> -->
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/ad19db41-0d97-4662-8c0f-578f0066ac6e)
_______________________________________________________________________________________________________________
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/76d1222a-98fd-4f46-a894-82fea879f5fa)
_______________________________________________________________________________________________________________
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/a03eb400-7834-4314-89c0-680f3c474eef)
_______________________________________________________________________________________________________________
![image](https://github.com/rscaglione/Azure-SOC-Honeynet/assets/54590449/d1d4782b-810c-4456-8952-7cf8871c83be)
_______________________________________________________________________________________________________________





## Metrics Before Hardening / Security Controls

Here are the metrics that were measured in the insecure environment for 24 hours:
<br>Start Time 2023-11-17 T19:29:49</br>
Stop Time 2023-11-18 T19:29:49

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 161562
| Syslog                   | 15338
| SecurityAlert            | 9
| SecurityIncident         | 461
| AzureNetworkAnalytics_CL | 4620

## Attack Maps After Hardening / Security Controls

```None of the map queries showed any results because there were no instances of harmful activities during the 24-hour period after implementing security measures.```

## Metrics After Hardening / Security Controls

The following table shows the metrics measured in the environment for another 24 hours, but after the security controls were applied:
<br>Start Time 2023-11-23 T17:15:02</br>
Stop Time	2023-11-24 T17:15:02

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7945
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I set up a small security system in Microsoft Azure, bringing together various logs into a Log Analytics workspace. I used Microsoft Sentinel to detect issues and create incident reports based on these logs. I also measured security metrics in the less secure setup before making it more secure and then checked again afterward. Importantly, the number of security problems significantly decreased after implementing these security measures, showing that they are effective.

