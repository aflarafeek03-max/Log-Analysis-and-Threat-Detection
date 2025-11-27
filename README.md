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
