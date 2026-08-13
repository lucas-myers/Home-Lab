# Home-Lab
My homelab containing Proxmox, Windows, Kali, pfSense, Splunk, Docker, and Cisco switches

Graphics Card: GTX 1060 6 GB
Memory: 16 GB 3200 
CPU: Ryzen 3 3300X
OS: Proxmox

My home lab is currently setup, I don't have everything running at all times as my home lab computer only holds 16 GB, but I am planning to upgrade to 32 GB.

My plan with this lab is to test attacks on the kali machine, then on the other windows 11 machine with sysmon/wazuh running off a docker image on the ubuntu server I will review the attack with a write up.

I also have the ubuntu server running OWASP Juice Shop for web vulnerabilities.

I wanted to explore more in windows server, so I am running a vm of Windows Server 2022 and set up Active Directory.

                              ┌──────────────────────┐                                      

                              │       INTERNET       │
                              │      ISP / WAN       │
                              └──────────┬───────────┘
                                         │
                                         │ WAN
                                         ▼
                              ┌──────────────────────┐
                              │       pfSense        │
                              │      FIREWALL        │
                              │                      │
                              │ WAN: ISP             │
                              │ LAN: 192.168.50.1    │
                              └──────────┬───────────┘
                                         │
                                         │ LAN
                                         │ 192.168.50.0/24
                                         │
                                  ┌──────┴──────┐
                                  │             │
                                  │   vmbr1     │
                                  │ Proxmox LAN  │
                                  │             │
                                  └──────┬──────┘
                                         │
             ┌───────────────────────────┼───────────────────────────┐
             │                           │                           │
             │                           │                           │
             ▼                           ▼                           ▼
     ┌──────────────┐           ┌──────────────┐            ┌──────────────┐
     │     DC01     │           │     PC01     │            │    Ubuntu    │
     │ Windows      │           │ Windows 11   │            │    Server    │
     │ Server       │           │              │            │              │
     │              │           │              │            │              │
     │ AD DS        │           │ Domain       │            │ Linux        │
     │ DNS          │           │ Workstation  │            │ Services     │
     │              │           │              │            │              │
     │ 192.168.50.20│           │ DHCP         │            │ DHCP         │
     └──────┬───────┘           └──────┬───────┘            └──────┬───────┘
            │                          │                           │
            │                          │                           │
            └──────────────────────────┼───────────────────────────┘
                                       │
                                       │
                              ┌────────▼────────┐
                              │   Active        │
                              │   Directory     │
                              │                 │
                              │    lab.local    │
                              └─────────────────┘
                                       │
                         ┌─────────────┼─────────────┐
                         │             │             │
                         ▼             ▼             ▼
                    ┌─────────┐  ┌─────────┐  ┌────────────┐
                    │ Users   │  │ Groups  │  │   GPOs     │
                    └─────────┘  └─────────┘  └────────────┘


                         SECURITY / ATTACK SIDE
                         
                              ┌──────────────┐
                              │     Kali     │
                              │    Linux     │
                              │              │
                              │ Nmap         │
                              │ Impacket     │
                              │ BloodHound   │
                              │ Wireshark    │
                              │              │
                              │ 192.168.50.x │
                              └──────┬───────┘
                                     │
                                     │
                              ┌──────▼──────┐
                              │ AD LAB      │
                              │             │
                              │ DC01        │
                              │ PC01        │
                              │ Users       │
                              └─────────────┘


                         SECURITY MONITORING SIDE

                              ┌──────────────┐
                              │    Wazuh    │
                              │   Manager   │
                              │             │
                              │ SIEM / EDR  │
                              │ Log Analysis │
                              └──────┬───────┘
                                     │
                         ┌───────────┼───────────┐
                         │           │           │
                         ▼           ▼           ▼
                       DC01        PC01       Ubuntu
                         │           │           │
                         └───────────┴───────────┘
                               Windows/Linux
                                  Logs
