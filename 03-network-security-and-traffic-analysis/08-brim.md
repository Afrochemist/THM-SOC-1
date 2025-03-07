# What is Brim?
![alt text](ff4d1d9dead9acca747fc48cc2f43ec2.png)

Brim is an open-source desktop application that processes pcap files and logs files, with a primary focus on providing search and analytics. It uses the Zeek log processing format. It also supports Zeek signatures and Suricata Rules for detection.

It can handle two types of data as an input;
- Packet Capture Files: Pcap files created with tcpdump, tshark and Wireshark like applications.
- Log Files: Structured log files like Zeek logs.

Brim is built on open-source platforms:
- Zeek: Log generating engine.
- Zed Language: Log querying language that allows performing keywoırd searches with filters and pipelines.
- ZNG Data Format: Data storage format that supports saving data streams.
- Electron and React: Cross-platform UI.

### Why Brim?

Ever had to investigate a big pcap file? Pcap files bigger than one gigabyte are cumbersome for Wireshark. Processing big pcaps with tcpdump and Zeek is efficient but requires time and effort. Brim reduces the time and effort spent processing pcap files and investigating the log files by providing a simple and powerful GUI application.

### Brim vs Wireshark vs Zeek

While each of them is powerful and useful, it is good to know the strengths and weaknesses of each tool and which one to use for the best outcome. As a traffic capture analyser, some overlapping functionalities exist, but each one has a unique value for different situations.

<b><i>The common best practice is handling medium-sized pcaps with Wireshark, creating logs and correlating events with Zeek, and processing multiple logs in Brim.</i></b>

<table class="table table-bordered"><tbody><tr><td><br></td><td>Brim</td><td>Wireshark</td><td><span data-testid="glossary-term" class="glossary-term">Zeek</span></td></tr><tr><td>Purpose</td><td><span data-testid="glossary-term" class="glossary-term">Pcap</span> processing; event/stream and log investigation.</td><td>Traffic sniffing. <span data-testid="glossary-term" class="glossary-term">Pcap</span> processing; packet and stream investigation.</td><td><span data-testid="glossary-term" class="glossary-term">Pcap</span> processing; event/stream and log investigation.</td></tr><tr><td><span data-testid="glossary-term" class="glossary-term">GUI</span></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td>✖<br></td></tr><tr><td>Sniffing</td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td><span data-testid="glossary-term" class="glossary-term">Pcap</span> processing</td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Log processing</td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Packet decoding</td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Filtering</td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Scripting<br></td><td>✖<br></td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Signature Support</td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Statistics</td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>File Extraction</td><td>✖<br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td><td><span style="font-family:&quot;Segoe UI Symbol&quot;, sans-serif;font-weight:700">✔</span><br></td></tr><tr><td>Handling&nbsp; pcaps over 1GB</td><td><span style="font-family:Ubuntu">Medium performance</span><br></td><td>Low performance<br></td><td><span style="font-family:Ubuntu">Good performance</span><br></td></tr><tr><td>Ease of Management</td><td>4/5</td><td>4/5</td><td>3/5</td></tr></tbody></table>


# The Basics

### Landing Page

Once you open the application, the landing page loads up. The landing page has three sections and a file importing window. It also provides quick info on supported file formats.
- Pools: Data resources, investigated pcap and log files.
- Queries: List of available queries.
- History: List of launched queries.

### Pools and Log Details

Pools represent the imported files. Once you load a pcap, Brim processes the file and creates Zeek logs, correlates them, and displays all available findings in a timeline, as shown in the image below. 

![alt text](e429e9a957eef2c68ed6f7a84d004fd6.png)

The timeline provides information about capture start and end dates. Brim also provides information fields. You can hover over fields to have more details on the field. The above image shows a user hovering over the Zeek's conn.log file and uid value. This information will help you in creating custom queries. The rest of the log details are shown in the right pane and provides details of the log file fields. Note that you can always export the results by using the export function located near the timeline.

