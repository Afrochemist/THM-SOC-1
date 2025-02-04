# Scenario 1 | Brute-Force

Use the attached VM to finish this task.

[+] THE NARRATOR


J&Y Enterprise is one of the top coffee retails in the world. They are known as tech-coffee shops and serve millions of coffee lover tech geeks and IT specialists every day. 


They are famous for specific coffee recipes for the IT community and unique names for these products. Their top five recipe names are;

WannaWhite, ZeroSleep, MacDown, BerryKeep and CryptoY.


J&Y's latest recipe, "Shot4J", attracted great attention at the global coffee festival. J&Y officials promised that the product will hit the stores in the coming months. 


The super-secret of this recipe is hidden in a digital safe. Attackers are after this recipe, and J&Y enterprises are having difficulties protecting their digital assets.


Last week, they received multiple attacks and decided to work with you to help them improve their security level and protect their recipe secrets.  


This is your assistant J.A.V.A. (Just Another Virtual Assistant). She is an AI-driven virtual assistant and will help you notice possible anomalies. Hey, wait, something is happening...


[+] J.A.V.A.

Welcome, sir. I am sorry for the interruption. It is an emergency. Somebody is knocking on the door!

[+] YOU

Knocking on the door? What do you mean by "knocking on the door"?

[+] J.A.V.A.

We have a brute-force attack, sir.

[+] THE NARRATOR

This is not a comic book! Would you mind going and checking what's going on! Please... 

[+] J.A.V.A.

Sir, you need to observe the traffic with Snort and identify the anomaly first. Then you can create a rule to stop the brute-force attack. GOOD LUCK!

First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

    Create the rule and test it with "-A console" mode. 
    
    Use "-A full" mode and the default log path to stop the attack.
    
    Write the correct rule and run the Snort in IPS "-A full" mode.
    
    Block the traffic at least for a minute and then the flag file will appear on your desktop.

### Stop the attack and get the flag (which will appear on your Desktop)

Hint - "IPS mode and Dropping Packets" is covered in the main Snort room TASK-7. https://tryhackme.com/room/snort

THM{81b7fef657f8aaa6e4e200d616738254}

I created some rules to test the traffic, and you can see various attempts on port 22 from the same IP address to different IP addresses which is consistent with brute-force attack pattern. The I created a rule to drop traffic from that IP to any IP:22

`rules.conf`
```
#alert tcp any any <> any any (msg:"test";sid:1000001;rev:1)
#alert tcp any any <> any 80 (msg:"Alert on port 80";sid:1000001;rev:1)
#alert tcp any any <> any 22 (msg:"Alert posible ssh attempt";sid:1000002;rev:1)

drop tcp 10.10.245.36 any <> any 22 (msg:"brute-force ssh attempt";sid:1000002;rev:1)
```
alternatively you can run `sudo snort -v -l .` inspect the traffic and create the rule to drop the traffice on port 22

then we run snort in IPS mode to effectively use the rule:
```
ubuntu@ip-10-10-55-235:~/Desktop$ sudo snort -c rules.conf -q -Q --daq afpacket -i eth0:eth1 -A full
```
### What is the name of the service under attack?

SSH

Which uses port 22 by default

### What is the used protocol/port in the attack?

tcp/22




# Scenario 2 | Reverse-Shell

Use the attached VM to finish this task.


[+] THE NARRATOR

Good Job! Glad to have you in the team!


[+] J.A.V.A.

Congratulations sir. It is inspiring watching you work.


[+] You

Thanks team. J.A.V.A. can you do a quick scan for me? We haven't investigated the outbound traffic yet. 


[+] J.A.V.A.

Yes, sir. Outbound traffic investigation has begun. 


[+] THE NARRATOR

The outbound traffic? Why?


[+] YOU

We have stopped some inbound access attempts, so we didn't let the bad guys get in. How about the bad guys who are already inside? Also, no need to mention the insider risks, huh? The dwell time is still around 1-3 months, and I am quite new here, so it is worth checking the outgoing traffic as well.


[+] J.A.V.A.

Sir, persistent outbound traffic is detected. Possibly a reverse shell...


[+] YOU

You got it!


[+] J.A.V.A.

Sir, you need to observe the traffic with Snort and identify the anomaly first. Then you can create a rule to stop the reverse shell. GOOD LUCK!
Answer the questions below
First of all, start Snort in sniffer mode and try to figure out the attack source, service and port.

Then, write an IPS rule and run Snort in IPS mode to stop the brute-force attack. Once you stop the attack properly, you will have the flag on the desktop!

Here are a few points to remember:

    Create the rule and test it with "-A console" mode. 
    
    Use "-A full" mode and the default log path to stop the attack.
    
    Write the correct rule and run the Snort in IPS "-A full" mode.
    
    Block the traffic at least for a minute and then the flag file will appear on your desktop.

### Stop the attack and get the flag (which will appear on your Desktop)

Hint - You can easily drop all the traffic coming to a specific port as a rapid response.

THM{0ead8c494861079b1b74ec2380d2cd24}

`rules.conf`
```
drop tcp any any <> any 4444 (msg: "drop traffic on port 4444";sid:1000001;rev:1)
```
```
ubuntu@ip-10-10-55-235:~/Desktop$ sudo snort -c rules.conf -q -Q --daq afpacket -i eth0:eth1 -A full
```
### What is the used protocol/port in the attack?

tcp/4444

### Which tool is highly associated with this specific port number?

Metasploit


