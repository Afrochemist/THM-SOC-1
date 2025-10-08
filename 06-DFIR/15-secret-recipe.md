# Introduction

## Storyline

Jasmine owns a famous New York coffee shop Coffely which is famous city-wide for its unique taste. Only Jasmine keeps the original copy of the recipe, and she only keeps it on her work laptop. Last week, James from the IT department was consulted to fix Jasmine's laptop. But it is suspected he may have copied the secret recipes from Jasmine's machine and is keeping them on his machine. Image showing a Laptop with a magnifying glass

His machine has been confiscated and examined, but no traces could be found. The security department has pulled some important registry artifacts from his device and has tasked you to examine these artifacts and determine the presence of secret files on his machine.

## Room Machine

Before moving forward, let's deploy the machine by clicking on the Start Machine button on the top of the task. The machine will start in a split-screen view. In case the VM is not visible, use the blue Show Split View button at the top of the page. You may also access it via the AttackBox or RDP using the credentials below. It will take up to 3-5 minutes to start.

On the Desktop, there is a folder named Artifacts, which contains the registry Hives to examine and another folder named EZ tools, which includes all the required tools to analyze the artifacts.

Credentials

Username : Administrator

Password: thm_4n6

Note: If you are using Registry Explorer to parse the hives, expect some delay in loading as it takes time to parse the hives.

## Q & A

Q1 How many files are available in the Artifacts folder on the Desktop?

A1 6

![alt text](image-160.png)



# Windows Registry Forensics

## Registry Recap

Windows Registry is like a database that contains a lot of juicy information about the system, user, user activities, processes executed, the files accessed or deleted, etc. Image showing Registry icon

Following Registry Hives have been pulled from the suspect Host and placed in the `C:\Users\Administrator\Desktop\Artifacts` folder. All required tools are also placed on the path. `C:\Users\Administrator\Desktop\EZ Tools`.

Your challenge is to examine the registry hives using the tools provided, observe the user's activities and answer the questions.

Registry Hives

-    SYSTEM
-    SECURITY
-    SOFTWARE
-    SAM
-    NTUSER.DAT
-    UsrClass.dat

Note: The Download Task Files button has a cheat sheet, which can be used as a reference to answer the questions.

[Windows Forensics Cheatsheet](Windows%20Forensics%20Cheatsheet.pdf)

## Q & A

Q1 What is the computer name of the machine found in the registry?

A1 JAMES

![alt text](image-161.png)

![alt text](image-162.png)

Q2 When was the Administrator account created on this machine? (Format: yyyy-mm-dd hh:mm:ss)

A2 2021-03-17 14:58:48

![alt text](image-163.png)
![alt text](image-164.png)

Q3 What is the RID associated with the Administrator account?

A3 500

![alt text](image-165.png)

Q4 How many user accounts were observed on this machine?

A4 7

![alt text](image-166.png)

Q5 There seems to be a suspicious account created as a backdoor with RID 1013. What is the account name?

A5 bdoor

![alt text](image-167.png)

Q6 What is the VPN connection this host connected to?

A6 ProtonVPN

If we look up VPN we get several results with ProtonVPN but if we use the hint:  "Look for NetworkList in Software Hive" we can find the details, see image below.

Q7 When was the first VPN connection observed? (Format: YYYY-MM-DD HH:MM:SS)

A7 2022-10-12 19:52:36

![alt text](image-168.png)

Q8 There were three shared folders observed on his machine. What is the path of the third share?

A8 C:\RESTRICTED FILES

![alt text](image-169.png)

Q9 What is the last DHCP IP assigned to this host?

A9 172.31.2.197

![alt text](image-170.png)
![alt text](image-171.png)

Q10 The suspect seems to have accessed a file containing the secret coffee recipe. What is the name of the file?

A10 secret-recipe.pdf

![alt text](image-172.png)
![alt text](image-173.png)


Q11 The suspect executed multiple commands using the Run window. What command was used to enumerate the network interfaces?

A11 pnputil /enum-interfaces

![alt text](image-174.png)

Q12 The user searched for a network utility tool to transfer files using the file explorer. What is the name of that tool?

A12  netcat   

![alt text](image-175.png)
![alt text](image-176.png)


Q13 What is the recent text file opened by the suspect?

A13 secret-code.txt

![alt text](image-177.png)
![alt text](image-178.png)

Q14 How many times was PowerShell executed on this host?

A14 3

![alt text](image-180.png)
![alt text](image-179.png)

Q15 The suspect also executed a network monitoring tool. What is the name of the tool?

A15 wireshark

![alt text](image-182.png)

Q16 Registry Hives also note the amount of time a process is in focus. Examine the Hives and confirm for how many seconds was ProtonVPN executed?

A16 343

convert minutes to seconds
![alt text](image-181.png)

Q17 Everything.exe is a utility used to search for files in a Windows machine. What is the full path from which everything.exe was executed?

A17 C:\Users\Administrator\Downloads\tools\Everything\Everything.exe

![alt text](image-183.png)




