You can correlate each log entry by reviewing the correlation section at the log details pane (shown on image below). This section provides information on the source and destination addresses, duration and associated log files. This quick information helps you answer the "Where to look next?" question and find the event of interest and linked evidence.
![alt text](b190e9dc7fd7ff3b32d5cdfa2838f64d.png)

You can also right-click on each field to filter and accomplish a list of tasks.

- Filtering values
- Counting fields
- Sorting (A-Z and Z-A)
- Viewing details 
- Performing whois lookup on IP address
- Viewing the associated packets in Wireshark

The image below demonstrates how to perform whois lookup and Wireshark packet inspection.
![alt text](0e9b4478872cb03531abccd80bdf32f8.png)

### Queries and History

Queries help us to correlate finding and find the event of interest. History stores executed queries.

![alt text](28cc8ffb12a9b997833779fb228a379e.png)

The image above demonstrates how to browse the queries and load a specific query from the library.

Queries can have names, tags and descriptions. Query library lists the query names, and once you double-click, it passes the actual query to the search bar.

You can double-click on the query and execute it with ease. Once you double-click on the query, the actual query appears on the search bar and is listed under the history tab.

The results are shown under the search bar. In this case, we listed all available log sources created by Brim. In this example, we only insert a pcap file, and it automatically creates nine types of Zeek log files. 

Brim has 12 premade queries listed under the "Brim" folder. These queries help us discover the Brim query structure and accomplish quick searches from templates.  You can add new queries by clicking on the "+" button near the "Queries" menu.
![alt text](05866c647f05235deaad8a9b32dbb454.png)

# Default Queries

### Activity Overview

This query provides general information on the pcap file. The provided information is valuable for accomplishing further investigation and creating custom queries. It is impossible to create advanced or case-specific queries without knowing the available log files.

The image below shows that there are 20 logs generated for the provided pcap file. 

![alt text](700e9a56564f3bb4ca7fdad421dc0cab.png)

### Windows Networking Activity

This query focuses on Windows networking activity and details the source and destination addresses and named pipe, endpoint and operation detection. The provided information helps investigate and understand specific Windows events like SMB enumeration, logins and service exploiting.

![alt text](8146a1b9eb1481fd8b4a03f3f8af0f63.png)

### Unique Network Connections and Connection received Data

These two queries provide information on unique connections and connection-data correlation. The provided info helps analysts detect weird and malicious connections and suspicious and beaconing activities. The uniq list provides a clear list of unique connections that help identify anomalies. The data list summarises the data transfer rate that supports the anomaly investigation hypothesis.

![alt text](b94be33d13d9c597c070f151b3521bb4.png)

### Unique DNS queries, HTTP Requests and HTTP POST Requests

These queries provide the list of the DNS queries and HTTP methods. The provided information helps analysts to detect anomalous DNS and HTTP traffic. You can also narrow the search by viewing the "HTTP POST" requests with the available query and modifying it to view the "HTTP GET" methods.

![alt text](3c9173d3c3c36f3f9972bba86e54f174.png)

![alt text](image-1.png)

### File Activity

This query provides the list of the available files. It helps analysts to detect possible data leakage attempts and suspicious file activity. The query provides info on the detected file MIME and file name and hash values (MD5, SHA1).

![alt text](138f5f08d57d005d47c168c42db7887d.png)

### Show IP Subnet

This query provides the list of the available IP subnets. It helps analysts detect possible communications outside the scope and identify out of ordinary IP addresses. 

![alt text](16d18107e659e30667e63f2b7175cfad.png)

### Suricata Alerts

These queries provide information based on Suricata rule results. Three different queries are available to view the available logs in different formats (category-based, source and destination-based, and subnet based). 

Note: Suricata is an open-source threat detection engine that can act as a rule-based Intrusion Detection and Prevention System. It is developed by the Open Information Security Foundation (OISF). Suricata works and detects anomalies in a similar way to Snort and can use the same signatures. 

