# INTERNAL NETWORK PENETRATION TESTIING

Submitted by:  
Nketia-Dardom Ferdinand



# Table of Contents

- [SCOPE](#scope)
-  [EXECUTIVE SUMMARY](#executive-summary)  
- [ANALYSIS OF OVERALL SECURITY POSTURE](#analysis-of-overall-security-posture)   
- [KEY RECOMMENDATIONS](#key-recommendations)
- [TESTING METHODOLOGY](#testing-methodology)
- [DETAILED FINDINGS](#detailed-findings)
  - [*Weak login credentials of the MySQL server*](#weak-login-credentials-of-the-mysql-server)
  - [*Allowed access to unauthorized users by bypassing authentication on the VNC server* ](#allowed-access-to-unauthorized-users-by-bypassing-authentication-on-the-vnc-server)
  - [*Misconfigurations on server making it vulnerable to injection attacks*](#misconfigurations-on-server-making-it-vulnerable-to-injection-attacks)  
- [SUMMARY OF FINDING](#summary-of-finding)



## SCOPE  
The scope of engagement comprises of an internal network `10.10.10.0/24` and a domain name: [Virtual InfoSec Africa](https://virtualinfosecafrica.com)

## ANALYSIS OF OVERALL SECURITY POSTURE   
The internal network assessment reveals a troubling security posture, marked by critical vulnerabilities and systemic weaknesses. During the host and service discovery phase, several systems with exposed services were identified, some of which were running outdated software. This significantly increases the likelihood of exploitation, as outdated software is often vulnerable to known attacks. The vulnerability scan intensified these concerns, revealing numerous high-risk vulnerabilities, including unpatched software and misconfigurations that attackers could exploit to gain unauthorized access or disrupt operations.

The web-based surface attack assessment exposed further risks, such as default credentials and insecure web interfaces, creating potential entry points for attackers. Overall, the network has multiple security flaws that compromise its ability to withstand potential threats. Immediate corrective actions are crucial, including applying security patches, strengthening password policies, and improving configuration management. Resolving these issues is vital to fortifying the network’s defenses and preventing future security breaches.  
 
## EXECUTIVE SUMMARY  
A penetration test was conducted on the internal network of the above [SCOPE](#scope) with the aim to identify vulnerabilities and evaluate the network’s security posture. The assessment followed a thorough process, including host and service discovery, vulnerability scanning, and web-based attack surface analysis.

To start, Nmap was used for host and service discovery, to map the active systems and their running services. This scan revealed several critical systems with exposed services, some running outdated or insecure versions, signaling potential entry points for attackers.

Next, a vulnerability scan was performed using Metasploit, uncovering multiple critical and high-risk vulnerabilities. The scan highlighted unpatched software and configuration flaws that could be exploited by malicious actors to gain unauthorized access or disrupt the network.

Additionally, web attack surface analysis was conducted using Eyewitness. This assessment uncovered several security issues, such as default credentials and vulnerable web interfaces, which could be targeted for further system compromise.

The test findings reveal significant security concerns, including critical vulnerabilities from outdated software, insecure configurations, and weak or default passwords. Immediate remediation actions, such as patching vulnerabilities, enforcing stronger password policies, and regularly updating configurations, are recommended to improve the network's security and reduce risk exposure.  

## KEY RECOMMENDATIONS  
* Establish a robust patch management system to maintain up-to-date security across all systems.  

* Improve authentication methods by enforcing strong password policies and implementing multi-factor authentication (MFA).  

* Focus on configuration hardening to secure system settings and minimize attack vectors.  

* Incorporate regular vulnerability scanning as part of a continuous monitoring strategy.  

* Provide ongoing security awareness training for employees to enhance organizational security practices.  

* Strengthen web application defenses by deploying web application firewalls (WAFs) and conducting routine security assessments.  

* Develop and regularly test a comprehensive incident response plan to ensure preparedness for potential security breaches.

## TESTING METHODOLOGY  

A Host discovery is conducted using the nmap tool to:  
* a. find out all the addresses in the above [Scope](#scope)      
[Scanning](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Nmap%20block%20address%20scan.png) is produced, create a file, filter the results using the grep command, cut using the awk command and save that in it. [saving scan list](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/saving%20scan%20results.png)  
* b. find out hosts online in this network by passing to the nmap, the list of the addresses file,  
[Hosts online scan a](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/hosts%20online%20scan%20a.png)  
filter the results using the grep command, cut using the awk command and then saving it in another file. [Hosts online scan](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/hosts%20online%20scan.png)  

Utilizing the nmap tool, a service discovery and port scan is done to scan ports to find out the services they are running.  
[Nmap ports scanning](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Nmap%20port%20scanning.png)  
Text files are created for each of the service protocol from the output of the scan 
[Protocol Separation](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Protocol%20separation.png)    
For each service protocol, ip addresses it run on are saved in its assigned text file created using the vim command.  
[Inserting using vim](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Inserting%20ip%20addresses.png)  

## DETAILED FINDINGS  

## *Weak login credentials of the MySQL server*  
                  MySQL 5.6.49 Analysis   
|CURRENT RATING      |  CVSS                      |  
|--------------------|----------------------------|  
|           High     |             8.0            |  

* **FINDING SUMMARY**   
Successful entry into the MySQL server was accomplished by bruteforcing. Utilizing the metasploit auxiliary scanner module for MySQL, a scan was conducted on the ip addresses with mysql services running on, to discover probable vulnerabilities by bruteforcing with a local pass wordlist.  
Selecting a metasploit auxiliary exploit module with payload, an exploitation into these discovered vulnerabilities was done to gain access into the server.  

* **EVIDENCE**  
[Search for MySQL module](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Search%20for%20mysql%20module.jpg)   
  
[Scan for vulnerabilities on MySQL server](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Scan%20for%20vulnerabilities_mysql.jpg)  
  
  **Affected resources:**  
* `10.10.10.5`     
* `10.10.10.40`  

**RECOMMENDATION**  
* Upgrade MySQL  

It is recommended to upgrade to the latest stable version of MySQL that addresses the identified vulnerabilities. If you are currently using MySQL 5.6, consider upgrading to a more recent, supported version such as MySQL 5.7.x or 8.0.x, where feasible. These newer versions offer enhanced security features, improved performance, and patched vulnerabilities, ensuring a more secure and stable database environment.

## *Allowed access to unauthorized users by bypassing authentication on the VNC server*   
                REALVNC 5.3.2 (vnc)   
| Current rating       |    CVSS        |  
|----------------------|----------------|  
|  Critical            |  9.8           |  
  
  **FINDING SUMMARY:**  
Using the metasploit auxiliary scanner module, a scan was conducted into the VNC server for vulnerabilities on the ip addresses vnc service runs on.  
  
**EVIDENCE**  
[Search vnc module](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/search%20for%20vnc%20module.png)  
[Scanning VNC module](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/scanning%20vnc.png)  

**Affected resources:**  
* `10.10.10.10`  
* `10.10.10.50`  

**RECOMMENDATION**  

* Review Authentication Settings    

Regularly audit and update your authentication settings to ensure they adhere to best security practices. This helps prevent unauthorized access by enforcing strong authentication mechanisms. Implement measures such as multi-factor authentication (MFA), strong password policies, and frequent credential reviews to mitigate risks and enhance overall system security.  

## *Misconfigurations on server making it vulnerable to injection attacks*  
                  APACHE HTTP SERVER 2.24.49   
|  Current Rating  | CVSS                  |  
|------------------|-----------------------|  
|   High           |    7.5                |  
 
Using the eyewitness, I was able to get screenshots of websites running on these services. Using a metasploit auxiliary http scanner module for apache, a scan was conducted into the apache server to discover probable vulnerabilities.  

For host `10.10.10.55` that runs an Apache Tomcat web server(Java based), a TCP bind shell payload was generated using the msfvenom tool, afterwards injected into the web server through a vulnerability.  
For host `10.10.10.30` that runs a python server, a base64 encoded payload was generated using the msfvenom tool, to be uploaded unto the web server.  

**EVIDENCE**  
[Eyewitness](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/eyewitness.png)  
[Scanning apache http server](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/apache%20http%20scanning.png)  
[Generating java payload](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Generating%20java%20payload.jpg)  
[Generating python payload](https://github.com/ULTRAE100/Internal-Network-Penetration-Testing/blob/main/Generating%20python%20payload.jpg)  

**Affected resources:**  
`10.10.10.2`, `10.10.10.30`, `10.10.10.55`  

**RECOMMENDATION**  
Review Configurations:  
 Regularly check and audit directory configurations and access controls.  

## SUMMARY OF FINDING
| FINDING                   | SEVERITY                |  
|---------------------------|-------------------------|  
|  Weak login credentials of the MySQL server| High   |  
|    Allowed access to unauthorized users by bypassing authentication on the VNC server                      |  Critical                       |  
| Misconfigurations on server making it vulnerable to injection attacks| High                               |   
 
CVSS v3.0 Reference Table  
 
|Qualitative Rating|CVSS Score|  
|------------------|----------|  
| None/Informational|N/A      |    
|Low               |0.1 – 3.9 |  
|Medium            |4.0 – 6.9 |  
|High              |7.0 – 8.9 |  
|Critical          |9.0 – 10.0|  

## Table 1 : Common Vulnerability Scoring System Version 3.0  
