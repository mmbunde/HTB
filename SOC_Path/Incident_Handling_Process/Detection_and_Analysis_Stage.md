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

|**Date**|**Time of the event**|**Hostname**|**Event Description**|**Data Source**|<br>
|----|----|----|----|----|<br>
|08-10-2024|14:13UTC|SQLServer01|Hacker tool 'Mimikatz' was detected|Antivirus Software|<br>

## Incident Severity and Extent Questions

When handling an incident you need to be thinking about the impact that the incident is going to have on the organization, some questions you should ask yourself:
* What is the exploitation impact?
* What are the exploitation requirements?
* Can or are any business-critical systems be effected?
* How many systems are compromised?
* Is the exploit being used in the wild?
* Does the exploit have worm like capabilities?

The last couple of questions give you an idea of how sophisticated the threat actor is.

## Incident Confidentiality and Communication

Incidents need to kept to a need to know basis, unless there are laws, regulations, or a management decision to disclose that information. When an investigation has started expectations need to be set, like how much time is needed to complete the investigation. It is also important to keep everyone involved in the investigation and management informed and keep that line of communication open

## The Investigation

The investigation starts with the limited information that was gathered when it was first deteted. With this information the incident response team begins the cyclic 3 step process:
* Creation and usage of indicators of compromise (IOC)
* Identification of new leads and impacted machines
* Data collection and analysis from the new leads
Once you get get done with the third step you go back to the beginning

### Initial Investigation Data

The incident response team should follow where the leads are taking them and not jump to conclusions. They should take the the intial information gathered to guide them and then keep updating the leads throughout the investigation

### Creation and Usage of IOCs

IOCs are documented in a structured manner and they are so important that there are languages, like OpenIOC, that have been developed to document them in a standardized way. Yara is also another language developed for IOCs. You can use Mandiant's IOC Editor to create or edit IOCs. In order to take advantage of those langauges by deploying an IOC-obtaining/IOC-searching tool.

### Identification of New Leads and Impacted Systems

After searching for IOCs you will get some hits to see what systems are showing the same signs of the compromise. You could get some false positives and you need to be able to eliminate those. You could also get a lot of hits and in that case you need to prioritize the systems that are critial for the organization

### Data Collection and Analysis From the New Leads and Impacted Systems

Now that the incident response team has identified the compromised systems they need to start collecting and preserving the state of the systems. They will mostly keep the system up and running to preserve as much information as possible but there maybe some cases where they will need to shutdown or restart the system. The reason you don't want to just shut down the system is because there could some artifacts only live in the RAM which is cleared when the system turns off.<br>
Now that the information is collected it needs to be analyzed. It is the most time intensive. Disk forensics and malware analysis are the most common type of analysis that takes place. Any new leads that come from the analysis are then fed back into the loop and the process continues with that new information.<br>
If the incident is going to need legal action the chain of custody needs to be kept track of so the information gathered can be used in the court