![alt text](1fa588a68ed5d635ba8842ff3ecec6ad.png)

# Use cases

## Custom Queries and Use Cases

There are a variety of use case examples in traffic analysis. For a security analyst, it is vital to know the common patterns and indicators of anomaly or malicious traffic. In this task, we will cover some of them. Let's review the basics of the Brim queries before focusing on the custom and advanced ones.

### Brim Query Reference 

<table class="table table-bordered">
  <tbody>
    <tr>
      <td><b>Purpose</b></td>
      <td><b>Syntax</b></td>
      <td><b>Example Query</b></td>
    </tr>
    <tr>
      <td style="text-align:center">Basic search&nbsp;</td>
      <td style="text-align:center">
        You can search any string and numeric value.&nbsp;
      </td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>Find logs containing an IP address or any value.</span>
        </div>
        <div style="text-align:center"><code>10.0.0.1</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">Logical operators&nbsp;</td>
      <td style="text-align:center">Or, And, Not.&nbsp;</td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>Find logs contain three digits of an IP AND <span data-testid="glossary-term" class="glossary-term">NTP</span> keyword.</span>
        </div>
        <div style="text-align:center"><code>192 and NTP</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">Filter values</td>
      <td style="text-align:center">"field name" == "value"</td>
      <td>
        <p></p>
        <div style="text-align:center"><span>Filter source IP.</span></div>
        <div style="text-align:center"><code>id.orig_h==192.168.121.40</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">List specific log file contents<br></td>
      <td style="text-align:center">_path=="log name"<br></td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>List the contents of the conn log file.</span>
        </div>
        <div style="text-align:center"><code>_path=="conn"</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">Count field values&nbsp;</td>
      <td style="text-align:center">count () by "field"</td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>Count the number of the available log files.</span>
        </div>
        <div style="text-align:center"><code>count () by _path</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">Sort findings</td>
      <td style="text-align:center">sort</td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>Count the number of the available log files and sort
            recursively.</span>
        </div>
        <div style="text-align:center"><code>count () by _path | sort -r</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">Cut specific field from a log file</td>
      <td style="text-align:center">_path=="conn" | cut "field name"</td>
      <td>
        <p></p>
        <div style="text-align:center">
          <span>Cut the source IP, destination port and destination IP addresses
            from the conn log file.</span>
        </div>
        <div style="text-align:center"><code>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h</code></div>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">List unique values</td>
      <td style="text-align:center">uniq</td>
      <td>
        <p style="text-align:center">
          Show the unique network connections.&nbsp;
        </p>
        <p style="text-align:center"><code>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h | sort | uniq</code><br></p>
      </td>
    </tr>
  </tbody>
</table>

Note: It is highly suggested to use field names and filtering options and not rely on the blind/irregular search function. Brim provides great indexing of log sources, but it is not performing well in irregular search queries. The best practice is always to use the field filters to search for the event of interest. 

