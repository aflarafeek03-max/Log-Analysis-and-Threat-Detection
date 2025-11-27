# Log Analysis and Threat Detection
# BFOR 519 – Log Analysis and Threat Detection Project Topic
# Team Members: Afla Rafeek | Saanvi Shah | Elijah A. Acero

# Group Members & Roles
Saanvi Shah:	Data processing, cleaning & formatting; development of detection rules; documentation & result interpretation
Afla Rafeek:	Environment setup (Windows), dataset upload, log ingestion, Kibana visualization & dashboard creation
Elijah A. Acero:	Grafana setup, dashboard comparison, data analysis support, testing & validation

# 1. Project Summary
- The focus of this project is on the analysis of cybersecurity log data to identify suspicious and/or malicious activities via interactive dashboards. 
- The logs were gathered into Elasticsearch and were rendered into visualizations using Kibana and Grafana to show trends in traffic flow, abnormal traffic originating from a given IP address, what traffic was allowed, what traffic was blocked, and to what sensitive endpoints requests to access those endpoints were being made.
- The goal is to show how raw Source Log data from an organization's Security Operations Center(SOC) can be transformed into useful awareness of potential threats to that organization and allow for timely, effective responses to such threats, representing typical environments for today's modern Security Operations Centers (SOC).

# 2. Project Relevance
- In cybersecurity, log analysis is critical to threat hunting, SOC monitoring, and digital forensics.
- Most cyber attacks and intrusions start with slight behavior changes detected in the logs of all systems.
- Using visual analysis of logs, we can identify reconnaissance, brute force attacks, unauthorized scanning, and abuse of sensitive application areas far sooner than would be possible with standard techniques.

# Why We Selected This Topic
- Having hands-on experience with modern monitoring solutions, like Elasticsearch, Kibana, and Grafana, would help us widen our knowledge of currently used solutions in the industry for operational monitoring and security analytics.

# Skills & Knowledge Acquired
- Log preprocessing, normalization, and ingestion
- Dashboard creation, visualization techniques, and interpreting cyber threat patterns and traffic anomalies
- Collaborative systems analysis/documentation
- Understanding the workflows and detection logic of SOCs

# Who Can Benefit From This
- SOC analysts and cybersecurity engineers
- Digital forensic investigators
- Students who are learning about security monitoring tools
- Organizations that track network traffic and anomalies

# 3. Methodology
# Setup & Environment
Operating System: Windows
Datasets: Cybersecurity Threat Detection Logs (CSV file in Kaggle)
# Tools utilised:
- Elasticsearch used as the indexing/search engine
- Kibana provides security dashboards with analyses performed within them
- Grafana provides visual comparisons and monitoring capabilities
- Python  to assist with data cleansing and formatting.

# Architecture / Workflow:
<img width="908" height="680" alt="Screenshot 2025-11-27 002209" src="https://github.com/user-attachments/assets/a55f92da-7219-4fcc-aa7b-a8df42dedb41" />

# Step-by-Step Process:
1. Download the dataset
2. Clean and format fields (time format, path structure, type of data)
3. Set up Elasticsearch & Kibana on a Windows machine
4. Import the cleaned up data into an Elasticsearch index
5. Develop visualizations in Kibana (activity, IPs by distribution, protocols)
6. Set up a Grafana dashboard for side-by-side comparison
7. Test, analyze and validate the results
8. Identify insights and record them

# 4.Results
# Visualization & Analysis (Kibana)
# 1. Action Distribution(Blocked vs Allowed)
Description:
- This chart provides a quick view of the difference between the total number of network actions that were allowed versus those that were blocked when using the network security systems with respect to both inbound and outbound Internet Protocol (IP) connections.
Data Fields:
- The action
- The timestamp
Observations:
- The data shows that for both inbound and outbound connections that were initiated from this location, the number of inbound requests and outbound responses blocked was approximately equal in total counts when compared with all actions that were allowed.
- Such a finding would indicate a proper balance between filtering the data traffic that passes through these devices and allowing for valid connections.

![alt text](<Action Distribution.png>)

# 2. Top Protocols in Network Logs
Description:
- The top protocols (TCP, HTTP, UDP) captured by the Network Log Analytics (NLA) provide insights into the types of services being utilized on your network.
Data Fields:
- protocol
- timestamp
Insight:
- With both TCP and HTTP comprising a large percentage of incoming and outgoing messages, it is reasonable to assume that most of the traffic being collected consists of Web and Application service communications.
- Monitoring the protocols in this manner will help to identify abnormal data transfer behavior.
  
![alt text](<Top Protocols in Netwrok Logs.png>)

# 3. Top 10 Source IPs Generating Traffic
Description:
- The chart below displays all IPs that produced the highest total number of log entries, which is useful for identifying either devices or external hosts that produce unusually large volumes of data transfers.
Data Fields:
- source_ip
- bytes_transferred
Insight:
- An unusually high volume of requests from one or more IP addresses may indicate that either an aggregated data set was uploaded/downloaded from that IP address or that some form of automated scanning or brute-force attempts were being conducted from those IP addresses.

![alt text](<Top 10 Source IPs generating Traffics.png>)

# 4. Threat Type Distribution
Description:
- Visual Representation of Log Threat Labels, represents Safe vs. Potentially Harmful Activity.
- The visual representation below lists the logs received by an organization by their corresponding threat label (benign, suspicious, or malicious).
Data Fields Used:
- Threat Label
- Log Date/Time
Insight:
- Most of the log entries have a threat label of "benign," which signifies normal business operations being conducted on the network.
- Nevertheless, the presence of entries with threat labels of "suspicious" and "malicious" provides evidence that there are potential risks to the integrity of the network, and further scrutiny and or remedies are necessary and will require mitigation efforts.
![alt text](<Threat Type Distribution.png>)

