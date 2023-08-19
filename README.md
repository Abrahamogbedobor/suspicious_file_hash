# suspicious_file_hash
<h1>Project Description</h1>
I received an alert based on a supecious file that was downloaded by an employee in my organisation. At the initial stage of my investigation, i discovered the employee received an email that contain an attcached file, which happened to be a password proteced spreadsheet file. The emplooyee used the provided password to gain access to the file after downloading it, as soon as the file was opened, a malicious payload was successful executed on the employee system. I quickly retrieved the malicious file, and create a hash value of the file (SHA256) to uniquely identify it, then i proceeded with my investigation using VirusTotal to further discover and uncover any IOCs that is associated with it. <br />

<h2>Environments and Technologies Used</h2>

- Pyramid of Pain
- Linux Command-Line

<h2>Operating Systems Used</h2>

- Linux Operating System (Bash Shell)

<h2>High-Level Steps</h2>

- Retrieving Hash Value of the File (287d612e29b71c90aa54947313810a25)
- Reviewing Alert Details such as Timeline
- Entering File Hash into VirusTotal for Evaluation
- Analyzing VirusTotal Report (Tabs: Detection, Details, Relations, Behaviour)
- Determine if the File is Malicious by Observing; (High Vendor's Ratio, Negative Community Score, and Detection-tab)
- Uncovering Additional IoCs that are associated with the File Based on VirusTotal Report

<h2>Task Overview</h2>

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
The file hash has been reported as malicious by over 50 vendors. Upon further investigation, this file hash is known as the malware Flagpro, which has been commonly used by the advanced threat actor BlackTech.
  <h2>Filter and Analyze Captured Packets</h2>
For me to  generate some HTTP [port 80] traffic that i needed to capture later, i then used the "curl command" with the website i need to generate traffic from as shown; [curl opensource.google.com]. Moving forward, the [ls -1 capture.pcap] command was used to verify that the packet was captured successfully. Furthermore, i will explain the options used in capturing and saving the packet data above; the [-1 eth0;] helped to capture data from eth0 interface. [-nn] option warns Linux terminal not to convert IP to domain name for security reasons, so as not to alert malicious actors that they are being investigated. [-c9] captured 9 packets of data, [port 80] that was specified helped to only capture port 80 traffic which is the default port of HTTP. [-w capture.pcap] saved the capture packet data to the named file ‘capture.pcap’. Finally, the [&] at the end was the reason the command was run in the background, though some output text appears on the terminal.
  <h2>Saved the Captured Data for Detail Analysis</h2>
Finally, the saved packet data file needed to be retrieved, and filtered for further investigation, by using this command; sudo tcpdump [-nn -r capture.pcap -v] this filtered command will run the tcpdump command using the above options as explained; [-nn] disabled port and protocol name lookup, [-r] read the capture from the saved file, [-v] displayed a detail packet data.
  <h2>Tcpdump Packets Outputs Interpretation</h2>
  <img src="https://i.imgur.com/hThJoCT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
In the first line of the output after running the above commands, tcpdump reported that it was listening on the eth0 interface, and it also provided information about the link-type and capture size in bytes. On the second line of the output, the first field was the packet  timestamp followed by the protocol type IP. Because -v was used in the command which is the verbose option it further gives more details about the IP packet fields that were captured. In addition, the output data also show the systems that are communicating with each other in the network, using > to indicate the direction of traffic flow in their communication i.e from source IP which tcpdump normally does convert to domain names to destination IP. The remaining data is for the TCP packet where we have the flags field, which identifies TCP flags. From the output, the P indicates the PUSH FLAGS, why the dot indicates it is an ACK FLAG. Meaning, the packet is pushing out data. Lastly, there is the TCP checksum value, used in detecting errors in the data and next to it is the sequence and acknowledgement numbers, window size, and length of the inner TCP packet in bytes.

</p>
<br />