<table class="table table-bordered">
  <tbody>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Communicated Hosts</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Identifying the list of communicated hosts is the first step of the
          investigation. Security analysts need to know which hosts are actively
          communicating on the network to detect any suspicious and abnormal
          activity in the first place. This approach will help analysts to
          detect possible access violations, exploitation attempts and malware
          infections.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Frequently Communicated Hosts</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          After having the list of communicated hosts, it is important to
          identify which hosts communicate with each other most frequently. This
          will help security analysts to detect possible data exfiltration,
          exploitation and backdooring activities.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq -c | sort -r</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Most Active Ports</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Suspicious activities are not always detectable in the first place.
          Attackers use multiple ways of hiding and bypassing methods to avoid
          detection. However, since the data is evidence, it is impossible to
          hide the packet traces. Investigating the most active ports will help
          analysts to detect silent and well-hidden anomalies by focusing on the
          data bus and used services.&nbsp;
        </p>
        <p style="text-align:justify">
          <b>Query:</b>
          <code>_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count</code><br>
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<span style="text-align:left">&nbsp;</span><code>_path=="conn" | cut id.orig_h, id.resp_h, id.resp_p, service | sort id.resp_p | uniq -c | sort -r&nbsp;</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Long Connections</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          For security analysts, the long connections could be the first anomaly
          indicator. If the client is not designed to serve a continuous
          service, investigating the connection duration between two IP
          addresses can reveal possible anomalies like backdoors.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:&nbsp;</span><code>_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h, duration | sort -r duration</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Transferred Data&nbsp;</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Another essential point is calculating the transferred data size. If
          the client is not designed to serve and receive files and act as a
          file server, it is important to investigate the total bytes for each
          connection. Thus, analysts can distinguish possible data exfiltration
          or suspicious file actions like malware downloading and spreading.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:&nbsp;</span><code>_path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <a class="4HIRbGpP glossary-term"><span><span data-testid="glossary-term" class="glossary-term">DNS</span></span></a><span style="font-weight:700;text-align:justify">&nbsp;and <span data-testid="glossary-term" class="glossary-term">HTTP</span> Queries</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Identifying suspicious and out of ordinary domain connections and
          requests is another significant point for a security analyst. Abnormal
          connections can help detect&nbsp;<a class="5lC8Gyoa glossary-term"><span data-testid="glossary-term" class="glossary-term">C2</span></a>&nbsp;communications and possible compromised/infected hosts.
          Identifying the suspicious <span data-testid="glossary-term" class="glossary-term">DNS</span> queries and <span data-testid="glossary-term" class="glossary-term">HTTP</span> requests help security
          analysts to detect malware <span data-testid="glossary-term" class="glossary-term">C2</span> channels and support the investigation
          hypothesis.<br>
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="dns" | count () by query | sort -r</code><br>
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="http" | count () by uri | sort -r</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Suspicious Hostnames</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Identifying suspicious and out of ordinary hostnames helps analysts to
          detect rogue hosts. Investigating the <span data-testid="glossary-term" class="glossary-term">DHCP</span> logs provides the hostname
          and domain information.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="dhcp" | cut host_name, domain</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Suspicious IP Addresses</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          For security analysts, identifying suspicious and out of ordinary IP
          addresses is essential as identifying weird domain addresses. Since
          the connection logs are stored in one single log file (conn),
          filtering IP addresses is more manageable and provides more reliable
          results.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="conn" | put classnet := network_of(id.resp_h) | cut classnet | count() by classnet | sort -r</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Detect Files</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Investigating transferred files is another important point of traffic
          investigation. Performing this hunt will help security analysts to
          detect the transfer of malware or infected files by correlating the
          hash values. This act is also valuable for detecting transferring of
          sensitive files.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:&nbsp;</span><code>filename!=null</code><br>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify"><span data-testid="glossary-term" class="glossary-term">SMB</span> Activity</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Another significant point is investigating the <span data-testid="glossary-term" class="glossary-term">SMB</span> activity. This will
          help analysts to detect possible malicious activities like
          exploitation, lateral movement and malicious file sharing. When
          running an investigation, it is suggested to ask, "What is going on in
          <span data-testid="glossary-term" class="glossary-term">SMB</span>?".
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>_path=="dce_rpc" OR _path=="smb_mapping" OR _path=="smb_files"</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <span style="font-weight:700;text-align:justify">Known Patterns</span><br>
      </td>
      <td>
        <p style="text-align:justify">
          Known patterns represent alerts generated by security solutions. These
          alerts are generated against the common attack/threat/malware patterns
          and known by endpoint security products, firewalls and <span data-testid="glossary-term" class="glossary-term">IDS</span>/<span data-testid="glossary-term" class="glossary-term">IPS</span>
          solutions. This data source highly relies on available signatures,
          attacks and anomaly patterns. Investigating available log sources
          containing alerts is vital for a security analyst.
        </p>
        <p style="text-align:justify">
          Brim supports the <span data-testid="glossary-term" class="glossary-term">Zeek</span> and Suricata logs, so any anomaly detected by
          these products will create a log file. Investigating these log files
          can provide a clue where the analyst should focus.
        </p>
        <p style="text-align:justify">
          <span style="font-weight:bolder">Query:</span>&nbsp;<code>event_type=="alert" or _path=="notice" or _path=="signatures"</code><br>
        </p>
      </td>
    </tr>
  </tbody>
