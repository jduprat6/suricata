## Suricata an open-source intrusion detection system, intrusion prevention system, and network analysis tool. 

### Overview
In this project I explored Suricata, a tool used for monitoring network interfaces, where I focused on its alerting system and the process of creating rules. I learned to configure Suricata, specifying source and destination networks, and wrote custom rules to decide how packets should be handled, including whether they should generate alerts, be dropped, rejected, or allowed to pass through the interface. This involved determining which traffic should be processed based on the rules I created.

### Key Skills and Steps

#### Understanding Suricata Rules and Signatures:
- Learned the structure of Suricata rules, including actions (like alert, drop, pass, and reject), header (defining traffic attributes), and rule options (providing specific conditions).
  - **Alert**: Triggers an alert for traffic that matches the specified criteria.
  - **Drop**: Generates an alert but drops the traffic, used in IPS mode.
  - **Pass**: Allows traffic to pass through, can override other rules, including drop rules.
  - **Reject**: Blocks traffic and sends a TCP reset packet, stopping the communication.
- Analyzed an example rule below that alerts on specific HTTP traffic based on predefined conditions.

<div style="text-align:center;">
    <img src="https://i.imgur.com/TtM2Ond.png" alt="Description of Image">
</div>

- The $HOME_NET variable in Suricata, was defined in the /etc/suricata/suricata.yaml file. For the purposes of this lab, $HOME_NET was set to the 172.21.224.0/20 subnet. Additionally, I learned that using the term 'any' in the context of Suricata rules means that the system captures traffic from any port defined within the $HOME_NET network.



#### Rule Configuration and Testing:
- Created and modified custom rules in the `custom.rules` file.
- Applied these rules to network traffic data from a `sample.pcap` file and triggered alerts.

#### Log Analysis:
- Examined Suricata's log outputs, specifically `fast.log` and `eve.json`, to understand alert generation.
- Used `fast.log` for quick checks and `eve.json` for detailed analysis in JSON format.
- Utilized tools like `cat` and `jq` for reading and parsing log files.

#### Practical Application:
- Simulated the role of a security analyst monitoring network traffic.
- Ran Suricata with custom rules and packet capture files to generate and analyze alerts.
- Developed a deeper understanding of network flows and alert mechanisms in a cybersecurity context.

### Conclusion
This lab provided hands-on experience in using Suricata for intrusion detection, rule configuration, and log analysis. The skills developed are essential for network security monitoring and analysis, contributing significantly to the capabilities of a security analyst.
