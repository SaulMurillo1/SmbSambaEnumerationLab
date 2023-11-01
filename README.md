<h1>SMB Samba Enumeration</h1>


<h2>Description</h2>
This project consists of using the Nmap, msfconsole, nmblookup, smbclient & rpcclient Linux tools to enumerate SMB Samba information. 
<br />
<br />
- Samba is a suite of applications that implements the Server Message Block (SMB) protocol. Many operating systems, including Microsoft Windows, use the SMB protocol for client-server networking. Samba enables Linux / Unix machines to communicate with Windows machines in a network.
<br />
<br />

Disclaimer: The Kali Linux user machine and target machine used in this project was provided to me by INE for educational purposes. The misuse of the information in this project lab can result in criminal charges brought against the individual/individuals in question.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Nmap</b>
- <b>MSFconsole</b>
- <b>nmblookup</b>
- <b>smbclient</b>
- <b>rpcclient</b>


<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="left">
Ping target machine to verify that it is active: <br/>
<br/>
- INE has provided me with Kali Linux GUI & target machine (target machine is one ip address above from mine).  I will run and ip a command to verify my own ip address. 
<br/>
<br/>
Commands: ip a
<br/>
ping 192.38.82.3
<br/>
<br/>
<img src="https://i.imgur.com/9RWD15O.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap scan on target machine to try to find open ports: <br/>
<br/>
- We can see that port 445 (SMB) and 139 are open.
<br/>
<br/>
Command: nmap 192.38.82.3
<br/>
<br/>
<img src="https://i.imgur.com/NrI3Get.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap scan that will enumerate further details for ports 445 & 139: <br/>
<br/>
- We can now see the version that port 139 & 445 are running.  It looks like some version of Samba 3.x - 4.x is running for these open ports.
<br/>
<br/>
Command: nmap 192.38.82.3 -p 445,139 -sV
<br/>
<br/>
<img src="https://i.imgur.com/2capKNz.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap scan that will enumerate open UDP ports: <br/>
<br/>
- The past Nmap scans were for tcp ports. I will now run an Nmap scan that will look for open UDP ports. This can be done by adding -sU to the command so that Nmap will specifically target open UDP ports.
<br/>
- UDP port scans usually take a long time, so I'll add --top-ports 25 in order to scan the top 25 ports so that the scan can be a bit faster for the purpose of the lab. --open means that the Nmap command will only enumerate open ports and not closed ports.
<br/>
- We can see that UDP port 137 is open, and it's version is Samba nmbd.
<br/>
<br/>
Command: nmap 192.38.82.3 -sU --top-port 25 --open -sV
<br/>
<br/>
<img src="https://i.imgur.com/aqGUO8Q.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run msfconsole (Metasploit Framework Console) to use as enumeration tool: <br/>
<br/>
- We will use the Metasploit Framework Console tool to enumerate the actual Samba version.
<br/>
<br/>
Command: msfconsole
<br/>
<br/>
<img src="https://i.imgur.com/x9ihQ8l.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run msfconsole (Metasploit Framework Console) to enumerate SMB version of the target machine: <br/>
<br/>
- While using the msfconsole tool, you can use the show options command as a way to get help with which commands can be used.
<br/>
- We can see the RHOSTS change to the target machine in the screenshot down below. Once I set the target host, I was able to use the command exploit to begin enumeration.
<br/>
- It looks like the SMB version of the target machine is Samba 4.3.11-Ubuntu.
<br/>
<br/>
Commands:  use auxiliary/scanner/smb/smb_version
<br/>
set rhosts 192.38.82.3
<br/>
exploit
<br/>
<br/>
<img src="https://i.imgur.com/Ei1Nyt2.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run nmblookup to find the NetBIOS computer name of Samba server: <br/>
<br/>
- nmblookup is used to query NetBIOS names and map them to IP addresses in a network using NetBIOS over TCP/IP queries.
<br/>
- The nmblookup command can display the hostname, workgroup and MAC address of the given IP address.
<br/>
- We can see that the computer name of the Samba server is SAMBA-RECON. The number 20 next the the NetBIOS name means that there is a Samba server that can be connected to.
<br/>
<br/>
Command:  nmblookup -A 192.38.82.3
<br/>
<br/>
<img src="https://i.imgur.com/IZHAhQW.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Utilize the smbclient tool to verify if it is possible to connect to the Samba server: <br/>
<br/>
- The command below will check if a null session (-N) is possible on the Samba server. 
<br/>
- We can see that the command indeed enumerated a list of sharenames with IPC$ being one of them. This means that the Samba server does in fact allow null sessions.
<br/>
<br/>
Command:  smbclient -L 192.38.82.3 -N
<br/>
<br/>
<img src="https://i.imgur.com/8eNrCbT.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />


</p>
