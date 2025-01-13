Objective

After participating in one too many incident response activities, PicoSecure has decided to conduct a threat simulation and detection engineering engagement to bolster its malware detection capabilities. You have been assigned to work with an external penetration tester in an iterative purple-team scenario. The tester will be attempting to execute malware samples on a simulated internal user workstation. At the same time, you will need to configure PicoSecure's security tools to detect and prevent the malware from executing.

Following the Pyramid of Pain's ascending priority of indicators, your objective is to increase the simulated adversaries' cost of operations and chase them away for good. Each level of the pyramid allows you to detect and prevent various indicators of attack.

Room Prerequisites

Completing the preceding rooms in the Cyber Defence Frameworks module will be beneficial before venturing into this challenge. Specifically, the following:

    The Pyramid of Pain
    MITRE

Connection Details

Please click Start Machine to deploy the application, and navigate to https://LAB_WEB_URL.p.thmlabs.com once the URL has been populated.

Note: It may take a few minutes to deploy the machine entirely. If you receive a "Bad Gateway" response, wait a few minutes and refresh the page.

# 1
General Info - sample1.exe

File Name	sample1.exe

File Size	202.50 KB

File Type	PE32+ executable (GUI) x86-64, for MS Windows

Analysis Date	September 5, 2023

OS	Windows 10x64 v1803

Tags	Trojan.Metasploit.A

MIME	application/x-dosexec

MD5	cbda8ae000aa9cbe7c8b982bae006c2a

SHA1	83d2791ca93e58688598485aa62597c0ebbf7610

SHA256	9c550591a25c6228cb7d74d970d133d75c961ffed2ef7180144859cc09efca8c

Behaviour Analysis
Malicious

METASPLOIT was detected

    sample1.exe (PID: 2492)

Suspicious

Connects to unusual port

    sample1.exe (PID: 2492)

Info

Reads the machine GUID from the registry

    sample1.exe (PID: 2492)

The process checks LSA protection

    sample1.exe (PID: 2492)

Reads the computer name

    sample1.exe (PID: 2492)

Checks supported languages

    sample1.exe (PID: 2492) 

# 2

General Info - sample2.exe

File Name	sample2.exe

File Size	202.73 KB

File Type	PEXE - PE32+ executable (GUI) x86-64, for MS Windows

Analysis Date	September 5, 2023

OS	Windows 10x64 v1803

Tags	Trojan.Metasploit.A

MIME	application/x-dosexec

MD5	4d661bf605d6b0b15915a533b572a6bd

SHA1	6878976974c27c8547cfc5acc90fb28ad2f0e975

SHA256	d576245e85e6b752b2fdffa43abaab1b2e1383556b0169fd04924d6cebc1cdf9

Behaviour Analysis
Malicious

METASPLOIT was detected

    sample2.exe (PID: 1927)

Suspicious

Connects to unusual IP address

    sample2.exe (PID: 1927)

Connects to unusual port

    sample2.exe (PID: 1927)

Info

Reads the machine GUID from the registry

    sample2.exe (PID: 1927)

The process checks LSA protection

    sample2.exe (PID: 1927)

Reads the computer name

    sample2.exe (PID: 1927)

Checks supported languages

    sample2.exe (PID: 1927)
```
Network Activity
HTTP(S) requests
1
TCP/UDP connections
3
DNS requests
0
Threats
0
HTTP requests
PID	    Process	    Method	IP	                URL
1927	sample2.exe	GET	    154.35.10.113:4444	http://154.35.10.113:4444/uvLk8YI32

Connections
PID 	Process 	IP 	                Domain 	ASN
1927	sample2.exe	154.35.10.113:4444	-	    Intrabuzz Hosting Limited
1927	sample2.exe	40.97.128.3:443	    -	    Microsoft Corporation
1927	sample2.exe	40.97.128.4:443  	-	    Microsoft Corporation
```

# 3

General Info - sample3.exe

File Name	sample3.exe

File Size	207.12 KB

File Type	PEXE - PE32+ executable (GUI) x86-64, for MS Windows

Analysis Date	September 5, 2023

OS	Windows 10x64 v1803

Tags	Trojan.Metasploit.A

MIME	application/x-dosexec

MD5	e31f0c62927d9d5a897b4c45e3c64dbc

SHA1	a92d3de6b1e3ab295f10587ca75f15318cb85a7b

SHA256	acb9b1260bcd08a465f9f300ac463b9b1215c097ebe44610359bb80881fe6a05

Behaviour Analysis
Malicious

METASPLOIT was detected

    sample3.exe (PID: 1021)

Downloads executable files from the Internet

    backdoor.exe (PID: 2712)

Suspicious

Connects to unusual IP address

    sample3.exe (PID: 1021)

Connects to unusual port

    sample3.exe (PID: 1021)

Info

Reads the machine GUID from the registry

    sample3.exe (PID: 1021)

The process checks LSA protection

    sample3.exe (PID: 1021)

Reads the computer name

    sample3.exe (PID: 1021)