# 5. Dashboard Summary
# Description:
- The use of a single dashboard in Kibana enabled all visualizations to provide one location for viewing key information related to your networks.
- The Kibana interface offers a way to view network activity as it happens and analyze trends over time, thus allowing administrators to see current activity and determine whether or not that activity matches previously established patterns.
# Key Observations:
- The total number of blocked versus allowed connections is evenly distributed.
-  Web-based protocols (HTTP, HTTPS, and TCP) accounted for the majority of the data transmitted.
- There are a small number of source IP addresses creating most of the network traffic.
- While the majority of the transmitted data is considered non-malicious, there were suspicious and/or clearly malicious transmissions detected.
 
#Extended Findings (ElasticSearch)

1. Top 10 IP Addresses With Action (Allowed vs Blocked)

Description:
This sunburst visualization shows the top 10 source IP addresses in the dataset and breaks down their corresponding actions (allowed or blocked). 
Each outer slice represents how that specific IP's traffic was handled by the security system.

Interpretation:

- The top three IPs — 109.47.72.119, 44.137.187.63, and 61.72.172.125 — each contribute roughly 10% of all recorded traffic.
- Most high-volume IPs display a near-even split between allowed and blocked traffic (each around 4.8–5.2%).
- This suggests these hosts consistently interact with the network and are subject to security filtering rather than wholesale blocking.
- The repetition of near-equal allowed/blocked percentages indicates that security rules are actively evaluating traffic instead of blanket-blocking entire IPs, which is consistent with adaptive or behavior-based filtering rather than static denylists.

Key Security Insight:
A handful of IP addresses generate the majority of activity. While the even distribution of allowed/blocked actions suggests legitimate mixed traffic, the high volume itself warrants deeper inspection — these could represent automated services, misconfigured clients, or early signs of reconnaissance (e.g., repeated attempts triggering both approvals and denials).

2. Log Volume by Day (Top Values)
Description:
This bar chart displays the highest daily log counts in the dataset.
It highlights specific dates where activity significantly spikes.

Interpretation:

Two dates show notably elevated activity: April 19, 2024 (2,028 logs) and August 21, 2024 (2,007 logs).
This is nearly double the activity seen on the other days, which hover around 1,029–1,035 logs.

These spikes may indicate:
  - Scheduled system scans
  - High-traffic operational periods
  - Potential probing or brute-force attempts
  - Large bursts of automated activity

The remaining dates show an extremely consistent pattern (~1,030 logs), suggesting typical daily baseline traffic volume.

Key Security Insight:
The two high-activity days should be investigated to identify whether the spike correlates with increased blocked actions, repeated attempts from the same IP, or a sudden rise in suspicious or malicious threat labels. Consistent baseline volume across the remaining days confirms that most days follow predictable network behavior.

3. Hourly Activity: Blocked vs Allowed (Bar Chart)

Description:
This visualization compares the total number of blocked versus allowed network actions aggregated at the hourly level. 
It provides a clear view of how traffic is being filtered throughout the day and whether blocking patterns differ significantly from allowed activity.

Data Summary:

Blocked: 522,617 events
Allowed: 522,679 events

Interpretation:
The counts are nearly identical, with a difference of only **62 hour difference** between allowed and blocked.
This extremely balanced ratio suggests that the network’s filtering and detection systems are actively evaluating each request individually, rather than defaulting toward a heavier allow-or-deny bias.

The similarity in counts also indicates:
Traffic is highly mixed, with roughly half of all hourly events deemed suspicious or noncompliant.

This balanced filtering is characteristic of environments with:

- Regular automated scanning
- Frequent request retries
- Systems that generate both legitimate and malformed requests
- Potential low-level reconnaissance attempts that repeatedly trigger both outcomes

Key Security Insight:
Because the system blocks and allows traffic at almost identical rates, monitoring the context around each change (such as spikes in blocked actions during certain hours or repeated failures from specific IPs) becomes more important than relying on raw event volume. The even distribution suggests that while the network is performing as expected, high variability in request quality may indicate ongoing **probing** or **repeated automated processes** interacting with the system.

4. Request Path (Blocked vs Allowed)

Description

This chart visualizes the number of **allowed** and **blocked** requests across the most common request paths. 
It highlights which URL endpoints receive the highest volume of traffic and how often that traffic is denied due to security controls.

Data Summary

- / — 238,667 allowed, 239,067 blocked
- /login — 35,896 allowed, 36,198 blocked
- /admin/config — 19,943 allowed, 19,884 blocked
- /auth — 19,608 allowed, 19,746 blocked
- /api/v1/data — 19,645 allowed, 19,531 blocked

Interpretation:
The root path **/** received by far the most traffic, with almost equal proportions of allowed and blocked requests, suggesting **aggressive scanning** or **broad probing** behavior.
Sensitive paths such as **/login**, **/auth**, and **/admin/config** also show sizable traffic and near parity between allowed and blocked requests, indicating repeated authentication attempts or automated probing for admin interfaces.

Key Security Insight:
High traffic access attempts to authentication and administrative paths may indicate brute-force attempts, and potential automated recon activity.
The nearly equal split between allowed and blocked requests suggests that while the security system is filtering many requests, potentially risky traffic is still reaching the application.
Indicating a need for tighter access control or rate-limiting on sensitive endpoints.