</table>

# Exercise: Threat Hunting with Brim | Malware C2 Detection

It is just another malware campaign spread with CobaltStrike. We know an employee clicks on a link, downloads a file, and then network speed issues and anomalous traffic activity arises. Now, open Brim, import the sample pcap and go through the walkthrough.

# Investigate the traffic sample to detect malicious C2 activities!

Let's look at the available logfiles first to see what kind of data artefact we could have. The image on the left shows that we have many alternative log files we could rely on. Let's review the frequently communicated hosts before starting to investigate individual logs.

![alt text](fcae25712f15175255e7d725ff18cccd.png)

Query:  `cut id.orig_h, id.resp_p, id.resp_h | sort  | uniq -c | sort -r count`

![alt text](b56c196610b0a270aaab8102ef3e15ae.png)

This query provides sufficient data that helped us decide where to focus. The IP addresses "10.22.xx" and "104.168.xx" draw attention in the first place. Let's look at the port numbers and available services before focusing on the suspicious IP address and narrowing our search.

Query: `_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

![alt text](c166d49a6f0226462941ea3d7fa483b7.png)

Nothing extremely odd in port numbers, but there is a massive DNS record available. Let's have a closer look.

Query:  `_path=="dns" | count() by query | sort -r`

![alt text](e8e99b9574ae2bb9b9bcd00bc3a2f4d6.png)

There are out of ordinary DNS queries. Let's enrich our findings by using VirusTotal to identify possible malicious domains.

![alt text](aa38d28211b3017f4b0f6c158ffa9ae3.png)

We have detected two additional malicious IP addresses (we have the IP 45.147.xx from the log files and gathered the 68.138.xx and 185.70.xx from VirusTotal) linked with suspicious DNS queries with the help of external research. Let's look at the HTTP requests before narrowing down our investigation with the found malicious IP addresses.

Query:  `_path=="http" | cut id.orig_h, id.resp_h, id.resp_p, method, host, uri | uniq -c | sort value.uri`

![alt text](cdc582d20a3c62c89cdfba7af569c5ea.png)

We detect a file download request from the IP address we assumed as malicious. Let's validate this idea with VirusTotal and validate our hypothesis. 

![alt text](a040972d62794ecb27d03ca973251961.png)

VirusTotal results show that the IP address "104.xx" is linked with a file. Once we investigate that file, we discover that these two findings are associated with CobaltStrike. Up to here, we've followed the abnormal activity and found the malicious IP addresses. Our findings represent the C2 communication. Now let's conclude our hunt by gathering the low hanging fruits with Suricata logs.

Query:  `event_type=="alert" | count() by alert.severity,alert.category | sort count`

![alt text](bf13990b1e9cb18531f0a3c0e574fbc2.png)

# Exercise: Threat Hunting with Brim | Crypto Mining

Cryptocurrencies are frequently on the agenda with their constantly rising value and legal aspect. The ability to obtain cryptocurrencies by mining other than purchasing is becoming one of the biggest problems in today's corporate environments. Attackers not only compromise the systems and ask for a ransom, but sometimes they also install mining tools (cryptojacking). Other than the attackers and threat actors, sometimes internal threats and misuse of trust and privileges end up installing coin miners in the corporate environment.

Usually, mining cases are slightly different from traditional compromising activities. Internal attacks don't typically contain major malware samples. However, this doesn't mean they aren't malicious as they are exploiting essential corporate resources like computing power, internet, and electricity. Also, crypto mining activities require third party applications and tool installations which could be vulnerable or create backdoors. Lastly, mining activities are causing network performance and stability problems. Due to these known facts, coin mining is becoming one of the common use cases of threat hunters.

### Let's investigate a traffic sample to detect a coin mining activity!

Let's look at the available logfiles first to see what kind of data artefact we could have. The image on the left shows that we don't have many alternative log files we could rely on. Let's review the frequently communicated hosts to see if there is an anomaly indicator. 

![alt text](6bf48a81a4904ac4c0896ba38cb058b0.png)

Query:  `cut id.orig_h, id.resp_p, id.resp_h | sort  | uniq -c | sort -r`

![alt text](d6fbc67b061e4c38522ba5df364b8dc8.png)

This query provided sufficient data that helped us decide where to focus. The IP address "192.168.xx" draws attention in the first place. Let's look at the port numbers and available services before focusing on the suspicious IP address and narrowing our search.

Query: `_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

