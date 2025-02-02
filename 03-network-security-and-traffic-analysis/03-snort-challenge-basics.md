# Writing IDS Rules (HTTP)

Navigate to the task 2 folder.

Use the given pcap file.

Write a single rule to detect "all TCP port 80 traffic" packets in the given pcap file. 

Q: What is the number of detected packets?

Note: You must answer this question correctly before answering the rest of the questions in this task.

Hint - You need to investigate inbound and outbound traffic on port 80. Make sure to only use a single rule, or you potentially get wrong results for the next questions.

A: 164

`alert tcp any 80 <> any any (msg:"Detect port 80 traffic";sid:1000001;rev:1)`

Investigate the log file.

Q: What is the destination address of packet 63?

Hint - "-n" parameter helps analyze the "n" number of packets.

A: 216.239.59.99

`sudo snort -r snort.log.1738144686 -n 63`

Investigate the log file.

Q: What is the ACK number of packet 64?

A: 0x2E6B5384

`sudo snort -r snort.log.1738144686 -n 64`

Investigate the log file.

Q: What is the SEQ number of packet 62?

A: 0x36C21E28

Investigate the log file.

Q: What is the TTL of packet 65?

A: 128

`sudo snort -r snort.log.1738144686 -n 65`

Investigate the log file.

Q: What is the source IP of packet 65?

A: 145.254.160.237

Investigate the log file.

Q: What is the source port of packet 65?

A: 3372

# Writing IDS Rules (FTP)

Navigate to the task folder 3.

Use the given pcap file.

Write a single rule to detect "all TCP port 21"  traffic in the given pcap.

Q: What is the number of detected packets?

A: 307

`alert tcp any 21 <> any any (msg:"Detect all TCP port 21 traffic",sid:1000001;rev:1)`

Investigate the log file.

Q: What is the FTP service name?

Hint - Strings or the -a option with grep might help.

A: Microsoft FTP Service

`sudo strings snort.log.1738145709 | grep FTP`

Clear the previous log and alarm files.

Deactivate/comment on the old rules.

Write a rule to detect failed FTP login attempts in the given pcap.

Q: What is the number of detected packets?

Hint - Each failed FTP login attempt prompts a default message with the pattern; "530 User". Try to filter the given pattern in the inbound FTP traffic.

A: 41

`alert tcp any 21 <> any any (msg:"Detect all failed FTP login attempts";content:"530 User";sid:1000001;rev:1)`

Clear the previous log and alarm files.

Deactivate/comment on the old rule.

Write a rule to detect successful FTP logins in the given pcap.

Q: What is the number of detected packets?

Hint - Each successful FTP login attempt prompts a default message with the pattern; "230 User".Try to filter the given pattern in the FTP traffic.

A: 1

`alert tcp any 21 <> any any (msg:"Detect all successful FTP login attempts";content:"230 User";sid:1000001;rev:1)`

Clear the previous log and alarm files.

Deactivate/comment on the old rule.

Write a rule to detect FTP login attempts with a valid username but no password entered yet.

Q: What is the number of detected packets?

Hint - Each FTP login attempt with a valid username prompts a default message with the pattern; "331 Password". Try to filter the given pattern in the FTP traffic.

A: 42

`alert tcp any 21 <> any any (msg:"Detect FTP login attempts with valid username but no password";content:"331 Password";sid:1000001;rev:1)`

Clear the previous log and alarm files.

Deactivate/comment on the old rule.

Write a rule to detect FTP login attempts with the "Administrator" username but no password entered yet.

Q: What is the number of detected packets?

Hint - You can use the "content" filter more than one time.

A: 7

`alert tcp any 21 <> any any (msg:"Detect FTP login attempts with Administrator username but no password";content:"Administrator";content:"331 Password";sid:1000001;rev:1)`

# Writing IDS Rules (PNG)

Use the given pcap file.

Write a rule to detect the PNG file in the given pcap.

Investigate the logs and identify the software name embedded in the packet.

A: Adobe ImageReady

Look for File Magic Numbers, for PNG: 89 50 4E 47 0D 0A 1A 0A https://en.wikipedia.org/wiki/List_of_file_signatures

create a new rule:

`alert tcp any any <> any any  (msg: "png Packet Found";content:"|89 50 4E 47 0D 0A 1A 0A|";sid:100001; rev:1)`

Note: Put the hex number for png between | | as shown above

Inspect the log:
```
ubuntu@ip-10-10-166-243:~/Desktop/Exercise-Files/TASK-4 (PNG)$ sudo strings snort.log.1738232740 
IHDR
tEXtSoftware
Adobe ImageReadyq
.IDATx
nvfw
A)_,
` ^,
XBy6
`'?/
]}gb
lYy[)
3W}B=
OnOh
WLCO/
RnR7
0WGJ
```
Clear the previous log and alarm files.

Deactivate/comment on the old rule.

Write a rule to detect the GIF file in the given pcap.

Investigate the logs and identify the image format embedded in the packet.

A: GIF89a

Magic numbers for GIF:
![alt text](image.png)

`alert tcp any any <> any any  (msg:"gif Packet Found";content:"GIF89a";sid:100001;rev:1)`

```
ubuntu@ip-10-10-166-243:~/Desktop/Exercise-Files/TASK-4 (PNG)$ sudo strings snort.log.1738233769 
GIF89a
GIF89a
GIF89a
GIF89a
```

# Writing IDS Rules (Torrent Metafile)

Use the given pcap file.

Write a rule to detect the torrent metafile in the given pcap.

Q: What is the number of detected packets?

Hint - Torrent metafiles have a common name extension (.torrent). Try to filter the given pattern in the TCP traffic.

A: 2

`alert tcp any any <> any any (msg:"Torrrent file found";content:".torrent";sid:1000001;rev:1)`

Investigate the log/alarm files.

Q: What is the name of the torrent application?

A: bittorrent

```
ubuntu@ip-10-10-166-243:~/Desktop/Exercise-Files/TASK-5 (TorrentMetafile)$ sudo strings snort.log.1738234245 
GET /announce?info_hash=%01d%FE%7E%F1%10%5CWvAp%ED%F6%03%C49%D6B%14%F1&peer_id=%B8js%7F%E8%0C%AFh%02Y%967%24e%27V%EEM%16%5B&port=41730&uploaded=0&downloaded=0&left=3767869&compact=1&ip=127.0.0.1&event=started HTTP/1.1
Accept: application/x-bittorrent
Accept-Encoding: gzip
User-Agent: RAZA 2.1.0.0
Host: tracker2.torrentbox.com:2710
Connection: Keep-Alive
GET /announce?info_hash=%01d%FE%7E%F1%10%5CWvAp%ED%F6%03%C49%D6B%14%F1&peer_id=%B8js%7F%E8%0C%AFh%02Y%967%24e%27V%EEM%16%5B&port=41730&uploaded=0&downloaded=0&left=3767869&compact=1&ip=127.0.0.1 HTTP/1.1
Accept: application/x-bittorrent
Accept-Encoding: gzip
User-Agent: RAZA 2.1.0.0
Host: tracker2.torrentbox.com:2710
Connection: Keep-Alive
```
Investigate the log/alarm files.

Q: What is the MIME (Multipurpose Internet Mail Extensions) type of the torrent metafile?

A: application/x-bittorrent

Investigate the log/alarm files.

Q: What is the hostname of the torrent metafile?

A: tracker2.torrentbox.com



