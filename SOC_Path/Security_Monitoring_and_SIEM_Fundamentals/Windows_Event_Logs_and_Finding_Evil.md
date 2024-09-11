# Windows Events Logs & Finding Evil

## Windows Events Logs

Windows Event Logs are an essential part of the Windows OS, capturing logs from various systems components, including the OS itself, applications, services, and Event Tracing for Windows (ETW) providers. These logs are vital for cybersecurity professionals, offering detailed insights into application errors, security events, and diagnostic data, which are crucial for analysis and intrusion detection<br>
The logs are organized into different categories such as "Application", "System", "Security" and more, allowing for easy identification of events based on their origin or purpose. These logs can be accessed through the Event Viewer application of programmatically via the Windows Event log API

* **Default Windows Logs**
* **Application**: Logs related to software applications
* **Security**: Captures security related events like logins
* **Setup**: Logs related to system setup activities
* **System**: General system information and errors
* **Forwarded Events**: Logs forwarded from other machines, useful for centralized monitoring

Administrators can explore these logs using Event Viewer and can also open previously saved .evtx files for further analysis

## The Anatomy of an Event Log

When analyzing application logs in Windows Event Logs, two primary event levels are encountered: Information and Error
* Information Events: Provide general details about application activities, such as start or stop actions
* Error events: Highlight specific issues within the application, offering detailed insights for troubleshooting

Each event in the Windows Event Log contains several key components:
* **1. Log Name**: Identifies the log category (e.g., Application, System)
* **2. Source**: The Software that generated the event
* **3. Event ID**: A unique identifier for the event, useful for further research
* **4. Task Category**: Describes the event's purpose of function
* **5. Level**: Indicates the severity of the event (Information, Warning, Warning, Error, Critical, Verbose)
* **6. Keywords**: Flags that categorize events, enhancing search precision (e.g. "Audit Success")
* **7. User**: The user account active when the event occurred
* **8. OpCode**: Specifies the operation reported by the event 
* **9. Logged**: The date and time when the event was logged
* **10. Computer**: The name of the computer where the event took place
* **11. XML Data**: The event data, also available in XML format for detailed analysis

The Keywords field is particularly valuable for filtering and refining search queries, allowing for more efficient log management<br>
For example, when examining an error event, the Event ID and Source (e.g., "SideBySide") provide specific information about the error, which can be further explored using Microsoft's documentation. Detailed descriptions and XML views offer rich context and additional data, such as the process ID, aiding in precise analysis<br>
Switching to Security logs, consider Event ID 4624, which records the creation of a logon session. This event log contains critical details such as the Logon ID, which can be correlated with other events, and the Logon Type, indication the nature of the logon (e.g., a service initiated by "SYSTEM"). Further investigation may be needed to identify the specific service involved, using correlation techniques with additional data points like the Logon ID

## Leveraging Custom XML Queries

To enhance our log analysis, we can utilize custom XML queries to efficiently identify and correlate related events, starting with the "Logon ID". This process begins by navigating to the Windows Event Viewer and selecting "Filter Current Log" -> "XML" -> "Edit Query Manually" which provides access to a specialized XML query language. This language allows for more detailed and specific log searches.<br>
In a practical scenario, consider a query that filters events based on the "SubjectLogonId" field with the value "0x3E7". This Logon ID is chosen to trace all events associated with a particular logon session, thereby facilitating a deeper understanding of the activities linked to that ID.<br>
### Customization and Support
* **Automatic Filters**: If crafting the query manually seems challenging, automatic filters can be used to experiment with their impact on the XML output. This can simplify the process and guide query construction
* **Microsoft Resources**: For detailed guidance on advanced XML filtering, Microsoft provides comprehensive articles on using SML in the Windows Event Viewer.

By leveraging custom XML queries, we can concentrate on specific events related to a particular Logon ID, filtering out irrelevant data and revealing a clearer view of logon activities

### Analyzing Log Details
1. **Event ID 4907**: This event indicates a change in audit policy, Specifically, it signifies a modification to the System Access Control List (SACL) of an object, such as a registry key or file. SACLs log access attempts, which can be valuable for understanding security changes
    * **SACL Overview**: The SACL contains Access Control Entries (ACEs) that define the conditions under which access attempts are recorded. ACEs can log both successful and failed access attempts
    * **Reference**: For detailed information on SACLs, refer to Microsoft's documentation on access control lists ([SACL Documentation](https://learn.microsoft.com/en-us/windows/win32/secauthz/access-control-lists))
2. **Event Analysis**
    * **SetupHost.exe**: The event details reveal that "SetupHost.exe" was responsible for the policy change. This process, often associated with software setup, might be legitimate or could be potentially disguised malware. the specific object affected is "bootmanager" and examining the security descriptors ("NewSd" and "OldSd") helps identify the changes made
    * **Security Descriptor Fields**: Understanding these fields is crucial for interpreting the nature of the modifications. Resources such as "ACE Strings" and Understanding SDDL Syntax" offer detailed explanations
