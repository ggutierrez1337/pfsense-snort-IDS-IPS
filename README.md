# pfSense - Installing and Configuring Snort IDS/IPS on a pfSense Firewall

# Description
This project showcases the **integration and configuration** of a well-known IPS/IDS tool known as **Snort** with pfSense Firewall. By integrating Snort into a pfSense Firewall, the attack-surface of the network is further minimized as it comes with a robust ruleset such as **Snort VRT, Snort GPLv2, ET Open and Pro,** and **OpenAppID Detectors** detecting well known malicious signatures and is continuously updated with the latest threats and signatures. 

## Tools and Utilities
- **VirtualBox**: Used for virtualization of pfSense and Ubuntu.
- **pfSense**: Open-source firewall and router software.
- **Ubuntu Desktop 24**: Interacting with pfSense GUI.

# Documentation
## Installing Snort on pfSense

1. Go to **System → Package Manager,** and install Snort

![image 32](https://github.com/user-attachments/assets/eda178d1-8c01-47c9-8f48-5170335ed8e0)

2. Snort will be installed if the Success prompt appears

![Screenshot_(1054)](https://github.com/user-attachments/assets/b495919c-42f7-43c5-8ee9-0ea0654e5ef0)

## Snort Rule Sets

1. To access Snort, go to **Services → Snort**
2. Some common rule sets that are provided by Snort are
    - **Snort VRT** - Vulnerability Research Team proactively discovering, accessing, and responding to intrusion attempts, malware, and vulnerabilities
    - **Snort GPLv2** - Official community rule set and no subscriptions but only has a subset of the subscriber ruleset
    - **ET Open and ET Pro** - Emerging Threats
    - **OpenAppID Detectors** - Application focused detection language and process module

## Configuring Snort

Enabling rulesets and scheduling automatic updates for those rulesets

1. Ensure that a Snort account has been registered and the Oinkcode is in the user account information
2. Go to **Services → Snort** and enable **Snort VRT** then provide the Oinkcode given to the Snort user account created

![image 33](https://github.com/user-attachments/assets/46a63787-ade7-4eec-9595-5292ac984c9a)

3. Enable the following rulesets
    - Snort VRT
    - Snort GPLv2
    - ET Open
    - OpenAppID Detectors
4. Be sure to enable text rules for OpenAppID and to update Snort daily at a desired time. Ensure to hide all **deprecated rules** as well. Once finished, select save

![image 34](https://github.com/user-attachments/assets/b01828a5-349a-4be6-b797-2e7d29150f52)

![image 35](https://github.com/user-attachments/assets/2cfa9f64-28be-4abf-b355-fc9dd77362a6)

5. When Snort has been configured the first time go to **Services → Snort → Updates** and select **Update Rules.** The **Results** section will say **Success** and MD5 Hashes/Date will be updated to latest version

![Screenshot_(1059)](https://github.com/user-attachments/assets/716b442c-d7e8-4113-b07a-76b74e34165d)

## Assigning Snort to Interfaces on the Firewall

1. Go to **Services → Snort → Snort Interfaces,** and select **Add.** WAN will be added first and then LAN. Check **Send Alerts to System Log** and check the **Block Offenders** that generate Snort alerts. Block the source IP of the offender and leave the rest of the settings as default

![image 36](https://github.com/user-attachments/assets/e1059e6e-d3fe-4009-8f09-26afd57928f3)

![image 37](https://github.com/user-attachments/assets/686448e1-a291-4e39-afe5-938d6ddb1b4d)

2. Repeat the same process for **LAN,** then start Snort on the interfaces by selecting the **play button** under **Snort Status**

![image 38](https://github.com/user-attachments/assets/a5ac1692-5b82-4991-add4-852414328ce6)

## Snort Deployment Strategy

Enabling IPS for Snort can be done by checking the **block offenders** check box in the WAN/LAN settings as done previously

Prevent mode can be good starting off, but there are cases where there are false positives which could lead to remediation efforts or requiring troubleshooting and making changes to Snort and pfSense

- To avoid this, uncheck **block offenders** in the WAN/LAN to leave Snort in **Detect Mode** which will only alert for detections and not take action against the traffic. Can then tune Snort and turn on **block offenders**

# Conclusion
By integrating **Snort with pfSense**, it makes for a robust combination allowing the use of created detection rules by the Snort Community as well as Talos. Enabling **Firewall Rules** catered to the network, ensures only specific communications are being held that are allowed while **Snort** ensures that malicious activity is to be detected and prevented, if so.
