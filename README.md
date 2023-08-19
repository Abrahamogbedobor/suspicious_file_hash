# suspicious_file_hash
<h1>Project Description</h1>
For this task,c.<br />

<h2>Environments and Technologies Used</h2>

- (Virtual Machines/Computer)
- Linux Command-Line
- Remote Desktop
- Tcpdump

<h2>Operating Systems Used</h2>

- Linux Operating System (Bash Shell)

<h2>High-Level Steps</h2>

- Identified Network Interfaces
- Inspect Network Interface Traffic with Tcpdump
- Capture Network Traffic with Tcpdump
- Filtered Captured Packet Data

<h2>Task Overview</h2>

<p>
<img src="https://i.imgur.com/YFgUA1T.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/mY9vRkm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dktmosu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
<img src="https://i.imgur.com/UStCEIp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <h2>Identifying/Inspect/Capture Network Interfaces</h2>
First, I identified the network interfaces that could be used or that are running for packet data capturing in my organization systems. In doing that, I used the [sudo command + tcpdump -D], to gain privilege to access the available interfaces i.e [sudo tcpdump -D]. This then outputs all the available interfaces on my directory. Note, the [sudo ifconfig] command could also be use to display available interfaces. Furthermore, i then used tcpdump to filter, and inspect network traffic in my selected network interface which was eth0 (Ethernet network interface). In doing that, I used the [sudo tcpdump -i eth0 -v -c5] commands with some options. Notably, [-i eth0] option was used to capture data only from the ethernet interface, and [-v] gives more information about the captured data i.e verbose, and [-c5] captured 5 packets of data.
 After my inspection, I was able to captured some network traffics such as (HTTP web TCP port 80) on my selected interface eth0, then i saved the captured data as a P-cap file extension [.pcap], using this command; [sudo tcpdump -1 eth0 -non -c9 port 80 -w capture.pcap &]. This command only run at the background using the above options that was specified, not on the terminal as expected.
  <h2>Filter and Analyze Captured Packets</h2>
For me to  generate some HTTP [port 80] traffic that i needed to capture later, i then used the "curl command" with the website i need to generate traffic from as shown; [curl opensource.google.com]. Moving forward, the [ls -1 capture.pcap] command was used to verify that the packet was captured successfully. Furthermore, i will explain the options used in capturing and saving the packet data above; the [-1 eth0;] helped to capture data from eth0 interface. [-nn] option warns Linux terminal not to convert IP to domain name for security reasons, so as not to alert malicious actors that they are being investigated. [-c9] captured 9 packets of data, [port 80] that was specified helped to only capture port 80 traffic which is the default port of HTTP. [-w capture.pcap] saved the capture packet data to the named file ‘capture.pcap’. Finally, the [&] at the end was the reason the command was run in the background, though some output text appears on the terminal.
  <h2>Saved the Captured Data for Detail Analysis</h2>
Finally, the saved packet data file needed to be retrieved, and filtered for further investigation, by using this command; sudo tcpdump [-nn -r capture.pcap -v] this filtered command will run the tcpdump command using the above options as explained; [-nn] disabled port and protocol name lookup, [-r] read the capture from the saved file, [-v] displayed a detail packet data.
  <h2>Tcpdump Packets Outputs Interpretation</h2>
  <img src="https://i.imgur.com/hThJoCT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
In the first line of the output after running the above commands, tcpdump reported that it was listening on the eth0 interface, and it also provided information about the link-type and capture size in bytes. On the second line of the output, the first field was the packet  timestamp followed by the protocol type IP. Because -v was used in the command which is the verbose option it further gives more details about the IP packet fields that were captured. In addition, the output data also show the systems that are communicating with each other in the network, using > to indicate the direction of traffic flow in their communication i.e from source IP which tcpdump normally does convert to domain names to destination IP. The remaining data is for the TCP packet where we have the flags field, which identifies TCP flags. From the output, the P indicates the PUSH FLAGS, why the dot indicates it is an ACK FLAG. Meaning, the packet is pushing out data. Lastly, there is the TCP checksum value, used in detecting errors in the data and next to it is the sequence and acknowledgement numbers, window size, and length of the inner TCP packet in bytes.

</p>
<br />
