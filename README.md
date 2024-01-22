## Suricata Network Analysis Tool

### Overview
In this project I explored Suricata, an open-source IDS, IPS, and network analysis tool used for monitoring networks. In this project, I focused on its alerting system and the process of creating rules. I learned to configure Suricata, specifying source and destination networks, and explored custom rules to decide how packets should be handled, including whether they should generate alerts, be dropped, rejected, or allowed to pass through the interface. 

### Key Skills and Steps

#### Understanding Suricata Rules and Signatures:
- Learned the structure of Suricata rules, including actions (like alert, drop, pass, and reject), header (defining traffic attributes), and rule options (providing specific conditions).
  - **Alert**: Triggers an alert for traffic that matches the specified criteria.
  - **Drop**: Generates an alert but drops the traffic, used in IPS mode.
  - **Pass**: Allows traffic to pass through, can override other rules, including drop rules.
  - **Reject**: Blocks traffic and sends a TCP reset packet, stopping the communication.
- Analyzed an example rule below that alerts on specific HTTP traffic based on predefined conditions.

<div style="text-align:center;">
    <img src="https://i.imgur.com/TtM2Ond.png" alt="suricata1">
</div>

- The $HOME_NET variable in Suricata, was defined in the /etc/suricata/suricata.yaml file. For the purposes of this lab, $HOME_NET was set to the 172.21.224.0/20 subnet. Additionally, I learned that using the term 'any' in the context of Suricata rules means that the system captures traffic from any port defined within the $HOME_NET network.
- The msg: option provides the alert text. In this porject, the alert will print out the text “GET on wire”, which specifies why the alert was triggered.
- The flow:established,to_server option determines that packets from the client to the server should be matched. (In this instance, a server is defined as the device responding to the initial SYN packet with a SYN-ACK packet.)
- The content:"GET" option tells Suricata to look for the word GET in the content of the http.method portion of the packet.
- The sid:12345 (signature ID) option is a unique numerical value that identifies the rule.
- The rev:3 option indicates the signature's revision which is used to identify the signature's version. Here, the revision version is 3.

#### Rule Configuration and Testing:
- I created and modified custom rules in the `custom.rules` file.
- I applied these rules to network traffic data from a `sample.pcap` file and triggered alerts.
  
<div style="text-align:center;">
  <img src="https://i.imgur.com/t4EsBl1.png" alt="suricata2">
</div>

- I ran the command "sudo suricata -r sample.pcap -S custom.rules -k none" to start the Suricata application and process the sample.pcap file using the rules defined in the custom.rules file. This command provided output on the number of packets (200) processed by Suricata. 

  - The command's options were:

    - -r sample.pcap: This specified sample.pcap as the input file to simulate network traffic.
    - -S custom.rules: This instructed Suricata to use the rules I had defined in the custom.rules file.
    - -k none: This option disabled all checksum checks. Since I was working with a sample packet capture file, there was no need for Suricata to verify the integrity of the checksums.
  - Suricata then logged an alert in the /var/log/suricata/fast.log file whenever the conditions in any of the rules were met.

#### Log Analysis:
- Examined Suricata's log outputs, specifically `fast.log` and `eve.json`, to understand alert generation.
- Used `fast.log` for quick checks and `eve.json` for detailed analysis in JSON format.
- Utilized tools like `cat` and `jq` for reading and parsing log files.

<div style="text-align:center;">
  <img src="https://i.imgur.com/2vGjyVq.png" alt="suricata3">
</div>

- The jq command above extracts the fields specified in the list in the square brackets from the JSON data. The fields selected are the timestamp (.timestamp), the flow id (.flow_id), the alert signature or msg (.alert.signature), the protocol (.proto), and the destination IP address (.dest_ip).

#### Practical Application:
- Simulated the role of a security analyst monitoring network traffic.
- Ran Suricata with custom rules and packet capture files to generate and analyze alerts.
- Developed a deeper understanding of network flows and alert mechanisms in a cybersecurity context.

### Conclusion
This lab provided hands-on experience in using Suricata for intrusion detection, rule configuration, and log analysis. The skills developed are essential for network security monitoring and analysis, contributing significantly to the capabilities of a security analyst.
