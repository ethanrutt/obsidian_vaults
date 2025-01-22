# OWASP 
- non-profit foundation focused on improving security of software
- resources, tools, more...
- [owasp top 10](https://owasp.org/www-project-top-ten/)
- Good to know and check your programs against this since these are the most common. This is like a sanity check, since most attackers know how to exploit all these vulnerabilities
## Top 10
### Broken Access Control
- Access control enforces policies to prevent users from acting beyond their permissions
- i.e.
	- Accessing another user's data by modifying URL
	- Escalating privileges
- Mitigation
	- Enforce least privilege
	- Deny access by default
### Cryptographic Failures
- Weaknesses in cryptographic algorithms or their implementation
- i.e.
	- using outdated cryptographic protocols (MD5, SHA-1)
	- insecure storage of sensitive data
- Mitigation
	- Use strong crypto algorithms (AES, SHA-256)
	- Properly secure keys and credentials
- downgrade attack
	- There is a known vulnerability in a version, but the next version is used
	- Libraries for legacy support still have vulnerable version *just in case*
	- Attacker can force the communication to downgrade to the vulnerable version and then attack that version
### Injection
- Injection flaws occur when untrusted input is sent to an interpreter
- i.e.
	- SQL Injection `'SELECT * FROM users WHERE id = '" + userInput + "';`
	- Command injection: `exec(userInput)`
- Mitigation
	- Use parametrized queries
	- Validate and sanitize user inputs
### Insecure Design
- Security issues arising from flawed application design
- i.e.
	- Lack of thread modeling
	- Absence of secure development lifecycle
	- Messaging systems that don't have a user login, instead they have a cell phone number as the userid. If a user changes their number and someone gets that new number, then they have access to all of that users messages
	- "First make the code work, then make it secure." **Don't do this**
- Mitigation
	- Integrate security during design phase
	- Conduct regular architecture reviews
### Security Misconfiguration
- Misconfigured security controls or incomplete configurations
- i.e.
	- Default credentials left unchanged
	- Overexposed cloud storage
- Mitigation
	- Regularly audit configurations
	- Apply security hardening guidelines
### Vulnerable and Outdated Components
- Usage of components with known vulnerabilities
- i.e.
	- Running unpatched software
	- Using libraries with critical CVEs
- Mitigation
	- Regularly update software dependencies
	- Use vulnerability scanning tools
### Identification and Authentication Failures
- Failures in auth mechanisms allow attackers to compromise user identities
	- i.e.
		- Weak or default passwords
		- Missing account lockout after multiple failed login attempts
		- Exposed auth tokens in URLs
- Mitigation
	- Enforce strong password policies
	- Implement multi-factor auth
	- Securely store and transmit auth credentials
### Software and Data Integrity Failures
- These occur when software updates, critical data, or CI/CD pipelines are unprotected
	- i.e.
		- Insecure deserialization of objects
		- Manipulation of unsigned software packages
		- Lack of isolation
- Mitigation
	- Use digital signatures to validate data integrity
	- Secure CI/CD pipelines with strict access controls
### Security Logging and Monitoring Failures
- Insufficient logging and monitoring capabilities hinder incident detection and response
	- i.e.
		- Lack of logging for key security events
		- Failure to alert on suspicious activities
- Mitigation
	- Implement centralized logging systems
	- Set up alerts for anomalous behaviors
	- Regularly review logs for suspicious activities
### Server Side Request Forgery
- SSRF flaws occur when a server fetches remote resources without sufficient validation, enabling attackers to manipulate requests
	- i.e.
		- Retrieving internal files via an exposed URL fetch mechanism
		- Scanning internal networks through manipulated requests
		- XSS
- Mitigation
	- Validate and sanitize all URLs and user inputs
	- Block unnecessary outbound requests from servers
	- Use allowlists for permitted domains or IPs

#web #OWASP #OWASPtop10