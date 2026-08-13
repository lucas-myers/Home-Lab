# Home-Lab
My homelab containing Proxmox, Windows, Kali, pfSense, Splunk, Docker, and Cisco switches


My homelab is currently setup    

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
