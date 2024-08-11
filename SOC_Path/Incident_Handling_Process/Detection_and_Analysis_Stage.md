# Detection & Analysis

In order to detect an incident you need to use all your resources, sensors, logs, and trained personnel. Threats can be come at your organization from a whole bunch of different threat vectors but there are many ways that you can find an indicator of compromise like:
* Employees that notice abnormal behavior
* An alert from the tools that you implemented
    * SIEM/SOAR
    * IDS/IPS
    * Firewall
* Threat hunting activities

It is recommended to different levels of detection of your network by setting it up logically:
* Detection at the perimeter or internet facing
* Detection on the internal network
* Detection on an endpoint
* Detection on the application level

## Initial Investigation
Security professionals need to do an initial investigation when an incident is detected before you call everyone in to help when it is something that the person who discovered or was alerted to the incident could handle it. When responding to an incident you should collect as much information as possible, below are some of the things that should be documented:
* Date/Time for when the incident was reported and who detected/reported it
* How the incident was detected
* What was the incident
* List of impacted systems
* Who accessed the impacted system and what actions were taken
* Physical location, OS, IP address, hostname, system owner, systems's purpose, and current state of the system
* If malware is detected the list of IPs, time and date of detection, type of malware, systems impacted, export of the malicious files with their hashes

Now that you have all this information you are better equipped to handle the incident at hand, you will be able to take the appropriate actions given the incident.<br>
You can start building a timeline of the incident, this will keep everything organized and give you a better idea of the big picture. Listing everything in the time that they happened you can see how other events are related or you can find that it is unrealted and need to look somewhere else. Below is an example of what should be documented:
|**Date**|**Time of the event**|**Hostname**|**Event Description**|**Data Source**|
|----|----|----|----|----|----|
|08-10-2024|14:13UTC|SQLServer01|Hacker tool 'Mimikatz' was detected|Antivirus Software|