Checks supported languages

    sample3.exe (PID: 1021)
```
Network Activity
HTTP(S) requests
2
TCP/UDP connections
4
DNS requests
2
Threats
0

HTTP requests
PID	Process	Method	IP	URL
1021	sample3.exe	GET	62.123.140.9:1337	http://emudyn.bresonicz.info:1337/kzn293la
1021	sample3.exe	GET	62.123.140.9:80	http://emudyn.bresonicz.info/backdoor.exe

Connections
PID 	Process 	IP 	                Domain 	                ASN
1021	sample3.exe	40.97.128.4:443	    services.microsoft.com	Microsoft Corporation
1021	sample3.exe	62.123.140.9:1337	emudyn.bresonicz.info	XplorIta Cloud Services
1021	sample3.exe	62.123.140.9:80	    emudyn.bresonicz.info	XplorIta Cloud Services
2712	backdoor.exe	62.123.140.9:80	emudyn.bresonicz.info	XplorIta Cloud Services

DNS requests
Domain 	                IP
services.microsoft.com	40.97.128.4
emudyn.bresonicz.info	62.123.140.9

```

# 4

General Info - sample4.exe

File Name	sample4.exe

File Size	219.46 KB

File Type	PEXE - PE32+ executable (GUI) x86-64, for MS Windows

Analysis Date	September 5, 2023

OS	Windows 10x64 v1803

Tags	None

MIME	application/x-dosexec

MD5	5f29ff19d99fe244eaf5835ce01a4631

SHA1	cd12d2328f700ae1ba1296a5f011bfc5a49f456d

SHA256	a80cffb40cea83c1a20973a5b803828e67691f71f3c878edb5a139634d7dd422

Behaviour Analysis
Malicious

Disables Windows Defender Real-time monitoring

    sample4.exe (PID: 3806)

Downloads executable files from the Internet

    backdoor.exe (PID: 1367)

Suspicious

Connects to unusual IP address

    sample4.exe (PID: 3806)

Connects to unusual port

    sample4.exe (PID: 3806)

Makes changes to the registry

    sample4.exe (PID: 3806)

Info

Reads the machine GUID from the registry

    sample4.exe (PID: 3806)

The process checks LSA protection

    sample4.exe (PID: 3806)

Reads the computer name

    sample4.exe (PID: 3806)

Checks supported languages

    sample4.exe (PID: 3806)

```
Network Activity
HTTP(S) requests
2
TCP/UDP connections
3
DNS requests
1
Threats
0
HTTP requests
PID	Process	Method	IP	URL
3806	sample4.exe	GET	102.23.20.118:1337	http://cranes0ft.iniware.xyz:1337/ab9z83ja

3806	sample4.exe	GET	102.23.20.118:80	http://cranes0ft.iniware.xyz/backdoor.exe

Connections

PID 	Process 	IP 	Domain 	ASN

3806	sample4.exe	102.23.20.118:1337	cranes0ft.iniware.xyz	XplorIta Cloud Services

3806	sample4.exe	102.23.20.118:80	cranes0ft.iniware.xyz	XplorIta Cloud Services

1367	backdoor.exe	102.23.20.118:80	cranes0ft.iniware.xyz	XplorIta Cloud Services

DNS requests

Domain 	IP
cranes0ft.iniware.xyz	102.23.20.118

Registry Activity
Total events
3
Read events
1
Write events
2
Delete events
0

Modification events
(PID) Process: (3806) sample4.exe	Key: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
Operation: write	Name: DisableRealtimeMonitoring
Value: 1

(PID) Process: (1928) explorer.exe	Key: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
Operation: write	Name: EnableBalloonTips
Value: 1

(PID) Process: (9876) notepad.exe	Key: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.txt
Operation: read	Name: Progid
Value: txtfile
```

# 5
Viewing attachment: outgoing_connections.log
```
2023-08-15 09:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 09:23:45 | Source: 10.10.15.12 | Destination: 43.10.65.115 | Port: 443 | Size: 21541 bytes
2023-08-15 09:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:00:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
2023-08-15 10:14:21 | Source: 10.10.15.12 | Destination: 87.32.56.124 | Port: 80  | Size: 1204 bytes
2023-08-15 10:30:00 | Source: 10.10.15.12 | Destination: 51.102.10.19 | Port: 443 | Size: 97 bytes
...
```

# 6

Viewing attachment: commands.log
```
dir c:\ >> %temp%\exfiltr8.log
dir "c:\Documents and Settings" >> %temp%\exfiltr8.log
dir "c:\Program Files\" >> %temp%\exfiltr8.log
dir d:\ >> %temp%\exfiltr8.log
net localgroup administrator >> %temp%\exfiltr8.log
ver >> %temp%\exfiltr8.log
systeminfo >> %temp%\exfiltr8.log
ipconfig /all >> %temp%\exfiltr8.log
netstat -ano >> %temp%\exfiltr8.log
net start >> %temp%\exfiltr8.log
```