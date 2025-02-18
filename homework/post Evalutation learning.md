## NAT

Translates private IP to public IP and Public IP to Private IP to gain access to internet.

> [!NOTE]
> we cannot access internet through private ip, internet can be access only by public ip, which is where NAT helps us access internet by translating private ip to public ip and public ip to private ip


### DMARC (Domain-based Message Authentication, Reporting & Conformance)

- **Purpose**: Provides instructions to receiving email servers on how to handle emails that fail SPF or DKIM checks
- **Function**: Allows domain owners to publish policies in their DNS records, specifying how to check the From field and what to do if the email fails authentication
- **Benefits**: Helps protect domains from being used in email scams and phishing attacks

**Example**
Imagine you have a domain called example.com, By setting up a DMARC policy, you can ensure that only authorized servers can send emails on behalf of example.com If an unauthorized email fails the DMARC check, it can be marked as spam or rejected, preventing phishing and scam attempts.
### DKIM (DomainKeys Identified Mail)

- **Purpose**: Verifies that an email message was not altered in transit and that it truly comes from the claimed domain
- **Function**: Uses cryptographic signatures to sign email headers, which can be verified by the recipient using the sender's public key stored in DNS
- **Benefits**: Ensures the integrity and authenticity of email messages
### SPF (Sender Policy Framework)

- **Purpose**: Specifies which mail servers are authorized to send emails on behalf of a domain
- **Function**: Domain owners publish SPF records in their DNS, listing the IP addresses of authorized sending servers
- **Benefits**: Helps prevent unauthorized use of a domain to send spam or phishing emails


### Key Distribution Center (KDC)

A **Key Distribution Center (KDC)** is part of a cryptosystem that helps securely distribute cryptographic keys to users or devices. It's commonly used in systems like **Kerberos**, which authenticate users and services in a network

#### How KDC Works:

1. **Authentication**: The KDC verifies the identity of users or devices requesting access
2. **Key Distribution**: Once authenticated, the KDC provides session keys for secure communication between the user and the service
3. **Ticket Granting**: In Kerberos, the KDC issues tickets that allow users to access services without repeatedly entering credentials

### Certificate Authority (CA)

A **Certificate Authority (CA)** is an entity that issues digital certificates. These certificates verify the ownership of encryption keys used in secure communications, like SSL/TLS for websites.

#### How CA Works:

1. **Verification**: The CA verifies the identity of the entity requesting the certificate.
    
2. **Issuance**: Once verified, the CA issues a digital certificate that contains the entity's public key.
    
3. **Trust**: Browsers and systems trust certificates issued by recognized CAs, ensuring secure communication.
    

### Key Differences:

- **KDC**: Focuses on distributing session keys for secure communication within a network
- **CA**: Issues digital certificates to verify identities and facilitate secure communication over the internet




