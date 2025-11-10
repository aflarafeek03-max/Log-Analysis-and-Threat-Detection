# Log-Analysis-and-Threat-Detection
BFOR 519 Project - Log Analysis and Threat Detection using Kibana and Kaggle Data

#Group Members
- Afla Rafeek
- Saanvi Shah
- Elijah A. Acero

#Group Members and Roles
- Saanvi Shah: Detection rules, documentation on rule logic  
- Afla Rafeek: Data upload, visualization, dashboard creation  
- Elijah A. Acero: Grafana setup, system monitoring, dashboard comparison

#Visualization & Analysis (Kibana)

1. Action Distribution(Blocked vs Allowed)

Description:
This chart compares the number of network actions that were allowed versus blocked. It provides a quick overview of how the security system handled incoming and outgoing connections.

Data Fields Used:
- action
- timestamp

Insight:
The chart shows an almost equal number of blocked and allowed actions. This indicates that the network security policies are balanced, filtering traffic effectively while still allowing legitimate connections.

![alt text](<Action Distribution.png>)

2. Top Protocols in Network Logs

Description:
This visualization highlights the top communication protocols (such as TCP, HTTP, and UDP) recorded in the network logs. It helps understand which protocols are most frequently used in the captured traffic.

Data Fields Used:
- protocol
- timestamp

Insight:
TCP and HTTP dominate the traffic, indicating that most of the network activity involves web and application-related communication. Monitoring these protocols closely can help detect unusual data transfer behaviors.

![alt text](<Top Protocols in Netwrok Logs.png>)

3. Top 10 Source IPs Generating Traffic

Description:
This chart lists the IP addresses responsible for the most log entries. It helps in identifying devices or external hosts that are generating large amounts of traffic.

Data Fields Used:
- source_ip
- bytes_transferred

Insight:
One or more IP addresses generate a disproportionately high number of requests which could indicate either an aggregated dataset entry or potential scanning or brute-force activity.

![alt text](<Top 10 Source IPs generating Traffics.png>)

4. Threat Type Distribution

Description:
This visualization categorizes logs based on their threat labels — benign, suspicious, or malicious. It shows how much of the dataset represents safe vs potentially harmful activity.

Data Fields Used:
- threat_label
- timestamp

Insight:
Most logs are labeled as benign, indicating normal network operations. However, the presence of suspicious and malicious entries highlights ongoing risks that need further analysis or mitigation strategies.

![alt text](<Threat Type Distribution.png>)

5. Dashboard Summary

Description:
All visualizations were combined into a single Kibana dashboard for centralized monitoring.
This provides a real-time overview of network behavior, traffic patterns, and detected threats.

Key Observations:
- Balanced action distribution between blocked and allowed connections.
- Heavy use of web-based protocols (HTTP, HTTPS, TCP).
- A few source IPs dominate the network activity.
- Majority of data is benign, but suspicious and malicious traffic exists.