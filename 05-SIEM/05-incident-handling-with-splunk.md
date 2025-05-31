# Introduction: Incident Handling

This room covers an incident Handling scenario using Splunk. An incident from a security perspective is "Any event or action, that has a negative consequence on the security of a user/computer or an organization is considered a security incident." Below are a few of the events that would negatively affect the environment when they occurred:

-    Crashing the system
-    Execution of an unwanted program
-    Access to sensitive information from an unauthorized user
-    A Website being defaced by the attacker
-    The use of USB devices when there is a restriction in usage is against the company's policy

## Learning ObjectiveAnalyst standing with magnifying glass

-    Learn how to leverage OSINT sites during an investigation
-    How to map Attacker's activities to Cyber Kill Chain Phases
-    How to utilize effective Splunk searches to investigate logs
-    Understand the importance of host-centric and network-centric log sources 

## Room Prerequisites

Before going through this room, it is expected that the participants will have a basic understanding of Splunk. If not, consider going through this room, Splunk 101 (https://tryhackme.com/jr/splunk101).

It is good to understand the following before completing this lesson:

-    Splunk overview and basic navigation
-    Important Splunk Queries
-    Know how to use different functions/values to craft a search query
-    How to look for interesting fields


# Incident Handling - Life Cycle 

Incident Handling Life Cycle

![alt text](0b438ea4fe36b9ca02cce5a6e91e4f14.png)

As an Incident Handler / SOC Analyst, we would aim to know the attackers' tactics, techniques, and procedures. Then we can stop/defend/prevent against the attack in a better way. The Incident Handling process is divided into four different phases. Let's briefly go through each phase before jumping into the incident, which we will be going through in this exercise.

## 1. Preparation

The preparation phase covers the readiness of an organization against an attack. That means documenting the requirements, defining the policies, incorporating the security controls to monitor like EDR / SIEM / IDS / IPS, etc. It also includes hiring/training the staff.


## 2. Detection and Analysis

The detection phase covers everything related to detecting an incident and the analysis process of the incident. This phase covers getting alerts from the security controls like SIEM/EDR investigating the alert to find the root cause. This phase also covers hunting for the unknown threat within the organization.


## 3. Containment, Eradication, and Recovery

This phase covers the actions needed to prevent the incident from spreading and securing the network. It involves steps taken to avoid an attack from spreading into the network, isolating the infected host, clearing the network from the infection traces, and gaining control back from the attack.

## 4. Post-Incident Activity / Lessons Learnt

This phase includes identifying the loopholes in the organization's security posture, which led to an intrusion, and improving so that the attack does not happen next time. The steps involve identifying weaknesses that led to the attack, adding detection rules so that similar breach does not happen again, and most importantly, training the staff if required.



# Incident Handling: Scenario

In this exercise, we will investigate a cyber attack in which the attacker defaced an organization's website. This organization has Splunk as a SIEM solution setup. Our task as a Security Analysis would be to investigate this cyber attack and map the attacker's activities into all 7 of the Cyber Kill Chain Phases. It is important to note that we don't need to follow the sequence of the cyber kill chain during the Investigation. One finding in one phase will lead to another finding that may have mapped into some other phase.

## Cyber Kill Chain 

We will follow the Cyber kill Chain Model and map the attacker's activity in each phase during this Investigation. When required, we will also utilize Open Source Intelligence (OSINT) and other findings to fill the gaps in the kill chain. It is not necessary to follow this sequence of the phases while investigating.

-    Reconnaissance
-    Weaponization
-    Delivery
-    Exploitation
-    Installation
-    Command & Control
-    Actions on Objectives

##   Scenario   

A Big corporate organization Wayne Enterprises  has recently faced a cyber-attack where the attackers broke into their network, found their way to their web server, and have successfully defaced their website http://www.imreallynotbatman.com . Their website is now showing the trademark of the attackers with the message YOUR SITE HAS BEEN DEFACED  as shown below.  

![alt text](dcc528c218e8dda78504f55f58188575.png)

They have requested " US " to join them as a Security Analyst and help them investigate this cyber attack and find the root cause and all the attackers' activities within their network.

The good thing is, that they have Splunk already in place, so we have got all the event logs related to the attacker's activities captured. We need to explore the records and find how the attack got into their network and what actions they performed.

This Investigation comes under the <b>Detection and Analysis phase</b>

##  Splunk

During our investigation, we will be using Splunk as our SIEM solution. Logs are being ingested from webserver/firewall/Suricata/Sysmon etc. In the data summary tab, we can explore the log sources showing visibility into both network-centric and host-centric activities.To get the complete picture of the hosts and log sources being monitored in Wayne Enterprise, please click on the Data summary and navigate the available tabs to get the information.

![alt text](dc5ec747ef4b0f3eada2aac0bb1fa0ed.gif)

###  Interesting log Sources

Some of the interesting log sources that will help us in our Investigation are:

<table class="table table-bordered">
<tbody>
<tr>
<td><strong>Log Sources <br></strong></td>
<td><strong>Details <br></strong></td>
</tr>
<tr>
<td><strong>wineventlog </strong></td>
<td>It contains Windows Event logs</td>
</tr>
<tr>
<td><strong>winRegistry </strong></td>
<td>It contains the logs related to registry creation / modification / deletion etc.</td>
</tr>
<tr>
<td><strong>XmlWinEventLog </strong></td>
<td>It contains the <span data-testid="glossary-term" class="glossary-term">sysmon</span> event logs. It is a very important log source from an investigation point of view.</td>
</tr>
<tr>
<td><strong>fortigate_utm <br></strong></td>
<td>It contains Fortinet <span data-testid="glossary-term" class="glossary-term">Firewall</span> logs</td>
</tr>
<tr>
<td><strong>iis <br></strong></td>
<td>It contains IIS web server logs</td>
</tr>
<tr>
<td><strong>Nessus:scan <br></strong></td>
<td>It contains the results from the Nessus vulnerability scanner.</td>
</tr>
<tr>
<td><strong>Suricata <br></strong></td>
<td>It contains the details of the alerts from the Suricata <span data-testid="glossary-term" class="glossary-term">IDS</span>. This log source shows which alert was triggered and what caused the alert to get triggered— a very important log source for the Investigation.</td>
</tr>
<tr>
<td><strong>stream:<span data-testid="glossary-term" class="glossary-term">http</span> <br></strong></td>
<td>It contains the network flow related to <span data-testid="glossary-term" class="glossary-term">http</span> traffic.</td>
</tr>
<tr>
<td><strong>stream: <span data-testid="glossary-term" class="glossary-term">DNS</span> <br></strong></td>
<td>It contains the network flow related to <span data-testid="glossary-term" class="glossary-term">DNS</span> traffic.</td>
</tr>
<tr>
<td><strong>stream:icmp <br></strong></td>
<td>It contains the network flow related to icmp traffic.</td>
</tr>
</tbody>
</table>


<b>Note</b>:  All the event logs that we are going to investigate are present in index=botsv1  

Now that we know what hosts we have to investigate, what sources and the source types are, let's connect to the lab and start Investigating .


### Room Machine

Before moving forward, deploy the machine. When you deploy the machine, it will be assigned an IP Machine IP : MACHINE_IP . The machine will take up to 3-5 minutes to start.

### Disclaimer

As this is a public [dataset](https://github.com/splunk/botsv1) released by Splunk, which depicts a realistic scenario, it is advised that this dataset may contain profanity, slang, vulgar expressions, and/or generally offensive terminology. Please use with discretion.



# Reconnaissance Phase

Reconnaissance is an attempt to discover and collect information about a target. It could be knowledge about the system in use, the web application, employees or location, etc.

We will start our analysis by examining any reconnaissance attempt against the webserver imreallynotbatman.com. From an analyst perspective, where do we first need to look? If we look at the available log sources, we will find some log sources covering the network traffic, which means all the inbound communication towards our web server will be logged into the log source that contains the web traffic. Let's start by searching for the domain in the search head and see which log source includes the traces of our domain.

Search Query: `index=botsv1 imreallynotbatman.com`

Search Query explanation: We are going to look for the event logs in the index "botsv1" which contains the term imreallynotbatman.com

![alt text](c320e7a1192dd94671fb5048e6a3cf3d.gif)

Here we have searched for the term imreallynotbatman.com in the index botsv1. In the sourcetype field, we saw that the following log sources contain the traces of this search term.

-    Suricata
-    stream:http
-    fortigate_utm
-    iis

From the name of these log sources, it is clear what each log source may contain. Every analyst may have a different approach to investigating a scenario. Our first task is to identify the IP address attempting to perform reconnaissance activity on our web server. It would be obvious to look at the web traffic coming into the network. We can start looking into any of the logs mentioned above sources.

Let us begin looking at the log source `stream:http`, which contains the http traffic logs, and examine the `src_ip` field from the left panel. Src_ip field contains the source IP address it finds in the logs.
Search Query: `index=botsv1 imreallynotbatman.com sourcetype=stream:http`

Search Query Explanation: This query will only look for the term  `imreallynotbatman.com` in the `stream:http` log source.

![alt text](11b2317ec891d4b9b9a4c5bdaa594aa6.png)

<b>Note</b>: The important thing to note, if you don't find the field of interest, keep scrolling in the left panel. When you click on a field, it will contain all the values it finds in the logs.

So far, we have found two IPs in the `src_ip` field 40.80.148.42 and 23.22.63.114. The first IP seems to contain a high percentage of the logs as compared to the other IP, which could be the answer. If you want to confirm further, click on each IP one by one, it will be added into the search query, and look at the logs, and you will find the answer.

To further confirm our suspicion about the IP address 40.80.148.42, click on the IP and examine the logs. We can look at the interesting fields like `User-Agent`, `Post request`, `URIs`, etc., to see what kind of traffic is coming from this particular IP.

![alt text](6e4de3d85d3322f76b20c71ea020d0b4.gif)

We have narrowed down the results to only show the logs from the source IP 40.80.148.42, looked at the fields of interest and found the traces of the domain being probed.

## Validate the IP that is scanning

So what do we need to do to validate the scanning attempt? Simple, dig further into the weblogs. Let us narrow down the result, look into the suricata logs, and see if any rule is triggered on this communication.

Search Query: `index=botsv1 imreallynotbatman.com src=40.80.148.42 sourcetype=suricata`

Search Query Explanation: This query will show the logs from the suricata log source that are detected/generated from the source IP 40.80.248.42

![alt text](ff5428b053d955ddc89da6ff9dc0f81e.gif)

We have narrowed our search on the src IP and looked at the source type suricata to see what Suricata triggered alerts. In the right panel, we could not find the field of our interest, so we clicked on more fields and searched for the fields that contained the signature alerts information, which is an important point to note. 

## Q & A

Q1 One suricata alert highlighted the CVE value associated with the attack attempt. What is the CVE value?

A1 CVE-2014-6271

![alt text](image-23.png)

Q2 What is the CMS our web server is using?

A2 joomla

![alt text](image-24.png)

![alt text](image-25.png)

Q3 What is the web scanner, the attacker used to perform the scanning attempts?

A3 acunetix

![alt text](image-26.png)

![alt text](image-27.png)

Q4 What is the IP address of the server imreallynotbatman.com?

A4 192.168.250.70

![alt text](image-28.png)




# Exploitation Phase

The attacker needs to exploit the vulnerability to gain access to the system/server.

In this task, we will look at the potential exploitation attempt from the attacker against our web server and see if the attacker got successful in exploiting or not.

To begin our investigation, let's note the information we have so far:

-    We found two IP addresses from the reconnaissance phase with sending requests to our server.
-    One of the IPs `40.80.148.42` was seen attempting to scan the server with IP `192.168.250.70`.
-    The attacker was using the web scanner Acunetix for the scanning attempt.

## Count

Let's use the following search query to see the number of counts by each source IP against the webserver.

Search Query:`index=botsv1 imreallynotbatman.com sourcetype=stream* | stats count(src_ip) as Requests by src_ip | sort - Requests`

Query Explanation: This query uses the stats function to display the count of the IP addresses in the field `src_ip`.

![alt text](7ba883b04d37c2eca99362c9bda29454.png)

Additionally, we can also create different visualization to show the result. Click on Visualization → Select Visualization as shown below.

![alt text](caed557285bfc17702c039120aac1b4f.png)

Now we will narrow down the result to show requests sent to our web server, which has the IP 192.168.250.70

Search Query: `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70"`

Query Explanation: This query will look for all the inbound traffic towards IP 192.168.250.70.

![alt text](d570547792358eed228ca92e06c27af9.png)

The result in the src_ip field shows three IP addresses (1 local IP and two remote IPs) that originated the HTTP traffic towards our webserver.

Another interesting field, http_method will give us information about the HTTP Methods observed during these HTTP communications.

We observed most of the requests coming to our server through the POST request, as shown below.

![alt text](45495b910d4f5ad7ca9215a15166835f.png)

To see what kind of traffic is coming through the POST requests, we will narrow down on the field `http_method=POST` as shown below:

Search Query: `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST`

![alt text](e9e7ec45af9290353dffb5809e33ac53.png)

The result in the src_ip field shows two IP addresses sending all the POST requests to our server.

Interesting fields: In the left panel, we can find some interesting fields containing valuable information. Some of the fields are:

-    src_ip
-    form_data
-    http_user_agent
-    uri

![alt text](17ef54b0e1fdf69923e5c30f5650aad1.gif)


The term Joomla is associated with the webserver found in a couple of fields like uri, uri_path, http_referrer, etc. This means our webserver is using Joomla CMS (Content Management Service) in the backend.

A little search on the internet for the admin login page of the Joomla CMS will show as -> /joomla/administrator/index.php

It is important because this uri contains the login page to access the web portal therefore we will be examining the traffic coming into this admin panel for a potential brute-force attack.

![alt text](ea62d4ec767a649904b5f5bba9ba1d62.png)

Reference: https://www.joomla.org/administrator/index.php

We can narrow down our search to see the requests sent to the login portal using this information.

Search query: index=botsv1 imreallynotbatman.com sourcetype=stream:http dest_ip="192.168.250.70"  uri="/joomla/administrator/index.php"

Query Explanation: We are going to add uri="/joomla/administrator/index.php" in the search query to show the traffic coming into this URI.

![alt text](83b8b3e58e245701708a7e7ccac8c748.png)

form_data The field contains the requests sent through the form on the admin panel page, which has a login page. We suspect the attacker may have tried multiple credentials in an attempt to gain access to the admin panel. To confirm, we will dig deep into the values contained within the form_data field, as shown below:

Search Query:` index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" | table _time uri src_ip dest_ip form_data`

Query Explanation: We will add this -> `| table _time uri src_ip dest_ip form_data` to create a table containing important fields as shown below:

![alt text](1738f09ad30036c48e6849f7f8123e3e.png)

If we keep looking at the results, we will find two interesting fields username that includes the single username admin in all the events and another field passwd that contains multiple passwords in it, which shows the attacker from the IP 23.22.63.114 Was trying to guess the password by brute-forcing and attempting numerous passwords.

The time elapsed between multiple events also suggests that the attacker was using an automated tool as various attempts were observed in a short time.

## Extracting Username and Passwd Fields using Regex

Looking into the logs, we see that these fields are not parsed properly. Let us use Regex in the search to extract only these two fields and their values from the logs and display them.

We can display only the logs that contain the username and passwd values in the form_data field by adding `form_data=*username*passwd*` in the above search.

Search Query: `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* | table _time uri src_ip dest_ip form_data`

![alt text](9c47791d96dbadf8ab0d6a0adf1a9508.png)

It's time to use Regex (regular expressions) to extract all the password values found against the field passwd in the logs. To do so, Splunk has a function called rex. If we type it in the search head, it will show detail and an example of how to use it to extract the values.

![alt text](5ff9ecd4bf13a65356c0f6b9431d90c5.png)

Now, let's use Regex.  `rex field=form_data "passwd=(?<creds>\w+)"` To extract the passwd values only. This will pick the `form_data` field and extract all the values found with the field. `creds`.

Search Query:`index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd* | rex field=form_data "passwd=(?<creds>\w+)"  | table src_ip creds`

![alt text](594dedebeb2d2d5a7cc6cae8d1ebc226.gif)

We have extracted the passwords being used against the username admin on the admin panel of the webserver. If we examine the fields in the logs, we will find two values against the field `http_user_agent` as shown below:

![alt text](c8f99804c3e8a60170be32c01cdc0857.png)

The first value clearly shows attacker used a python script to automate the brute force attack against our server. But one request came from a Mozilla browser. WHY? To find the answer to this query, let's slightly change to the about search query and add `http_user_agent` a field in the search head.

Let's create a table to display key fields and values by appending -> `| table _time src_ip uri http_user_agent creds` in the search query as shown below.

Search Query: `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd* | rex field=form_data "passwd=(?<creds>\w+)" |table _time src_ip uri http_user_agent creds`

![alt text](ef2cbed333760fbe7d2fa7c507d2c625.png)

This result clearly shows a continuous brute-force attack attempt from an IP 23.22.63.114 and 1 password attempt batman from IP 40.80.148.42 using the Mozilla browser.


## Q & A

Q1 What was the URI which got multiple brute force attempts?

A1 /joomla/administrator/index.php

Q2 Against which username was the brute force attempt made?

A2 admin

Q3 What was the correct password for admin access to the content management system running imreallynotbatman.com?

A3 batman

Q4 How many unique passwords were attempted in the brute force attempt?

A4 412

Q5 What IP address is likely attempting a brute force password attack against imreallynotbatman.com?

A5 23.22.63.114

Q6 After finding the correct password, which IP did the attacker use to log in to the admin panel?

A6 40.80.148.42

![alt text](image-29.png)




# Installation Phase

Once the attacker has successfully exploited the security of a system, he will try to install a backdoor or an application for persistence or to gain more control of the system. This activity comes under the installation phase.

In the previous Exploitation phase, we found evidence of the webserver iamreallynotbatman.com getting compromised via brute-force attack by the attacker using the python script to automate getting the correct password. The attacker used the IP 23.22.63.114 for the attack and the IP 40.80.148.42 to log in to the server. This phase will investigate any payload / malicious program uploaded to the server from any attacker's IPs and installed into the compromised server.

To begin an investigation, we first would narrow down any http traffic coming into our server 192.168.250.70 containing the term ".exe." This query may not lead to the findings, but it's good to start from one extension and move ahead.

Search Query: `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" *.exe`

![alt text](4097da92bb83bd61cdacec4539c58d67.gif)

With the search query in place, we are looking for the fields that could have some values of our interest. As we could not find the file name field, we looked at the missing fields and saw a field. `part_filename{}`.

Observing the interesting fields and values, we can see the field `part_filename{}` contains the two file names. an executable file `3791.exe` and a PHP file `agent.php`

![alt text](f2206e28fac1af4e5033d1eb7cd7f29d.png)

Next, we need to find if any of these files came from the IP addresses that were found to be associated with the attack earlier.

Click on the file name; it will be added to the search query, then look for the field c_ip, which seems to represent the client IP.

Search Query:`index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" "part_filename{}"="3791.exe"`

![alt text](e8f2b1f9924e74acaf2224cd7c13f6f6.png)

### Was this file executed on the server after being uploaded?

We have found that file 3791.exe was uploaded on the server. The question that may come to our mind would be, was this file executed on the server? We need to narrow down our search query to show the logs from the host-centric log sources to answer this question.

Search Query: `index=botsv1 "3791.exe"`

![alt text](2dd77a76ba3366bf822576b7600d4669.png)

Following the Host-centric log, sources were found to have traces of the executable 3791. exe.

    Sysmon
    WinEventlog
    fortigate_utm

For the evidence of execution, we can leverage sysmon and look at the EventCode=1 for program execution.

Reference: https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon

![alt text](0135d57671ea197866054124115cfb4c.png)

Search Query: `index=botsv1 "3791.exe" sourcetype="XmlWinEventLog" EventCode=1`

Query Explanation: This query will look for the process Creation logs containing the term "3791.exe" in the logs.

![alt text](140a87acbf87ae7b9cf62f41dd93acdb.png)

Looking at the output, we can clearly say that this file was executed on the compromised server. We can also look at other host-centric log sources to confirm the result.

## Q & A

Q1 Sysmon also collects the Hash value of the processes being created. What is the MD5 HASH of the program 3791.exe?

A1 AAE3F5A29935E6ABCC2C2754D12A9AF0

![alt text](image-30.png)

Q2 Looking at the logs, which user executed the program 3791.exe on the server?

A2 NT AUTHORITY\IUSR

![alt text](image-31.png)

Q3 Search the hash on virustotal. What other name is associated with this file 3791.exe?

A3 ab.exe

![alt text](image-32.png)



# Action on Objectives

As the website was defaced due to a successful attack by the adversary, it would be helpful to understand better what ended up on the website that caused defacement.

As an analyst, our first quest could be to figure out the traffic flow that could lead us to the answer to this question. There can be a different approach to finding the answer to this question. We will start our investigation by examining the Suricata log source and the IP addresses communicating with the webserver 192.168.250.70.

Search Query:`index=botsv1 dest=192.168.250.70 sourcetype=suricata`

![alt text](47741c5563b7aebe667ec7eafdeaf1b3.png)

The logs do not show any external IP communicating with the server. Let us change the flow direction to see if any communication originates from the server.

Search Query: `index=botsv1 src=192.168.250.70 sourcetype=suricata`

![alt text](9cdce04d736980734ede35d17bc9d9a7.png)

What is interesting about the output? Usually, the web servers do not originate the traffic. The browser or the client would be the source, and the server would be the destination. Here we see three external IPs towards which our web server initiates the outbound traffic. There is a large chunk of traffic going to these external IP addresses, which could be worth checking.

Pivot into the destination IPs one by one to see what kind of traffic/communication is being carried out.

Search Query: `index=botsv1 src=192.168.250.70 sourcetype=suricata dest_ip=23.22.63.114`

![alt text](d012293c246dcc717ab0c80a7190845b.png)

The URL field shows 2 PHP files and one jpeg file. This jpeg file looks interesting. Let us change the search query and see where this jpeg file came from.

Search Query: `index=botsv1 url="/poisonivy-is-coming-for-you-batman.jpeg" dest_ip="192.168.250.70" | table _time src dest_ip http.hostname url`

![alt text](da31347a03f68b6e9998e66db946dccb.gif)

The end result clearly shows a suspicious jpeg `poisonivy-is-coming-for-you-batman.jpeg` was downloaded from the attacker's host `prankglassinebracket.jumpingcrab.com` that defaced the site.

![alt text](b71e2d7ed8b035a368d34ce02441a105.png)


## Q & A

Q1 What is the name of the file that defaced the imreallynotbatman.com website ?

A1 poisonivy-is-coming-for-you-batman.jpeg 

Q2 Fortigate Firewall 'fortigate_utm' detected SQL attempt from the attacker's IP 40.80.148.42. What is the name of the rule that was triggered during the SQL Injection attempt?

A2 HTTP.URI.SQL.Injection

![alt text](image-33.png)

![alt text](image-34.png)



# Command and Control Phase

The attacker uploaded the file to the server before defacing it. While doing so, the attacker used a Dynamic DNS to resolve a malicious IP. Our objective would be to find the IP that the attacker decided the DNS.

To investigate the communication to and from the adversary's IP addresses, we will be examining the network-centric log sources mentioned above. We will first pick `fortigate_utm` to review the firewall logs and then move on to the other log sources.

Search Query: `index=botsv1 sourcetype=fortigate_utm"poisonivy-is-coming-for-you-batman.jpeg"`

![alt text](a2df650b7d76e7cc7a795b8d0b627bfe.png)

Looking into the Fortinet firewall logs, we can see the src IP, destination IP, and URL. Look at the fields on the left panel and the field url contains the FQDN (Fully Qualified Domain Name).

![alt text](e5cda837fe7a7cbfa791515b49756f69.png)


Though we have found the answer, we can verify other log sources.
Let us verify the answer by looking at another log source.stream:http.

Search Query: `index=botsv1 sourcetype=stream:http dest_ip=23.22.63.114 "poisonivy-is-coming-for-you-batman.jpeg" src_ip=192.168.250.70`

![alt text](495918ac13b99ae950a0ac470fa349fc.png)

We have identified the suspicious domain as a Command and Control Server, which the attacker contacted after gaining control of the server.

Note: We can also confirm the domain by looking at the last log source `stream:dns` to see what DNS queries were sent from the webserver during the infection period.


## Q & A

Q1 This attack used dynamic DNS to resolve to the malicious IP. What fully qualified domain name (FQDN) is associated with this attack?

A1 prankglassinebracket.jumpingcrab.com




# Weaponization Phase

In the weaponization phase, the adversaries would:

-    Create Malware / Malicious document to gain initial access / evade detection etc.
-    Establish domains similar to the target domain to trick users.
-    Create a Command and Control Server for the post-exploitation communication/activity etc.

We have found some domains / IP addresses associated with the attacker during the investigations. This task will mainly look into OSINT sites to see what more information we can get about the adversary.

So far, we have found a domain `prankglassinebracket.jumpingcrab.com` associated with this attack. Our first task would be to find the IP address tied to the domains that may potentially be pre-staged to attack Wayne Enterprise.
In the following exercise, we will be searching the online Threat Intel sites for any information like IP addresses/domains / Email addresses associated with this domain which could help us know more about this adversary.

## Robtex:
Robtex (https://www.robtex.com/) is a Threat Intel site that provides information about IP addresses, domain names, etc.

Please search for the domain on the robtex site and see what we get. We will get the IP addresses associated with this domain.

![alt text](7ad2296f02b00a73a3ae2e4182fa7cfc.png)

Some domains/subdomains associated with this domain:

![alt text](c6aa355d30ed9425cd6e923526a03d46.png)

Reference: https://www.robtex.com/dns-lookup/prankglassinebracket.jumpingcrab.com

Next, search for the IP address 23.22.63.114 on this Threat Intel site.

![alt text](2a9dd066e2b6ef2cd55a5e0c04983776.png)

What did we find? this IP is associated with some domains that look pretty similar to the WAYNE Enterprise site.

Reference: https://www.robtex.com/ip-lookup/23.22.63.114

![alt text](87794e9d70b8b0dac729232443427181.png)

## Virustotal

Virustotal is an OSINT site used to analyze suspicious files, domains, IP, etc. Let's now search for the IP address on the virustotal site. If we go to the RELATIONS tab, we can see all the domains associated with this IP which look similar to the Wayn Enterprise company. 

![alt text](b217030ec313023a8d811ad513a28378.png)

In the domain list, we saw the domain that is associated with the attacker www[.]po1s0n1vy[.]com . Let us search for this domain on the virustotal.

![alt text](0d1024a79200a34705ac77b986782104.png)

We can also look for the whois information on this site -> whois.domaintools.com to see if we can find something valuable.

![alt text](a306319398fa56470363ca0f41cd814f.png)


## Q & A

Q1 What IP address has P01s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises?

A1 23.22.63.114

Q2 Based on the data gathered from this attack and common open-source intelligence sources for domain names, what is the email address that is most likely associated with the P01s0n1vy APT group? 

Note: Mind the spelling you get different results if you look up P01s0n1vy Po1s0n1vy, etc. po1s0n1vy worked for me best at Alienvault

A2 	lillian.rose@po1s0n1vy.com 

![alt text](image-35.png)



# Delivery Phase

Attackers create malware and infect devices to gain initial access or evade defenses and find ways to deliver it through different means. We have identified various IP addresses, domains and Email addresses associated with this adversary. Our task for this lesson would be to use the information we have about the adversary and use various Threat Hunting platforms and OSINT sites to find any malware linked with the adversary.

Threat Intel report suggested that this adversary group Poison lvy appears to have a secondary attack vector in case the "initial compromise" fails. Our objective would be to understand more about the attacker and their methodology and correlate the information found in the logs with various threat Intel sources.

## OSINT sites

-    Virustotal
-    ThreatMiner
-    Hybrid-Analysis

## ThreatMiner

Let's start our investigation by looking for the IP 23.22.63.114 on the Threat Intel site ThreatMiner. https://www.threatminer.org/host.php

![alt text](994b52e66e64ffba61ca57d32ace6a54.png)

We found three files associated with this IP, from which one file with the hash value  `c99131e0169171935c5ac32615ed6261` seems to be malicious and something of interest.

Now, click on this MD5 hash value to see the metadata and other important information about this particular file.

![alt text](511a309aacc571f2176931686df681e0.png)

## Virustotal

Open virustotal.com and search for the hash on the virustotal now. Here, we can get information about the metadata about this Malware in the Details tab.

![alt text](c380913c90e52016683cbcfe9174b35e.png)

![alt text](8edbbf929731d7718587d3c1adc66648.png)

## Hybrid-Analysis

Hybrid Analysis is a beneficial site that shows the behavior Analysis of any malware. Here you can look at all the activities performed by this Malware after being executed. Some of the information that Hybrid-Analysis provides are:

-    Network Communication.
-    DNS Requests
-    Contacted Hosts with Country Mapping
-    Strings
-    MITRE ATT&CK Mapping
-    Malicious Indicators.
-    DLLs Imports / Exports
-    Mutex Information if created
-    File Metadata
-    Screenshots

![alt text](6ef05247bb5c92e91d0a2894f219758a.png)

Scroll down, and you will get a lot of information about this Malware.

![alt text](7a714d6ca3a44c0c570c45cb2711b660.png)

Reference: https://www.hybrid-analysis.com/sample/9709473ab351387aab9e816eff3910b9f28a7a70202e250ed46dba8f820f34a8?environmentId=100


## Q & A

Q1 What is the HASH of the Malware associated with the APT group?

A1 c99131e0169171935c5ac32615ed6261

they refer to the MD5 hash

![alt text](image-36.png)

Q2 What is the name of the Malware associated with the Poison Ivy Infrastructure?

A2 MirandaTateScreensaver.scr.exe




# Conclusion

In this fun exercise, as a SOC Analyst, we have investigated a cyber-attack where the attacker had defaced a website 'imreallynotbatman.com' of the Wayne Enterprise. We mapped the attacker's activities into the 7 phases of the Cyber Kill Chain. Let us recap everything we have found so far:

## Reconnaissance Phase:

We first looked at any reconnaissance activity from the attacker to identify the IP address and other details about the adversary.

### Findings:

-    IP Address 40.80.148.42 was found to be scanning our webserver.
-    The attacker was using Acunetix as a web scanner.

## Exploitation Phase:

We then looked into the traces of exploitation attempts and found brute-force attacks against our server, which were successful.

### Findings:

-    Brute force attack originated from IP 23.22.63.114.
-    The IP address used to gain access: 40.80.148.42
-    142 unique brute force attempts were made against the server, out of which one attempt was successful

## Installation Phase:

Next, we looked at the installation phase to see any executable from the attacker's IP Address uploaded to our server.

### Findings:

-    A malicious executable file 3791.exe was observed to be uploaded by the attacker.
-    We looked at the sysmon logs and found the MD5 hash of the file.

## Action on Objective:

After compromising the web server, the attacker defaced the website.

### Findings:

-    We examined the logs and found the file name used to deface the webserver.

## Weaponization Phase:

We used various threat Intel platforms to find the attacker's infrastructure based on the following information we saw in the above activities.

### Information we had:

Domain: prankglassinebracket.jumpingcrab.com
IP Address: 23.22.63.114

### Findings:

-    Multiple masquerading domains were found associated with the attacker's IPs.
-    An email of the user Lillian.rose@po1s0n1vy.com was also found associated with the attacker's IP address.

## Deliver Phase:

In this phase, we again leveraged online Threat Intel sites to find malware associated with the adversary's IP address, which appeared to be a secondary attack vector if the initial compromise failed.

### Findings:

-    A malware name MirandaTateScreensaver.scr.exe was found associated with the adversary.
-    MD5 of the malware was c99131e0169171935c5ac32615ed6261






















