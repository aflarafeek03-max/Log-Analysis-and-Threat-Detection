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

 # Extended Findings (Elasticsearch Queries & Statistics)

# 1. Top 10 IP Addresses With Action (Allowed vs Blocked) ![alt text](<Top 10 ips with action.png>)

Description:
- Sunburst visualisation of the top 10 source IP addresses that were found in the dataset showing all corresponding actions (allowed or blocked).
- Each slice represents how traffic from the specific IP was handled by the security system.
Interpretation:
- In the Top Three IPs 109.47.72.119, 44.137.187.63, and 61.72.172.125 there is close to an equal amount (approximately) each contributes about 10 percent of the total recorded traffic.
- Most High Volume IPs show an almost equal split of allowed/blocked traffic — right around 4.8 to 5.2 percent each.
- This means that these hosts interact consistently with the network and therefore traffic coming from them is subject to some type of security filtering, rather than being completely blocked.
- Since the percentage of both allowed/blocked actions is almost the same, it is likely that the security rules are using Adaptive/Based filtering to evaluate traffic, rather than simply putting them on a Denylist/Block List for that IP. 
Key Security Insight:
- A very limited number of IP addresses generates a large number of the total activity.
- While the fact that there are equal numbers of allowed and blocked indicates the legitimate mix of traffic coming from these IP addresses, the sheer volume of traffic generated warrants further investigation, as it could be possible that this traffic is the result of an automated service; the result of a misconfigured client; or early indicators of attempts to conduct reconnaissance against the network, as evidenced by the fact that the same client IP attempts to connect several times, resulting in both Approval and Denial actions.

# 2. Log Volume by Day (Top Values) ![alt text](<Top 10 logins.png>) 
Description:
The Bar Chart represents The Highest Amount Of Activity Gathered By Users Over the days From The Data Set And The Dates With The Most Activity:
Interpretation:
- There were two notable days of Increased Activity On The Graph: April 19th, 2024, there were 2,028 Logs Recorded; August 21st, 2024, there were 2,007 Logs Recorded.
- Both Of These Days Represent Almost Twice As Much Activity As All The Other Days (Most Days 1,029-1,035).
These spikes may indicate:
 - Scheduled System Scans
 - High Traffic Operational Periods
 - Probing Or Brute Force Attempts
 - Automated Large Bursts Of Activity
The rest of the Days Demonstrated a Consistent Pattern (Average ~1,030). The Consistent Pattern Is an indication Of Normal Daily Activity Levels.
Key Security Insight:
- The two days with increased user activity should be investigated to determine whether increased User Activity resulted from an increased number of blocked actions/an increased number of repeated access attempts by a single IP, or an  increased number of suspicious or malicious threat claims.
- Users were using not only average volume throughout 99% of Days, but it was also an indication of normal network activity and how users typically behave.

# 3. Hourly Activity: Blocked vs Allowed (Bar Chart) ![alt text](<Allowed blocked.png>)
Description:
- This visualization looks at how traffic flows through a network hourly through blocked or allowed actions.
- It gives an overall picture of how the network filters traffic throughout each hour of the day and how regularly and significantly there is a difference between blocked traffic behaviour from allowed traffic behaviour.
Data Summary:
Blocked Traffic: 522,617 events
Allowed Traffic: 522,679 events
Interpretation:
- The totals are nearly equal, with a **62-hour difference** separating the allowed actions from the blocked actions.
- The extraordinarily balanced ratio indicates that both filtering mechanisms and detection mechanisms within the network are looking at each request in isolation, rather than making a decision based on a stronger bias to allow requests versus deny requests.
All the similar events suggest that the vast majority (about half) of events that occurred in each hour would be considered to have the characteristics of non-compliance (suspicious) traffic.
When both filtering systems are equally applied to each event, it is indicative of environments that have:
Constant automated scanning
-  High frequency of retries
-  Systems that generate both valid and invalid requests
-  Low-level reconnaissance of both the blocked event outcomes and those allowed
Key Security Insight:
- Because both the blocking event and allowing event percentages are so nearly equal, it is more important to review the intent of each blocked or allowed event by reviewing the surrounding context, particularly as it relates to blocking events during specific hours (with an influx on particular IPs) instead of only on raw data event volume.
-  The balance suggests that, while the need is apparent, both filtering systems are working and evaluating traffic as it enters the network.

# 4. Request Path (Blocked vs Allowed) ![alt text](<Path.png>)
Description:
- This graph provides an overview of the volume of allowed versus blocked requests for the five most frequently accessed request paths among many.
-  It shows which URL endpoints are accessed the most frequently, and how many of those requests were denied as a result of security measures.
Data Overview:
The following request paths and associated numbers shown on the graph represent this overview of allowed and blocked requests:
- The **/** path has received the greatest amount of traffic with almost equal amounts of allowed and blocked requests.
- This demonstrates that there may be aggressive scanning or broad probing activities.
- There are also significant volumes of traffic on sensitive requests (i.e., "**/login**", "**/auth**" and "**/admin/config**"), as well as nearly equal amounts of allowed and blocked requests.
- This indicates repeated validation attempts or automated probing for admin access points.
Significant Security Insight:
- The high levels of attempts to access authentication and administration system paths may indicate brute-force attacks by way of automated reconnaissance due to the ratio of allowed to blocked requests.
- The results of the analysis suggest that while many requests are filtered out by security controls, there are still risks associated with requests that have been allowed access to the application.
- There may also be a need for stricter security measures and/or rate-limiting placed on these sensitive requests.
Data Summary:
- **/** - 238,667 Allowed | 239,067 Blocked
- **/login** - 35,896 Allowed | 36,198 Blocked
- **/admin/config** - 19,943 Allowed | 19,884 Blocked
- **/auth** - 19,608 Allowed | 19,746 Blocked
- **/api/v1/data** - 19,645 Allowed | 19,531 Blocked
Interpretation:
- The endpoint **/** has generated far more activity than any other, with approximately equal proportions of allowed to blocked traffic, which is indicative of either prolonged periods of **aggressive scanning** and/or broad-based intervals of **persistent probing**.
- Endpoints such as **/login**, **/auth**, and **/admin/config** all experienced considerable amounts of traffic with near parity between allowed and blocked traffic, suggesting frequent attempts to login / authenticate or that an automated probing of the Administrator type interface.

