# Honeypot Assignment

**Time spent:** **6** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** How did you deploy it? Did you use GCP, AWS, Azure, Vagrant, VirtualBox, etc.?
MHN-Admin was deployed using GCP, creating VM instances through a new project on that cloud service. I deployed it using the commands provided in the assignment documentation. The code snippet used can be found below. The honeypot-1 VM instance was created in a very similar matter with a different name and a firewall rule added.

```
gcloud compute instances create "mhn-admin" \
    --machine-type "n1-standard-1" \
    --subnet "default" \
    --maintenance-policy "MIGRATE" \
    --tags "mhn-admin" \
    --image-family "ubuntu-minimal-1804-lts" \
    --image-project "ubuntu-os-cloud" \
    --boot-disk-size "10" \
    --boot-disk-type "pd-standard" \
    --boot-disk-device-name "mhn-admin"
```

![mhn-admin](https://user-images.githubusercontent.com/29714687/161392421-594b5777-89bc-4695-9fc3-969d62a61b92.gif)

### Dionaea Honeypot Deployment (Required)

**Summary:** Briefly in your own words, what does dionaea do?
Dionaea creates a honeypot through scripting that acts as a decoy website which attackers will attempt to access. The whole point of this is to gather information about what the attack was, when it happened and how it was attempted. 

![honeypot](https://user-images.githubusercontent.com/29714687/161392438-b036ad3b-d756-4056-971c-f83c3c6ddee5.gif)

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?
MHN-Admin uses MongoDB which is a NoSQL database so data can be stored in a non-relational format. The ```mongoexport``` command we use makes it so that we can get the information in this MongoDB instance in a JSON format. The exported JSON file records the ID of the attack, the protocol used, the hpfeed_id, a timestamp holding date and time of day, a source IP address and port, a destination port, an identifier and which honeypot the attack was executed on.

*Be sure to upload session.json directly to this GitHub repo/branch in order to get full credit.*

## Notes

A challenge I encountered when I first attempted this is that I tried to do everything by hand using the GCP UI, but that proved to overcomplicate the work that had to be done. I initially executed the firewalls incorrectly and ended up with a honeypot which was not functional because the port access was incorrect. Upon redoing the assignment, I was able to get the desired results where attackers are trying to exploit my honeypot.

## nmap Attack proof
<img width="295" alt="nmap" src="https://user-images.githubusercontent.com/29714687/161392445-63cd8bbb-8203-4e35-938b-695703d192c9.png">
