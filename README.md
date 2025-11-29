# Attack-Defense-Homelab

Home lab on Linux VMs using  Kali and Wazuh

In security, we often are working in smaller and specialized teams that we forget to see the bigger picture. This is often constrained due to large enterprise environments and red/blue specialization in the field. So I decided I would create a home lab that features an attacking machhine, a victim  machine, and a Wazuh based SIEM to monitor logs from the attacker. Below is a network diagram of my project:

                         ┌────────────────────────────────────┐
                         │     VirtualBox Internal Network     │
                         │              “LabNet”               │
                         │        (Completely Isolated)        │
                         └────────────────────────────────────┘
                                      │        │        │
                                      │        │        │
                                      ▼        ▼        ▼
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
