# Containment, Eradication, and Recovery Stage

Once the investigation for the incident has been completed it is now time to move on to the containment stage.

## Containment

This stage is where the incident responder prevents the spread of the incident. They do this by have a short-term and long-term containment actions. They also don't want to alert the threat actor that they have been detected and have them pivot to persist in the network.<br>
For the short-term containment you are looking to take quick actions or isolating the compromised systems. The incident responders can do this by putting the systems on an isolated VLAN, pulling the network cable out of the system, or changing the name of the threat actors DNS to something that they control or that leads to nothing. The main goal of this is to contain the damage to the network/systems as much as possible. It also gives the incident response team the best possible opportunity to preserve as much information/evidence as they can and they are also able to take their forensic images.<br>
In long-term actions the goal is to make changes that will help in preventing the spread and future incidents. This is patching systems, changing or applying firewall rules, and adding host based IDS. Just because you have implemented these changes doesn't mean that the incident is over

## Eradication

With the compromised systems contained the incident response team can go through and eliminate the malware and make sure that the threat actor is completely out of the network. They maybe able to restore from a known good backup but the only way to be 100% positive that the threat actor is out of your system is to preform a clean install.

## Recovery

The systems need to be verified that they are ready to be put back on network and get operations back to normal. These systems need to be monitored more closely. Here are a few things to be on the look out for:
* Unusual logons, this could be user or service accounts
* Unusual processes
* Changes to the registry

If there was a big incident that resulted in a lot of systems being compromised the recovery process could take months and is usually approached in phases to prevent any future incidents.