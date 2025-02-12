


| IOA                                                                                                                 | IOC                        |
| ------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| Proactive                                                                                                           | Reactive                   |
| Credential theft=> means if credentials are stolen cyberattack is in progess                                        | IPAddress                  |
| Credential exploitation => after credential theft, next step is exploitation of the network or system.              | Vulnerability Exploitation |
| Lateral Movement => attacker moving lateraly, trying to exploit the credentials stolen to move to different segment | Malware Injection          |
| c2 communications                                                                                                   | Cyber Threat Signatures    |
| Data Exfiltration                                                                                                   | Static                     |

IOC limitations:
- IOC detection compares potential threats to a database of known attack signatures






### IOA (Indicators of Attack)

- **Focus:** Detects ongoing or imminent attacks by identifying suspicious behaviors or patterns.
    
- **Proactive:** Helps identify potential threats before they cause significant damage.
    
- **Example:** Unusual network traffic, unauthorized access attempts, or abnormal user behavior.
    

### IOC (Indicators of Compromise)

- **Focus:** Identifies evidence that a system or network has already been compromised.
    
- **Reactive:** Used after an attack has occurred to investigate and respond to security incidents.
    
- **Example:** Malware signatures, unusual files, or unauthorized changes to system configurations.
    

### Key Differences:

- **Timeframe:** IOAs are used during the early stages of an attack, while IOCs are used after an attack has occurred.
    
- **Purpose:** IOAs help detect and prevent attacks, while IOCs help investigate and mitigate the impact of breaches.
    
- **Nature:** IOAs are proactive and behavior-based, while IOCs are reactive and evidence-based.