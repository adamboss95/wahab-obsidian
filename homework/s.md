
### Phishing Types
##### Spear phishing
[Spear phishing] involves targeting a specific individual in an organization to try to steal their [login credentials]. The attacker often first gathers information about the person before starting the attack, such as their name, position, and contact details.
##### Email phishing
In an [email phishing] scam, the attacker sends an email that looks legitimate, designed to trick the recipient into entering information in reply or on a site that the hacker can use to steal or sell their data.

##### Pharming
In a [pharming] attack, the victim gets malicious code installed on their computer. This code then sends the victim to a fake website designed to gather their login credentials.

##### Evil Twin Attack
In an evil twin attack, the hacker sets up a false Wi-Fi network that looks real. If someone logs in to it and enters sensitive details, the hacker captures their info.

##### Whaling Attack
A [whaling attack] is a phishing attack that targets a senior executive. These individuals often have deep access to sensitive areas of the network, so a successful attack can result in access to valuable info.

##### Clone Phishing Attack
A clone phishing attack involves a hacker making an identical copy of a message the recipient already received. They may include something like “resending this” and put a malicious link in the email.

##### Deceptive phishing
Deceptive phishers use [deceptive technology] to pretend they are with a real company to inform the targets they are already experiencing a cyberattack. The users then click on a malicious link, infecting their computer.

##### Social Engineering
[Social engineering] attacks pressure someone into revealing sensitive information by manipulating them psychologically.



### Brute Force Attack:
A hacking method that involves systematically trying every possible combination of passwords or keys until the correct one is found.

#### Types of Brute Force Attacks:

1. **Simple Brute Force Attack:**
    Involves trying all possible combinations of passwords without any modifications or optimizations.
        
2. **Dictionary Attack:**
    Uses a pre-defined list of common words and phrases to guess the password.
        
3. **Hybrid Attack:**
    Combines dictionary attacks with additional variations like adding numbers or symbols to common words.
        
4. **Reverse Brute Force Attack:**
    Starts with a known password and tries to match it against multiple usernames.
        
5. **Credential Stuffing:**
    Uses stolen username-password pairs from one service to try and gain access to other services.


### CIA
In cybersecurity, **CIA** stands for **Confidentiality, Integrity, and Availability**. These three principles are the foundational pillars of information security:

1. **Confidentiality:**
    Ensuring that sensitive information is accessed only by authorized individuals and remains protected from unauthorized access.
        
2. **Integrity:**
    Maintaining the accuracy and completeness of data, ensuring that it is not altered or tampered with by unauthorized individuals.
        
3. **Availability:**
    Ensuring that information and resources are accessible to authorized users whenever needed, without undue delay.

**Non-repudiation** is a principle that ensures that a party in a communication cannot deny the authenticity of their signature on a document or a sent message


### Cyber Kill Chain
The **Cyber Kill Chain** is a model developed by Lockheed Martin to describe the stages of a cyberattack, from initial reconnaissance to achieving the attacker's objectives

#### Seven Stages of Cyber Kill Chain
**Reconnaissance:** The attacker gathers information about the target to find vulnerabilities
**Weaponization:** The attacker creates malware or tools to exploit the identified vulnerabilities
**Delivery:** The attacker delivers the weaponized payload to the target system, often through phishing emails or compromised websites
**Exploitation:** The attacker exploits the vulnerabilities to gain access to the target system
**Installation:** The attacker installs additional tools or malware to maintain access and control over the system
**Command and Control (C2):** The attacker establishes a command and control channel to remotely control the compromised system
**Actions on Objectives:** The attacker achieves their goals, such as data exfiltration, destruction, or disruption

Example:
**WannaCry** exploited a vulnerability in Microsoft Windows called **EternalBlue**, which was originally developed by the U.S. National Security Agency (NSA)
#### **WannaCry ransomware attack**:

##### Steps of the Cyber Kill Chain:

1. **Reconnaissance:**
    
    - Attackers identified systems primarily running Microsoft's Windows 7 and Windows Server 2008 as their targets. They gathered information about these systems to find vulnerabilities.
        
2. **Weaponization:**
    
    - The attackers weaponized the EternalBlue exploit, which took advantage of a vulnerability in Microsoft's implementation of the Server Message Block (SMB) protocol (CVE-2017-0144). They created the WannaCry ransomware using this exploit.
        
3. **Delivery:**
    
    - The ransomware was delivered via phishing emails and malicious downloads. Users unknowingly downloaded and executed the ransomware.
        
4. **Exploitation:**
    
    - Upon gaining access to a system, the EternalBlue exploit was used to compromise the target. This allowed the ransomware to execute on the victim's machine.
        
5. **Installation:**
    
    - The ransomware then encrypted user files, effectively locking them and making them inaccessible to the user.
        
6. **Command & Control (C2):**
    
    - After successful installation, the ransomware connected to an external server operated by the attackers to report a new infection and to update its encryption algorithms.
        
7. **Actions on Objectives:**
    
    - The ransomware displayed a ransom note, demanding payment in Bitcoin to decrypt the files. Victims were forced to pay the ransom to regain access to their files.





### MITR Attack
the **MITRE ATT&CK** framework is a comprehensive knowledge base of adversary tactics and techniques based on real-world observations.

#### Key Components of MITRE ATT&CK:

1. **Tactics:** The "why" of an attack, representing the adversary's goals (e.g., initial access, execution, persistence).
2. **Techniques:** The "how" of an attack, describing the methods adversaries use to achieve their goals (e.g., phishing, credential dumping).
3. **Sub-techniques:** More specific descriptions of adversarial behavior within a technique.
4. **Procedures:** Specific implementations or real-world examples of techniques and sub-techniques.
#### Key Tactics in the MITRE ATT&CK Framework

1. **Reconnaissance:** Gathering information about the target.
    
2. **Resource Development:** Establishing resources for the attack.
    
3. **Initial Access:** Gaining entry into the target environment.
    
4. **Execution:** Running malicious code on the target system.
    
5. **Persistence:** Maintaining access to the target system.
    
6. **Privilege Escalation:** Gaining higher-level permissions.
    
7. **Defense Evasion:** Avoiding detection and defenses.
    
8. **Credential Access:** Stealing account credentials.
    
9. **Discovery:** Identifying information about the target environment.
    
10. **Lateral Movement:** Moving through the target environment.
    
11. **Collection:** Gathering data from the target.
    
12. **Command and Control:** Communicating with compromised systems.
    
13. **Exfiltration:** Stealing data from the target.
    
14. **Impact:** Disrupting or destroying the target environment.

#### Example NotPetya Ransomware Attack

**Reconnaissance:**

- Attackers identified vulnerabilities in the Ukrainian financial sector and targeted companies using the M.E.Doc accounting software.
    

**Initial Access:**

- The attackers gained initial access by compromising the update mechanism of the M.E.Doc software, distributing the malware as a legitimate software update.
    

**Execution:**

- Once inside the network, the malware executed a payload that encrypted the victim's files and displayed a ransom note.
    

**Persistence:**

- The malware established persistence by creating scheduled tasks and modifying registry keys to ensure it would run on system reboot.
    

**Privilege Escalation:**

- NotPetya used the EternalBlue exploit and other techniques to escalate privileges and spread laterally across the network.
    

**Defense Evasion:**

- The malware used various techniques to evade detection, such as disabling security software and clearing event logs.
    

**Credential Access:**

- NotPetya harvested credentials from infected machines using tools like Mimikatz.
    

**Discovery:**

- The malware performed network discovery to identify other vulnerable systems within the network.
    

**Lateral Movement:**

- Using the harvested credentials and exploits, NotPetya moved laterally across the network, infecting other machines.
    

**Collection:**

- The malware collected sensitive data from the infected systems.
    

**Command and Control:**

- NotPetya communicated with command and control servers to receive instructions and report infection status.
    

**Exfiltration:**

- The malware exfiltrated collected data to the attacker's servers.
    

**Impact:**

- The primary impact was data encryption, rendering systems inoperable and causing significant disruption to businesses worldwide.





### What is Ransomware?

- **Definition:** Ransomware is a form of malware that encrypts a victim's data or locks them out of their system, demanding a ransom payment to restore access
- **Attack Method:** Attackers typically gain access to a system through phishing emails, infected websites, or exploiting software vulnerabilities. Once inside, the ransomware encrypts files or locks the system, making it unusable until the ransom is paid
- **Ransom Demand:** The ransom is usually demanded in cryptocurrency (e.g., Bitcoin) to make it harder to trace

Types of Ransomware:
- **Encrypting Ransomware:** This type encrypts the victim's data, making it inaccessible until the ransom is paid and the decryption key is provided
- **Non-Encrypting Ransomware:** This type locks the victim out of their system, often displaying a ransom note on the screen
- **Double-Extortion Ransomware:** In addition to encrypting data, this type also threatens to leak stolen data if the ransom is not paid
- **Triple-Extortion Ransomware:** This type takes the threat further by using stolen data to attack the victim's customers or business partners



### DoS (Denial of Service)

1. **What it is:**
    
    - A DoS attack involves a single source (one computer or network) overwhelming a target system (such as a website or server) with excessive traffic or requests.
        
    - The goal is to make the target system slow, unresponsive, or completely unavailable to legitimate users.
- **How it works:**
    
    - The attacker sends a large number of requests or data packets to the target, consuming its resources (like CPU, memory, or bandwidth) until it can no longer respond to legitimate traffic.
        
- **Example:**
    
    - Imagine a small shop where only one customer is allowed to enter at a time. If one person keeps going in and out repeatedly, real customers won't be able to enter and make purchases.

Real Life Example:
**Project Rivolta (2000):** This attack targeted 16 major companies, including well-known names like Amazon, eBay, and CNN. The attackers overwhelmed these companies' servers with a flood of traffic, causing significant downtime and financial losses estimated at $1.7 billion. The attack exploited the relatively nascent state of internet security at the time, leading to widespread disruption.



### DDoS (Distributed Denial of Service)

1. **What it is:**
    
    - A DDoS attack is similar to a DoS attack but involves multiple sources (often thousands or millions of compromised computers, also known as a botnet) targeting a single system.
        
    - The goal is the same: to make the target system slow, unresponsive, or completely unavailable to legitimate users.
        
2. **How it works:**
    
    - The attacker uses a botnet to send a massive amount of traffic or requests to the target system, overwhelming its resources. Because the attack comes from many different sources, it's harder to block or mitigate.
        
3. **Example:**
    
    - Imagine the same small shop, but now thousands of people are trying to enter at the same time. The shop will be overwhelmed, and real customers won't be able to enter.



