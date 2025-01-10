# SIEM Lab on Elastic Cloud with Ubuntu Linux [![License](https://img.shields.io/badge/License-MIT-green)](./LICENSE)
---
## *What is SIEM and what is its importance in the Security world?*
SIEM (Security Information and Event Management) is a cybersecurity solution that collects, organises, 
and analyses data from several sources within an organization's infrastructure, including servers, devices, 
and security systems. It brings together Security Information Management (SIM) and Security Event Management (SEM) to detect, monitor, and respond
to potential security risks in real time. SIEM systems normalise data, correlate events, generate alerts, and provide visual dashboards to monitor security problems.

SIEM is critical for detecting threats, ensuring compliance, and responding to incidents. It enables organisations to spot security issues, automate compliance reporting,
and respond quickly to breaches. SIEM improves operational efficiency and boosts an organization's overall security posture by centralising security monitoring and enabling 
forensic analysis.

---
## *Prerequisites*
These are some of the tools I used:
- Elastic Cloud Account: Access to the Elastic Cloud platform (I used the free trial).
- Ubuntu Linux Machine: A local or virtual machine running Ubuntu 20.04 or later.
<img width="1439" alt="Screenshot 2025-01-10 at 11 07 50 AM" src="https://github.com/user-attachments/assets/3e691ce0-1699-432c-ba24-64a49fbbecac" />

*Image 1 = My Ubuntu Linux VM*

- Basic knowledge of SIEM concepts: Understanding of how SIEM systems work, especially in real-time security monitoring and threat detection.
---

## *Tools Required:*
- Elastic Stack (Elasticsearch, Kibana, Logstash)
- Ubuntu Linux Server
- Curl and SSH for interacting with servers

---
## *Installation*:
Installation
1. Elastic Cloud Setup:
Create a cluster on Elastic Cloud by visiting Elastic Cloud.

<img width="1431" alt="Screenshot 2025-01-10 at 10 51 23 AM" src="https://github.com/user-attachments/assets/7617d012-ad33-4c24-bcf5-398200785daf" />

*Image 2 = This is what the Elastic cloud server looks like after an instance has been deployed.*

2. Configure your cluster to include Elasticsearch and Kibana.
   Note your Elastic Cloud credentials (username, password, and cluster URL).
   
3. Install Filebeat on Ubuntu:
Filebeat will be used to ship logs from your Ubuntu machine to your Elastic Stack cluster.

```bash
sudo apt-get update
sudo apt-get install filebeat
```
4. Configure Filebeat:
Edit the filebeat.yml configuration file to point to your Elastic Cloud cluster:
```bash
sudo nano /etc/filebeat/filebeat.yml
```
5. Add your Elastic Cloud URL and credentials under the output.elasticsearch section:

```yaml
output.elasticsearch:
  hosts: ["https://your-cluster-id.region.elastic-cloud.com:9243"]
  username: "your-username"
  password: "your-password"
```
6. Enable and start the Filebeat service:
```bash
sudo systemctl enable filebeat
sudo systemctl start filebeat
```
## *Lab Setup*
- Elasticsearch is used to store, search, and analyze log data in real-time.
- Kibana provides a web interface for visualization and exploration of logs and metrics.
- Logstash (optional) can be used to process and filter incoming logs before they are sent to Elasticsearch.
- Elastic Defend is used to add rules to the alerts

<img width="1169" alt="Screenshot 2025-01-10 at 10 58 08 AM" src="https://github.com/user-attachments/assets/cad120ec-e372-4e02-be2e-7b18c2ce7071" />

*Image 3 = Adding Integrations into my deployement (In this case, Elastic Defend).*

<img width="1440" alt="Screenshot 2025-01-10 at 11 13 35 AM" src="https://github.com/user-attachments/assets/a7aebaa9-48e1-479e-b8a0-18baadd1d58b" />

*Image 4*

---
## Steps to Setup Elastic Stack on Elastic Cloud:
- Create an Elasticsearch Cluster: Follow the Elastic Cloud UI prompts to deploy a new cluster.
- Configure Kibana: Once your Elasticsearch cluster is up and running, set up Kibana for data visualization.
- Set up Index Patterns: Create index patterns for your logs to view and analyze data in Kibana.
- Enable Security Features: Configure Kibana for secure access (SSL/TLS) and authentication.
---
## Usage
Once your SIEM lab is set up, you can begin ingesting logs and analyzing security events.

1. Access Kibana:
Open Kibana in your web browser using the URL provided by Elastic Cloud.
Log in with your credentials.
2. Exploring Logs:
<img width="1440" alt="Screenshot 2025-01-10 at 11 48 26 AM" src="https://github.com/user-attachments/assets/a47b6a1b-3c27-4f20-adc0-7f5adc94a85f" />

*Image 5 = Default viewing of the Logs in my SIEM*

4. Navigate to the "Discover" tab:
This allows you to view raw logs and explore the data collected by Filebeat.
5. Create Visualizations:
You can create dashboards to visualize trends, patterns, and anomalies in your data.
<img width="1440" alt="Screenshot 2025-01-10 at 11 49 21 AM" src="https://github.com/user-attachments/assets/949a4429-98ba-49e7-9c3f-a1cccb5c0484" />

*Image 6 = Visualising performance*

6. Set up Alerts:
You can configure Kibana to alert you to specific conditions such as unusual network activity or failed login attempts.
---
## Configurations
1. Filebeat Configuration:
- Ensure your logs (e.g., /var/log/syslog, /var/log/auth.log) are being shipped correctly to Elastic Cloud via Filebeat.
- Update the filebeat configuration file to include paths to relevant log files.
2. Kibana Dashboards:
- Customize dashboards in Kibana for specific use cases, like monitoring server logs, intrusion detection, or user activity.
3. Elastic Security:
- Use the Security tab in Kibana to create detection rules and monitor for threats.
4. Monitoring and Alerting:
- Set up monitoring for log data, system events, and security-related events.
5. Create alerts based on detection rules to automatically notify you of any suspicious activity, such as:
- Multiple failed login attempts
- Unauthorized access attempts
- Unusual network traffic patterns
  
---
## Example alert rule
- Name: Failed login attempts
- Query: event.action: "failed_login"
- Threshold: More than 3 failed login attempts within 10 minutes
---
## Troubleshooting
- Filebeat not sending logs: Ensure the Filebeat service is running correctly.
 You can check the status with:
```bash

sudo systemctl status filebeat
```
Also, check the Filebeat logs for errors:
```bash
sudo tail -f /var/log/filebeat/filebeat.log
```
- Elastic Cloud connection issues: Double-check your Elastic Cloud credentials and Elastic Cloud cluster URL.
Ensure there are no firewall or network issues blocking access.
---
## License
This project is licensed under the MIT License - see the LICENSE file for details.

---
MAIN TOOL USED: SIEM DASHBOARD(ELASTIC CLOUD)
---
## Contact
For questions, feedback, or contributions:
# [![GitHub](https://img.shields.io/badge/GitHub-azraxsif-pink)](https://github.com/azraxsif)
# [asifazra03@gmail.com](mailto:asifazra03@gmail.com) 



