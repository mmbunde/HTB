# SIEM Use Case Development

## What Is A SIEM Use Case?

A SIEM use case is a scenario designed to detect specific security incidents by analyzing log data and correlating events. These use cases are essential for building a strong cybersecurity strategy, as they help identify potential threats ranging from simple failed login attempts to complex situations like a ransomware outbreak.<br>
Consider a user named Rob who has ten consecutive failed authentication attempts. There could be two possibilities here, Rob could have forgotten his password or there could be a threat actor attempting a brute force attack. The SIEM system correlates these ten events into a single "brute force" alert and notifies the SOC team. The SOC team then investigates and takes appropriate action based on the data. If there were a few minutes between the login attempts, it could be Rob actually trying to login but if they were less than a second for all ten login attempts it is a brute force attack.

## SIEM Use Case Development Lifecycle

The SIEM Use Case Development Lifecycle consists of seven stages to ensure the effective detection and response to security incidents:
* **1. Requirements**: Understand the purpose of the use case, identifying the specific scenario that requires an alert. Requirements may come from customers, analysts, or employees. From the example above a use case is to detect a brute force attack, triggering an alert after ten consecutive login failures within four minutes
* **2. Data Points**: Identify all relevant data points in the network where user accounts can login. Gather logs from sources like Windows, Linux machines, servers, or applications ensuring they capture essential details such as user, timestamp, source, and destination
* **3. Log Validation**: Validate the logs to ensure they contain all necessary information, the data points, and confirm they are generated during the various authentication events, including local, web-based, application, VPN, OWA (Outlook Web Access)
* **4. Design and Implementation**: Design the use case by defining the conditions under which an alert should trigger, considering three primary parameters condition, aggregation, and priority. Using aggregation for the brute force example to limit false positives and sending priority alerts if the account is a privileged user
* **5. Documentation**: Develop a SOP that outlines the processes analysts should follow, including the conditions, priorities, and escalation path. The SOP also provides guidance on reporting and collaboration with other teams
* **6. Onboarding**: Begin with a development phase to identify and address any gaps before deploying the use case into the production environment. This stage helps reduce false positives and ensures the use case is ready for production
* **7. Periodic Update/Fine-Tuning**: Continuously refine and optimize the use case based on feedback from analysts. Regular updates ensure that correlation rules remain accurate and effective, improving the use case's overall performance

## How To Build SIEM Use Cases

Building an effective SIEM use cases involves a systematic approach to ensure comprehensive monitoring, timely detection, and effective incident response
* **Comprehend Needs and Risks**: Understand your organization's security needs and risks. Set up alerts to monitor the critical systems accordingly
* **Prioritize and Map Alerts**: Determine the priority and impact of each alert and map them to frameworks like the Cyber Kill Chain or MITRE ATT&CK to ensure relevance to threat scenarios
* **Assess TTD and TTR**: Establish Time to Detection (TTD) and Time to Respond (TTR) metrics for each alert to evaluate the SIEM effectiveness and the performance of security analysts
* **Create SOPs**: Develop SOPs for managing alerts, ensuring that analysts have clear guidelines on how to respond to different scenarios
* **Refine Alerts**: Continuously refine alerts based on monitoring results, reducing false positives and improving accuracy
* **Develop an Incident Response Plan (IRP)**: Prepare an IRP to address true positive incidents effectively, outlying steps for containment, eradication, and recovery
* **Set SLAs and OLAs**: Establish Service Level Agreements (SLAs) and Operational Level Agreements (OLAs) between teams to ensure timely handling of alerts and adherence to the IRP
* **Implement an Audit Process**: Maintain an audit process to mange alerts and incident reporting, ensuring accountability and continuous improvement
* **Document Logging and Alerts**: Create documentation to review the logging status of systems, the rational for alerts, and their triggering frequency, aiding in transparency and optimization
* **Establish a Knowledge Base**: Develop a knowledge base document that includes essential information and update to case management tools, helping analysts stay informed and effective in their roles

## Example 1 (MSBuild Engine Started By An Office Application)

The Elastic Stack is used to monitor suspicious activity, in this example MSBuild activity. MSBuild is a Microsoft Build Engine that is used for compiling applications, which can be exploited by threat actors. MSBuild uses XML files that are generated from Visual Studio and the threat actor can take advantage of MSBuild by adding malicious code into the engine.<br>
The goal is to detect when MSBuild is launched by a web browser or Microsoft Office application, which could indicate a potential security breach. Monitoring these instance is crucial because this behavior is unusual

**Detection Strategy**
* Establish a baseline of normal MSBuild usage to identify anomalies
* Set up a detection rule in the SIEM to flag instances where MSBuild is initiated by a web browser or Office application
* Given the potential risk, this behavior is classified as high severity or priority 1/2 due to its nature as a Living-off-the-land binaries (LoLBins)

**MITRE ATT&CK Framework Mappings**
* **Tactic**:
    * Execution (TA0002)
    * Defense Evasion (TA0005)
* **Techniques**:
    * Trusted Developer Utilities Proxy Execution (T1127)
        * MSBuild (T1127.001)

Creating a SOP and documenting alert handling the following need to be considered:
* `process.name`
* `process.parent.name`
* `event.action`
* Machine where the alert was detected
* User(s) associated with the machine
* User(s) activity within +/- two days of the alert's generation
* After this information has been gathered, the security analyst needs to talk with the user(s), examine the machine to analyze system logs, antivirus logs, and proxy logs from the SIEM

All information needs to be documented to be passed along to the Incident Handlers for reference

## Example 2 (MSBuild Making Network Connections)

This example focuses on detection when the MSBuild process makes outbound network connections, which may indicate potential malicious activity. The SOC team is monitoring MsBuild.exe for outbound connections to remote or potentially malicious IP addresses. These connections suggests adversarial activity, as attackers may use MSBuild to establish network communications while evading detection

* **Detection Strategy**
* The risk is that MSBuild could be used for outbound connections to malicious IP addresses, posing a potential threat
* Set up a SIEM rule to flag instances where MSBuild is responsible for network connections, particularly to suspicious or unknown IP addresses
* Assigning a medium severity due to the potential for false positives (e.g., legitimate connections to Microsoft IPs for updates)

**MITRE ATT&CK Framework Mapping**
* **Tactic**: Execution (TA0002)

For the SOP it should include handling alerts involving network connections made by MSBuild, based on the specific context of the alert, focusing on the IP address and connection behavior 