Key Security Insight:
- The volume of access attempts on Authentication and Administrator type endpoints will most likely indicate a **brute force** attempt or at the very least, show patterns of possible automated Recon Activity.
- Also, the near-even split of allowed versus blocked traffic indicates that while the security system is blocking a considerable number of requests, some potentially malicious traffic is still making its way to the application, and emphasizes the need for tighter access controls at the sensitive endpoints or implementing stricter rate limits.

# 5.Comparison of Kibana Visualizations and Kibana Lens Visual Analytics
- In this project, we used two different visualization techniques within Kibana to analyze cybersecurity logs — Basic Kibana Visualizations and Kibana Lens (Elastic Lens).
- While both use the same underlying dataset, they provide different levels of analytical depth and serve different SOC (Security Operations Center) purposes.
- The purpose of this comparison is to illustrate how the use of different analysis methodologies can yield different insights from the same dataset.
- The findings also demonstrate a similarity to Cyber operation workflows, where the use of higher-level dashboards is often used in conjunction with in-depth investigative queries to help validate or dismiss a suspected threat.

# Graph-by-Graph Comparison:
# 1)Security Question Answered: Through what method is traffic filtering accomplished? (Allowed versus Blocked) 
# Kibana Basic Visualization:
Provides summary statistics (the number of allowed and blocked events).
# Kibana Lens Advanced View:
Provides hourly summaries (including details of trends and identification of anomalies) of the number of allowed and blocked connections.
# Graph Numbers Used:
Basic Graph 1 - Lens Graph 3

# 2)Security Question Answered: Which IPs are generating the most activity?
# Kibana Basic Visualization:
Provides a list of the most active IP addresses based on traffic volume.
# Kibana Lens Advanced View:
Includes a sunburst chart that highlights the allow/block ratio for each IP, with a focus on identifying suspicious high-volume IP activity.
# Graph Numbers Used:
Basic Graph 3 - Lens Graph 1

# 3)Security Question Answered: What endpoints have been targeted?
# Kibana Basic Visualization:
Not shown in basic visuals
# Kibana Lens Advanced View:
Allowed vs Blocked requests for the following URIs; (/login, /auth, /admin/config) - Allows identification of active probing/brute force activity
# Graph Numbers Used:
Lens Graph 4

# 4)Security Question Answered: What activity has occurred over time?
# Kibana Basic Visualization:
Not visible in the  basic dashboard
# Kibana Lens Advanced View:
Log Volumes reveal periods of higher activity on April 19 and August 21
# Graph Numbers Used:
Lens Graph 2

# 5)Security Question Answered: Overall Threat Severity Level?
# Kibana Basic Visualization:
Distribution of benign, suspicious, and malicious events
# Kibana Lens Advanced View:
Correlation of threat severity levels over time and IP address patterns is shown.
# Graph Numbers Used:
Basic Graph 4 - Lens Graph 2 & 3

# Key Findings from Comparison:
- Kibana's standard visuals allow for a quick overview of overall network activity so that you can gauge typical usage patterns and how effective filtering is.
- Kibana Lens offers a more detailed approach when performing threat analysis, including the ability to identify irregularities in:
     Time periods during which attacks were heavily concentrated
     IP Addresses performing extensive scanning of your site
     Repeatedly accessing sensitive directories (/login, /auth, /admin/config)
- The combination of these two methods allows you to simulate the activities within a security operations centre (SOC), as analysts would begin their analysis with the higher-level dashboards and drill down from there into more concentrated work views.

# Why This Comparison Is Important:
- Visualising alternative perspectives of the same log data set illustrates how different analytical approaches yield insight into the same dataset, at various levels.
- For example, a basic level visualisation clearly indicates what is occurring within a network, while an updated Lens visualisation provides detailed information regarding the reasoning behind the activities within the network, as well as where to best focus investigative efforts. Providing multiple levels of understanding (analysis) is an essential component of real-world cybersecurity monitoring and threat-hunting.

# 6. Conclusion
# Key Takeaway
- Structured Visual Dashboards Give Unrivaled Threat Detection Visibility
- Multiple Patterns of High Volumes of Suspicious IPs and Accessing the Sensitive Paths Show Potential for Malicious Intent
- An Allow/Block Ratio Provides Context on Raw Volume and Opportunities to Add Contextual Alerts
# Lessons Learned
- Data Cleaning is Essential to Provide Accurate Analysis
- Using Visualization Makes Security Decisions Faster
- Using Multiple Tools (Kibana + Grafana) Increases Monitoring Capabilities
# Future Enhancements
- Add Automatic Alerting and Correlation Rules
- Increase Dataset by Adding more Log Types (Firewall, DNS, Proxy)
- Implement Machine Learning-Based Anomaly Detection
- Containerize the Ingestion and Visualization Pipeline

# References
- Kaggle Cybersecurity Threat Detection Dataset
- Elastic Stack Documentation
- Grafana Documentation
- BFOR 519 Course Resources
- Chat Gpt 5 and Gooogle for some visulization and comparison research
