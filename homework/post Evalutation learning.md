## NAT

Translates private IP to public IP and Public IP to Private IP to gain access to internet.

> [!NOTE]
> we cannot access internet through private ip, internet can be access only by public ip, which is where NAT helps us access internet by translating private ip to public ip and public ip to private ip


### DMARC (Domain-based Message Authentication, Reporting & Conformance)

- **Purpose**: Provides instructions to receiving email servers on how to handle emails that fail SPF or DKIM checks
**Function**: Allows domain owners to publish policies in their DNS records, specifying how to check the From field and what to do if the email fails authentication
**Benefits**: Helps protect domains from being used in email scams and phishing attacks
### DKIM (DomainKeys Identified Mail)

- **Purpose**: Verifies that an email message was not altered in transit and that it truly comes from the claimed domain
- **Function**: Uses cryptographic signatures to sign email headers, which can be verified by the recipient using the sender's public key stored in DNS
- **Benefits**: Ensures the integrity and authenticity of email messages
### SPF (Sender Policy Framework)

- **Purpose**: Specifies which mail servers are authorized to send emails on behalf of a domain
- **Function**: Domain owners publish SPF records in their DNS, listing the IP addresses of authorized sending servers
- **Benefits**: Helps prevent unauthorized use of a domain to send spam or phishing emails