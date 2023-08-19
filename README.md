# suspicious_file_hash
<h1>Project Description</h1>
I received an alert based on a supecious file that was downloaded by an employee in my organisation. At the initial stage of my investigation, i discovered the employee received an email that contain an attcached file, which happened to be a password proteced spreadsheet file. The emplooyee used the provided password to gain access to the file after downloading it, as soon as the file was opened, a malicious payload was successful executed on the employee system. I quickly retrieved the malicious file, and create a hash value of the file (SHA256) to uniquely identify it, then i proceeded with my investigation using VirusTotal to further discover and uncover any IOCs that is associated with it. <br />

<h2>Environments and Technologies Used</h2>

- Pyramid of Pain
- Linux Command-Line

<h2>Operating Systems Used</h2>

- Linux Operating System (Bash Shell)

<h2>High-Level Steps</h2>

- Retrieving Hash Value of the File (54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b)
- Reviewing Alert Details such as Timeline
- Entering File Hash into VirusTotal for Evaluation
- Analyzing VirusTotal Report (Tabs: Detection, Details, Relations, Behaviour)
- Determine if the File is Malicious by Observing; (High Vendor's Ratio, Negative Community Score, and Detection-tab)
- Uncovering Additional IoCs that are associated with the File Based on VirusTotal Report

<h2>Task Overview</h2>

<p>
<img src="https://i.imgur.com/olCw4s4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GqYmV5W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/2M3NvzM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The file hash has been reported as malicious by over 50 vendors. Upon further investigation, this file hash is known as the malware Flagpro, which has been commonly used by the advanced threat actor BlackTech.
  
Domain names: org.misecure.com is reported as a malicious contacted domain under the Relations tab in the VirusTotal report.
  
IP address: 207.148.109.242 is listed as one of many IP addresses under the Relations tab in the VirusTotal report. This IP address is also associated with the org.misecure.com domain as listed in the DNS Resolutions section under the Behavior tab from the Zenbox sandbox report.

Hash value: 54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b is a MD5 hash listed under the Details tab in the VirusTotal report.

Network/host artifacts: Network-related artifacts that have been observed in this malware are HTTP requests made to the org.misecure.com domain. This is listed in the Network Communications section under the Behavior tab from the Venus Eye Sandbox and Rising MOVES sandbox reports. 

Tools: Input capture is listed in the Collection section under the Behavior tab from the Zenbox sandbox report. Malicious actors use input capture to steal user input such as passwords, credit card numbers, and other sensitive information.

TTPs: Command and control is listed as a tactic under the Behavior tab from the Zenbox sandbox report. Malicious actors use command and control to establish communication channels between an infected system and their own system.
  
<br />
