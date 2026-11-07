# SIEM-Home-Lab-with-Detection-Engineering

For the lab I am going to use Wazuh as it is a very popular and well used open source SIEM

I downloaded Ubuntu and used this command for the installation:
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

Here I have finished Installing Wazuh and got my user and password:

<img width="1063" height="575" alt="image" src="https://github.com/user-attachments/assets/f89302b6-6693-483a-ba77-95055e76f62a" />

In Wazuh I deployed a new agent using the server address of the ubuntu machine itself:

<img width="1656" height="1094" alt="image" src="https://github.com/user-attachments/assets/ad6d298d-79db-45ae-a6b6-e70613a7214d" />

The first agent im going to use is another Ubuntu Agent where I will run these command on the terminal for "Ubuntu2":

<img width="1632" height="655" alt="image" src="https://github.com/user-attachments/assets/bf9f0d7e-5766-43a7-9b65-fd18924fbef6" />

The Agent installation was successful and is now active:

<img width="2224" height="601" alt="image" src="https://github.com/user-attachments/assets/0d8cd810-46cf-434a-a272-e366c1bcea69" />


I also set up a 3rd device, a windows 10 VM with Sysmon and SwiftOnSecurity

<img width="2205" height="942" alt="image" src="https://github.com/user-attachments/assets/dcd58b26-51fc-4537-9f2c-a63928c74796" />

With the assistance of claude I created a XML detection rules set in Wazuh to identify malicious behavior using Sysmon telemetry, specifically targeting MITRE ATT&CK techniques like LSASS Memory Dumping.

<img width="1477" height="911" alt="image" src="https://github.com/user-attachments/assets/18cacf35-eed5-40bb-b204-660d0f5a46d2" />


To validate the rules, I utilized Atomic Red Team to simulate multiple variations of LSASS credential dumping on the Windows endpoint.
"Invoke-AtomicTest T1003.001" 

The Wazuh agent successfully forwarded the Sysmon Event ID 1 telemetry to the SIEM. The custom XML rules triggered High-Severity (Level 12 and 13) alerts in the Wazuh dashboard, proving the detection pipeline is fully functional.

<img width="2269" height="1149" alt="image" src="https://github.com/user-attachments/assets/57dc8f80-8bff-4a0a-aaf1-4855c89db250" />

I mapped the validated detections back to the MITRE ATT&CK framework to visually document the SIEM's current detection capabilities for Credential Access.

<img width="1158" height="826" alt="image" src="https://github.com/user-attachments/assets/e11e5d7d-7a7a-4fa5-97dd-fe91771d1945" />





# Challenges Encountered & Troubleshooting
* **Telemetry Ingestion Failure:** Initially, the custom rules failed to trigger because the Wazuh agent was not forwarding Sysmon events to the SIEM. I diagnosed the pipeline break by verifying the raw Event ID 1 logs locally in Windows Event Viewer, then elevated Notepad to Administrator to modify `C:\Program Files (x86)\ossec-agent\ossec.conf`. I added a `<localfile>` block for the `Microsoft-Windows-Sysmon/Operational` event channel, restarted the Wazuh service, and successfully restored data flow.
* **Endpoint Defenses:** Windows Defender initially blocked and quarantined the Atomic Red Team payloads. To ensure the attack execution and log generation succeeded, I manually disabled Real-Time Protection for the duration of the simulation.

# Known Gaps & Future Work
While OS Credential Dumping via LSASS memory (T1003.001) is now successfully monitored, this project highlighted coverage gaps for other credential access sub-techniques, specifically Security Account Manager (T1003.002) and NTDS (T1003.003). Future iterations will focus on engineering detection rules for these additional vectors.


