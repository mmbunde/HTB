# Preparation Stage

Here you want to identify who is going to make up your incident response team, have a dedicated team, or have a third party be the team.<br>
The most important part of the preparation stage is to protect your infrastructure. This includes things like device hardening, patch management, multi-factor authentication, network segmentation, etc. You want to setup a defense in depth method so you don't have a single point of failure when it comes to your defenses. Think of a castles defenses, they have a moat as their first layer, then a high wall, and if that fails they have soldiers. Your organizations soldiers are the incident response team.<br>

## Preparation Prerequisites

The organization needs to make sure they have the following:
* **Risk Assessments**
    * You need to figure out what is important to the organization and prioritize the mission critical information. This needs to be done on a periodic basis.
* **Clear Policies and Documentation**
* **Skilled Incident Response Team**
* **Trained Workforce**
    
* **Tools for an incident response** (software and hardware)

## Clear Policies and Documentation

Below are some examples of policies and documentation that need to be reviewed and updated periodically or when changes have been made:<br>
* Contact information for the incident response team
* Contact information for legal, management, PR, law enforcement, ISP, and facility management
* Incident response SOPs
* Incident information policy
* Baselines for the systems and network
* Clean images of the systems and software
* Network diagrams
* Hashes of critical information

Not every incident is going to be a big deal and can be handled quickly and efficiently within the organization. For the more severe incidents that have legal ramifications the organization may have to reach out to law enforcement, regulatory bodies, customers, and vendors.<br>
It is crucial to have documentation while you are going through an incident. This can be stressful with trying to solve the issue as quickly as possible but as an incident responder you need to take note. Document events with timestamps, actions preformed, results of those actions. They are trying to answer the who, what, when, where, why and how.

## Tools (Software and Hardware)

The organization needs to make sure the incident response team has all the tools that they need to handle the incidents that come up. This are just some examples of the tools that maybe needed:
* A forensics workstation
* Memory capture and analysis tools
* Extra hard drives
* Write blockers
* Network analysis tools
* Packet sniffers
* Evidence gathering accessories
* Ticket tracking system

Another aspect in this stage that isn't really in the realm for the incident response team but they can assist is incident prevention. If the incident response team is made up of different people within the organization then it could fall on them. Below are a few important incident prevention measures that an organization can put in place

## DMARC

Domain based Message Authentication, Reporting and Conformance is a way to know if the an email is actually from the sender or not. The DMARC is a way to reject emails that try to spoof themselves as coming from a legit organization. This is stop threat actors from sending an email pretending to be an employee and sending out phishing emails or emails asking for an invoice to be paid.<br>
When implementing a DMARC you must test it to ensure that you are only blocking spoofed emails and not legitimate emails. You can even configure the DMARC to reject emails from domains that you don't own but this takes fine tuning and thorough testing

## Endpoint Hardening

Endpoints are where attacks are targeted at since they are the devices that connect to the internet and can give threat actors the entry point they need.<br>
There are baselines for hardening endpoint devices but the main two are the Center for Internet Security (CIS) and the Microsoft benchmarks. Below are the highly recommended actions to complete to harden your endpoints:
* Disable NetBIOS
* Remove administrative privileges from regular users
* Disable PowerShell in "ConstrainedLanguage" mode
* Enable Attack Surface Reduction (ASR) rules if using Microsoft Defender
* Implement whitelisting
* Utilize host based firewalls, block endpoint to endpoint communication
* Deploy an Endpoint Detection and Response (EDR) software

For hardening remember the words of Voltaire, *"Don't let perfect be the enemy of good."* Threats are always emerging and you can never have a 100% secure system but you can do your best and it will be good enough

## Privilege Identity Management/MFA/Passwords

Privileged escalation is the most common next path in AD environments. Admin users make the mistake of having a "complex" password but it is a weak password, like "P@55w0rd123!". It checks all the boxes:
- [x] lowercase
- [x] UPPERCASE
- [x] Number
- [x] Special Character
- [x] Minimum of 12 Characters

A good practice is to use a pass phrase because they can't easily be guessed and hard to brute force. Make sure it something that is easy to remember like "d0GS 0v3r C@ts!"

Multi-factor authentication (MFA) is another Identity Access Management (IAM) tool that should be in place for ALL access

## Vulnerability Scanning

New threats and vulnerabilities are always emerging and you need to keep up with them with repeated vulnerability scans. You can't just do the scans you also need to apply the patches to those vulnerabilities 

## User Awareness Training

Users need to know the policies and procedures for the appropriate use of the organizations resources
* Training on the current threats or the lessons learned from a previous incident. It is good to have training that is relevant to the department or roles that users belong to.
    * HR shouldn't be opening links or attachments from people sending their resume directly to them
    * Users with privileged access shouldn't be using their privileged account for their day to day, only when it is needed

## Active Directory Security Assessment

Being able to find misconfigurations or vulnerabilities in you systems you need to think like a threat actor. You can have this done by an internal team or from a third-party. This will help in identifying those misconfigurations or vulnerabilities and lets you be able to fix those making it harder for a threat actor to get in or move around your network<br>
AD has a few known escalation paths and new ones are being discovered. AD security assessments are critical to keeping your security posture and you can't assume that the system administrators are going to be aware of all of those vulnerabilities

## Purple Team Exercises

Purple team is where the blue and red teams train together. This is down inside the organization, the red team will attack the network and it is the blue teams job to try and detect the incident. If they aren't able to the blue team can work to improve themselves and any tools or rules for the defenses that are in place. If the blue team can detect the incident they can test their playbooks and incident handling procedures to make sure they work they way they are intended and can make tweaks if needed