![alt text](2b36a8f09b094b06da9ea95a354ff9e6.png)

There is multiple weird port usage, and this is not usual. Now, we are one step closer to the identification of the anomaly. Let's look at the transferred data bytes to support our findings and find more indicators.

Query: `_path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes`

![alt text](8d30202d4ab8b8b61b9c3c8f435761a5.png)

The query result proves massive traffic originating from the suspicious IP address. The detected IP address is suspicious. However, we don't have many supportive log files to correlate our findings and detect accompanying activities. At this point, we will hunt the low hanging fruits with the help of Suricata rules. Let's investigate the Suricata logs

Query: `event_type=="alert" | count() by alert.severity,alert.category | sort count`

![alt text](f1aa85bc7dfc14478afd0ffbbf832d20.png)

Suricata rules have helped us conclude our hunt quickly, as the alerts tell us we are investigating a "Crypto Currency Mining" activity. Let's dig deeper and discover which data pool is used for the mining activity. First, we will list the associated connection logs with the suspicious IP, and then we will run a VirusTotal search against the destination IP.

Query: `_path=="conn" | 192.168.1.100`

![alt text](79438eae146833967d3e6a3af7835a33.png)

![alt text](0103bf02af6332ba8d60e02a5107b926.png)

We investigated the first destination IP address and successfully identified the mining server. In real-life cases, you may need to investigate multiple IP addresses to find the event of interest.

Lastly, let's use Suricata logs to discover mapped out MITRE ATT&CK techniques.

Query: `event_type=="alert" | cut alert.category, alert.metadata.mitre_technique_name, alert.metadata.mitre_technique_id, alert.metadata.mitre_tactic_name | sort | uniq -c`

![alt text](cd0190902c6c195fc8e984d745998819.png)

Now we can identify the mapped out MITRE ATT&CK details as shown in the table below.

<table class="table table-bordered"><tbody><tr><td style="text-align:center"><span style="font-weight:bolder">Suricata Category</span><br></td><td style="text-align:center"><span style="font-weight:bolder"><span data-testid="glossary-term" class="glossary-term">MITRE</span> Technique Name</span><br></td><td style="text-align:center"><span style="font-weight:bolder"><span data-testid="glossary-term" class="glossary-term">MITRE</span> Technique Id</span><br></td><td style="text-align:center"><span style="font-weight:bolder"><span data-testid="glossary-term" class="glossary-term">MITRE</span> Tactic Name</span><br></td></tr><tr><td style="text-align:center">Crypto Currency Mining<br></td><td style="text-align:center">Resource_Hijacking<br></td><td style="text-align:center">T1496<br></td><td style="text-align:center">Impact<br></td></tr></tbody></table>

