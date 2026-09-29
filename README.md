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

(Left off with having Windows 10 and Ubuntu2 connected to Wazuh and need to write rules(STEP 4)).