3. **Logon and Special Logon Events**
    * Following the audit policy change, the logs show a logon event and a subsequent "special logon" event. This "special logon" provides insights into the token permissions granted to the user, which includes critical privileges
    * Documentation on privilege constants, such as "SeDebugPrivlege" outlines the specific permissions granted, like the ability to manipulate memory of other processes

    ## Useful Windows Event Logs

    Windows Event Logs are critical for monitoring and maintaining the security and performance of Windows systems. Understanding which events are valuable can significantly enhance threat detection and system management. Here's an overview of useful Windows event logs across different categories, along with practical examples and tips for effective monitoring

    ### Windows System Logs
    1. **Event ID 1074** (System Shutdown/Restart)
        * **Purpose**: Records when and why the system was shutdown or restarted
        * **Use**: Identify unexpected shutdowns or restarts which could indicate malware infections or unauthorized access attempts
    2. **Event ID 6005** (The Event Log Service was Started)
        * **Purpose**: Marks the start of the Event Log Service
        * **Use**: Indicates system boot up, useful for investigating performance issues or potential security incidents
    3. **Event ID 6006** (The Event Log Service was Stopped)
        * **Purpose**: Signifies the stopping of the Event Log Service, typically during system shutdown
        * **Use**: Anomalies may point to attempts to disrupt logging for covering illicit activities
    4. **Event ID**: (Windows Uptime)
        * **Purpose**: Displays the system uptime in seconds
        * **Use**: Shorter uptime than expected may indicate unauthorized reboots, possibly due to intrusions
    5. **Event ID 7040** (Service Status Change)
        * **Purpose**: Indicates changes in the startup type of services
        * **Use**: Changes to crucial services could indicate tampering or potential threats
    
    ### Windows Security Logs
    1. **Event ID 1102** (The Audit Log was Cleared)
        * **Purpose**: Records when the audit log was cleared
        * **Use**: Clearing logs may indicate attempts to hide evidence of malicious activity
    2. **Event ID 1116** (Antivirus Malware Detection)
        * **Purpose**: Logs detection of malware by Windows Defender
        * **Use**: A surge in these events may point to targeted attacks or widespread infections
    3. **Event ID 1118** (Antivirus Remediation Activity Started)
        * **Purpose**: Indicates that Defender has stared removing or quarantining malware
        * **Use**: Monitor to ensure successful remediation efforts
    4. **Event ID 1119** (Antivirus Remediation Activity Succeeded)
        * **Purpose**: Signifies successful removal or quarantine of detected malware
        * **Use**: Confirm that threats are effectively neutralized
    5. **Event ID 1120** (Antivirus Remediation Activity Failed)
        * **Purpose**: Logs failure of malware remediation
        * **Use**: Immediate attention required to address failed remediation attempts
    6. **Event ID 4624** (Successful Logon)
        * **Purpose**: Records successful logon attempts
        * **Use**: Identify normal vs suspicious logon behavior, especially at unusual times or locations
    7. **Event ID 4625** (Failed Logon)
        * **Purpose**: Logs failed logon attempts
        * **Use**: Multiple failures could indicate brute force attacks
    8. **Event ID 4648** (A Logon was Attempted Using Explicit Credentials)
        * **Purpose**: Triggered when explicit credentials are used to run a program
        * **Use**: Detects lateral movement or suspicious activities
    9. **Event ID 4656** (A Handle to an Object was Requested)
        * **Purpose**: Indicates requests for handles to objects like files or registry keys
        * **Use**: Useful for detecting access to sensitive resources
    10. **Event ID 4672** (Special Privileges Assigned to a New Logon)
        * **Purpose**: Records when accounts log on with super user privileges
        * **Use**: Monitor for potential misuse of elevated privileges
    11. **Event ID 4698** (A Scheduled Task was Created)
        * **Purpose**: Logs the creation of a scheduled task
        * **Use**: Detect persistence mechanisms used by attackers
    12. **Event ID 4700 & 4701** (Scheduled Task Enabled/Disabled)
        * **Purpose**: Records enabling or disabling of scheduled tasks
        * **Use**: Indicates potential tampering with tasks for malicious purposes
    13. **Event ID 4702** (A Scheduled Task was Updated)
        * **Purpose**: Indicates updates to scheduled tasks
        * **Use**: Monitor for changes that may signify malicious intent
    14. **Event ID 4719** (System Audit Policy was Changed)
        * **Purpose**: Indicates updates to scheduled tasks
        * **Use**: Potential attempt to disable or modify auditing to cover tracks
    15. **Event ID 4738** (A User Account was Changed)
        * **Purpose**: Logs changes to user accounts
        * **Use**: Detects unauthorized account modifications, indicating possible account takeover
    16. **Event ID 4771** (Kerberos Pre-Authentication Failed)
        * **Purpose**: Logs failed Kerberos pre-authentication attempts
        * **Use**: High volumes may indicate brute force attempts against Kerberos
    17. **Event ID 4776** (Domain Controller Credential Validation)
        * **Purpose**: Records attempts to validate credentials by the domain controller
        * **Use**: Monitor for repeated failures indicating potential brute force attacks
    18. **Event ID 5001** (Antivirus Real-Time Protection Configuration Changed)
        * **Purpose**: Indicates changes to real-time protection settings
        * **Use**: Unauthorized changes may suggest attempts to disable antivirus protections
    19. **Event ID 5140** (Network Share Accessed)
        * **Purpose**: Logs access to network shares
        * **Use**: Detect unauthorized access to network resources
    20. **Event ID 5142** (Network Share Added)
        * **Purpose**: Records the creation of new networks shares
        * **Use**: Unauthorized shares could be used for data exfiltration or malware spread
    21. **Event ID 5145** (Network Share Access Check)
        * **Purpose**: Indicates checks for client access to network shares
        * **Use**: Frequent checks may suggest mapping of network shares for malicious purposes
    22. **Event ID 5157** (Windows Filtering Platform Blocked Connection)
        * **Purpose**: Logs when the Windows Filtering Platform blocks a connection attempt
        * **Use**: Identify and investigate blocked connection attempts
    23. **Event ID 7045** (Service Installed)
        * **Purpose**: Records the installation of new services
        * **Use**: Appearance of unknown services may indicate malware installation

Effective monitoring involves understanding normal behavior in your environment, correlating logs from different sources, and using a centralized log management system for real-time alerting and analysis. Regular review and adjustment of monitoring parameters help in minimizing false positives and enhancing threat detection
