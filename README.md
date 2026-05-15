# SOC-lab
Project Name: FireOps Systems Threat Monitoring
Date: May 14, 2026
Author: Purine Wambita
Tools Used: Wazuh (SIEM/XDR), Ubuntu Server, Oracle VirtualBox

1. Executive Summary
The goal of this lab was to establish a functional Security Operations Center (SOC) environment to monitor endpoint activity and detect potential security breaches. By deploying a Wazuh Manager on an Ubuntu server and connecting remote agents, I successfully achieved real-time visibility into system logs and validated the setup through a simulated brute-force attack.

2. Project Architecture
The environment was built using a virtualized network to ensure isolation and safety:

SIEM Manager: Wazuh running on Ubuntu 26.04 LTS.

Endpoints: windows.

Network: Configured via VirtualBox using Bridged adapter to allow communication between the manager and agents.

3. Implementation Steps
Phase 1: SIEM Deployment

Server Preparation: Installed and updated Ubuntu Server.

Wazuh Installation: Utilized the Wazuh installation assistant to deploy the indexer, server, and dashboard.

Verification: Confirmed the web interface was accessible via the browser.

Phase 2: Agent Enrollment

Deployed the Wazuh Agent on the target endpoint.

Modified the ossec.conf file to point to the Manager's IP address.

Verified the agent status as "Active" in the Wazuh Dashboard.
<img width="1920" height="1080" alt="Screenshot (39)" src="https://github.com/user-attachments/assets/99613b1d-eb8d-401e-b4e7-a3eb71372398" />

4. Threat Simulation & Incident Detection
This is the core of the project where I validated the SOC's capability to detect malicious activity.

Scenario: SSH Brute Force Attack.

The Action: Attempted multiple failed logins from a remote machine to the monitored Ubuntu endpoint.

The Detection: The Wazuh Manager analyzed the auth.log files and identified a pattern of failures.

The "First Alert" Moment
<img width="1920" height="1080" alt="Screenshot (58)" src="https://github.com/user-attachments/assets/fb179d3c-e28a-4c35-9532-51f3e162c905" />

Wazuh Dashboard displaying a Level 10 alert for a Brute Force attack.

Technical Analysis of the Alert:

Rule Triggered: 5712 (SSHD brute force trying to get access).

Observation: The system correctly identified the source IP and the frequency of the attempts, providing immediate situational awareness.

5. Challenges & Troubleshooting
Connectivity: Initially, the agent could not reach the manager. I diagnosed this as a firewall issue and allowed traffic on port 1514/1515, which resolved the issue.

Resource Management: Adjusted RAM allocation in VirtualBox to ensure the Wazuh Indexer had enough memory to process logs efficiently.

6. Conclusion & Future Roadmap
This lab successfully demonstrated the power of centralized logging and real-time alerting.
Next Steps:

Integrate Suricata for Network Intrusion Detection (IDS).

Create custom Active Response scripts to automatically block IPs after a detected attack.

Explore Cloud-native security by migrating this setup to an AWS environment.
