# Attack-Defense-Homelab

Home lab on Linux VMs using  Kali and Wazuh

In security, we often are working in smaller and specialized teams that we forget to see the bigger picture. This is often constrained due to large enterprise environments and red/blue specialization in the field. So I decided I would create a home lab that features an attacking machhine, a victim  machine, and a Wazuh based SIEM to monitor logs from the attacker. Below is a network diagram of my project:

                         ┌────────────────────────────────────┐
                         │     VirtualBox Internal Network    │
                         │              “LabNet”              │
                         │        (Completely Isolated)       │
                         └────────────────────────────────────┘
                            │            │                 │
                            │            │                 │
                            ▼            ▼                 ▼
         ┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐
         │   Wazuh Server   │   │  Ubuntu Victim   │   │   Kali Attacker  │
         │  SIEM / Manager  │   │    Target VM     │   │  Pen-Testing VM  │
         ├──────────────────┤   ├──────────────────┤   ├──────────────────┤
         │ Adapter 1:       │   │ Adapter 1:       │   │ Adapter 1:       │
         │ Internal Network │   │ Internal Network │   │ Internal Network │
         │ (“LabNet”)       │   │ (“LabNet”)       │   │ (“LabNet”)       │
         ├──────────────────┤   ├──────────────────┤   ├──────────────────┤
         │ IP: 192.168.50.10│   │ IP: 192.168.50.20│   │ IP: 192.168.50.30│
         │ Role: SIEM       │   │ Role: Victim     │   │ Role: Attacker   │
         └──────────────────┘   └──────────────────┘   └──────────────────┘

                     ✦ All machines can talk to each other  
                     ✦ NO machine can reach the internet  
                     ✦ Host machine CANNOT see the lab  
                     ✦ Safe for attacks, scans, malware tests  

# Setting up the VMs and Network

1) I created 3 VMs within an isolated internal network and configured their IPs to only speak to each other.
2) Used an the quick installation for the Wazuh manager and deployed agents to the Ubuntu victim machine
3) Make sure you do not change the firewall rules on you wazuh manager. This may block agents from contacting it.
4) Begin Attacking!

# SSH From Kali to Victim
<img width="604" height="405" alt="image" src="https://github.com/user-attachments/assets/4fe15d7e-6dca-4d3f-a508-65f3e9216a76" />

1) SSH from Kali to Victim Machine

<img width="899" height="237" alt="image" src="https://github.com/user-attachments/assets/9864ed14-560f-4ab8-8654-d5261ff04287" />

2) Wazuh Manager Detecting SSH Login from Attacker Machine

<img width="917" height="148" alt="image" src="https://github.com/user-attachments/assets/6005fce1-e94d-4b2e-b515-a10c58221a5b" />

3) Wazuh Manager Detecting .txt File Creation on the Victim Machine

# Summary + Future Plans

I'll be tuning alerts and trying different attacks on the victim machine and then viewing them from the defensive side. Feel free to follow along!




