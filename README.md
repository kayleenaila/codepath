# Project 8 - Pentesting Live Targets

Time spent: **7** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:

* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.

## Blue

Vulnerability #1: SQL Injection

Description: The blue website does not sanitize inputs for the salesperson.php page, so attacker can easily add script to the URL in SQL to alter database or take all its info. The red and green websites make sure that a user cannot do this and changes some of the inputs and sends us back to a normally-functioning page. 

![blue-vuln1](https://user-images.githubusercontent.com/29714687/159184633-aa67c56d-f27d-4c03-aaed-80515f893649.gif)

Vulnerability #2: Session Hijacking/Fixation

Description: The blue website does not confirm that the user accessing the site is the same as the user who logged into the site. It only checks for a session ID and applies that current state associated with that session to the web model. The green and red sites make check for more factors like the cookies and session generation to ensure the person trying to access has valid credentials within their own point of entry.

![blue-vuln2](https://user-images.githubusercontent.com/29714687/159184645-394f6058-2480-4c3f-9292-6fd0234922d1.gif)

## Green

Vulnerability #1: Username Enumeration

Description: The green website has a flaw in how it notifies user that their login was not correct. For the blue and red sites, the error message is consistent but it seems on the green site that the login has two different styling classes applied for different situations that are visibily different to attackers. When the username is correct, we used a "failure" class type which has bold font while the incorrect usernames have the "failed" class type without bold font. Attackers can verify if a username is correct by this and then just need to secure a password.

![green-vuln1](https://user-images.githubusercontent.com/29714687/159184650-8287f8e7-e2b9-4455-8e5d-32cd70f717c9.gif)
<img src="green-vuln1.gif">

Vulnerability #2: Cross-Site Scripting (XSS)

Description: Malicious code is not sanitized in any way in the contact portion of the green website. When malicious code is put into the other sites, it is cleansed so tha tthe page cannot read this as code, but this is not done on the green so when an admin views the feedback from the comments, the scripts execute. 

![green-vuln2](https://user-images.githubusercontent.com/29714687/159184653-b002c65c-b073-47ad-b1f6-85b19c925a0f.gif)
<img src="green-vuln2.gif">


## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)

Description: An attacker on the red website is able to get direct access to a salesperson who should not be viewed because those ID's were not specified as being private and inaccessible. The other sites hide these IDs and make them inaccessible via the id variable, but this red page does not. Thus, ID's 10 and 11 who are no longer salespeople are accessed by an attacker, gaining access to privileged information that was not specified as such. 

![red-vuln1](https://user-images.githubusercontent.com/29714687/159184661-9b5bf967-380a-4b1d-ad0a-0728d90da65c.gif)

Vulnerability #2: Cross-Site Request Forgery (CSRF)

Description: An attacker is able to incite edits to the database in a few ways. If the attacker already somehow has access to the admin page, they do not need a CSRF token to be correct in order to execute an edit to user or salesperson information. That said, if the attacker leaves malicious code in the guise of a webpage to execute as a contact feedback, then an admin may access that page with their permissions and then the code executes, editing the information of the user. In other words, the other pages check that the CSRF token is valid before editing a user, but the red page does not do this.

![red-vuln2](https://user-images.githubusercontent.com/29714687/159184671-067f59cf-8de6-45cb-94df-df7c602546ac.gif)


## Notes

It was difficult to remember how each of these challeneges were executed and what their assoicated names were because I know how to perform an exploit, but often forget its name. It was also difficult to cross-reference all these sites to see what was different because there are so many places that one can look to realize where the vulnerability is.
