# SIEM Definition & Fundamentals

## What is SIEM?

Security Information and Event Management (SIEM) combines the supervision of security data and security events. It provides real time alerts of security events and incidents.<br>
SIEM tools have a wide range of core functionality. It collects and handles the administration of log events, it can examine the logs, has incident handling capabilities, and can give visual representation of what is going on within the network.<br>
This gives the security analyst the ability to detect cyberattacks when they happen or go back in time to view how a threat actor first got into the network undetected and update the rules to alert them for future detection.

## The Evolution of SIEM Technology

SIEM came about from combining Security Information Management (SIM) and Security Event Management (SEM) into one package. It was back in 2005 when Gartner wrote the proposition to combine the two technologies<br>
SIM was the first and did simple log collection management, this allowed mass storage for examination and reporting. SEM then came along to consolidate, correlate, and send notifications from security software like antivirus, firewalls, IDS, servers, and databases.<br>
When companies started to realize that they could combine the two technologies it quickly got adopted.

## How Does A SIEM Solution Work?

SIEM systems take all the data from across the organization infrastructure, endpoints, network devices, servers, SCADA, and much more. It then standardizes the information and consolidates its so it is easier to analyze.<br>
SIEM systems need someone to go through the alerts and make sure that they a true incidents and if they are false positives then they can go ahead and fine tune the SIEM.<br>
The alerts from the SIEM usually give the important relevant information for the security analyst to start looking into it. Alerts can be sent through multiple channels, pop-ups, emails, text messages, or even sent to Slack, so they don't go unnoticed.<br>
When the SIEM system sends out a false positive alert it is important to go and tune the SIEM to help keep the alerts down. Since the SIEM system is probably getting any where from hundreds to thousands of events an hour it vital to keep the alerts to true incidents that need to be handled. This will keep the security analysts from getting over worked and this can lead to burn out and maybe even a high turnover rate within the organization.<br>

## SIEM Business Requirements & Use Cases

### Log Aggregation & Normalization

Log aggregation and normalization are essential for robust cybersecurity, enabled by SIEM systems. Without theses processes an organizations cybersecurity efforts are weakened.<br>
Log aggregation collects extensive security data from various sources, such as firewalls, IDS/IPS, and databases. <br>
Log normalization then standardizes the data making it easier to interpret for security threats. This standardized and centralized data enables the security analysts one place to analyze and connect all the information that was collected.<br>
The security analysts can leverage the SIEM systems log aggregation and normalization for:
* **Identify and Investigate Threats**: Centralized data helps in pinpointing and analyzing security incidents
* **Detect Patterns and Trends**: Correlated information reveals potential threats and emerging risk
* **Respond Quickly**: Improved visibility allows for faster, more effective response to security incidents

### Threat Alerting

A SIEM systems ability to identify and alert Security Operation Center (SOC) teams about potential threats is crucial for effective cybersecurity in the organization. This capability ensures that the security team can conduct prompt, targeted investigations and address the security incident efficiently.<br>
SIEM systems use sophisticated analytics and threat intelligence to detect potential threats and generate real-time alerts. When a threat is identified, the SIEM sends an immediate alert to the security team, providing essential details for a thorough investigation and risk mitigation. Delivering timely alerts, SIEM solutions help minimize the impact of security incidents and protect the critical assets.

### Contextualization & Response

Generating alerts alone is insufficient for effective security management. Without contextualization, a SIEM system that triggers alerts for every security event can overwhelm the SOC teams, leading to alert fatigue and frequent false positives<br>
Contextualization involves filtering and analyzing alerts to understand the nature of the threat, including the involved actors, affected network segments, and timing. This process helps the SOC teams distinguish between genuine threats and false alarms, allowing for accurate and efficient responses.<br>
Advanced SIEM systems use automated processes to manage and filter contextualized threats reducing the volume of alerts and minimizing unnecessary noise.<br>
An ideal SIEM solution enables the organization to take immediate action on threats, such as halting operation during an investigation. This proactive approach helps mitigate the impact of security incidents and safeguards critical assets.

### Compliance

SIEM systems are crucial for helping organizations meet regulatory compliance requirements by providing a robust framework for threat detection and management.<br>
Standards such as PCI DSS, HIPPA, and GDPR demand rigorous security measures, including real-time monitoring and analysis of network traffic. SIEM systems support these requirements by enabling SOC teams to detect and respond to security incidents effectively.<br>
SIEM solutions offer automated reporting and auditing capabilities, streamlining the process of generating compliance reports. These features help organizations quickly produce accurate documentation, proving adherence to the regulatory standards and simplifying interactions with auditors and regulators.<br>
Beyond meeting compliance requirements, SIEM systems enhance overall security posture by integrating threat intelligence and facilitating continuous monitoring. This proactive approach not only aids in regulatory compliance but also improves the organization's ability to prevent and respond to security threats, thereby safeguarding sensitive data and maintaining operational integrity.

## Data Flows Within A SIEM

Understanding the journey of data within a SIEM is essential for effective threat detection and response.
* **1. Data Ingestion**: SIEM solutions begin by ingesting logs from various sources, such as firewalls, IDS/IPS, servers, endpoints, and applications. Each SIEM tool has its own methods for collecting this data, a process known as data ingestion
* **2. Data Normalization and Aggregation**: The collected raw data is then processed and standardized. This step converts diverse log formats into a unified format that the SIEM correlation engine can understand. This makes it easier to analyze and correlate data from different sources
* **3. Analysis and Response**: The normalized data is used to create detection rules, dashboards, visualizations, alerts, and incidents. SOC teams leverage these tools to identify potential security threats and respond effectively

Beyond these core steps, modern SIEM systems incorporate advanced features like threat intelligence integration and machine learning. These enhancements improve the systems ability to detect sophisticated threats and automate responses. By continuously analyzing and correlating data, SIEM solutions provide deeper insights and faster identification of security risks, enhancing the overall effectiveness of the organization's security posture