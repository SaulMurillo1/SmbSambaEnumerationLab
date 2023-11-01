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


</p>
