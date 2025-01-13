# Security
- Computational Attack or Threat
	- An action directed against one or more systems with the **intent** to *violate* its security
## ACID
- Authenticity
- Confidentiality
- Integrity
- Availability
if any of these properties are being violated, then it is a security vulnerability
### Authenticity
- Who are you
- are you truly yourself?
- where you see it
	- login forms
	- key-based auth
- don't confuse with authorization
	- are you allowed to do this?
### Confidentiality
- Is the information only know to the parties involved?
- Can no third party learn about it?
- where you see it
	- encrypted submission forms
	- secured connections
- Don't confuse with anonymity
	- nobody knows who you are!

### Integrity
- Is the data as it should be?
- Has the data remained unchanged?
- where you see it
	- read/write permissions
	- access controls
	- backup solutions
- when it is violated
	- ransomware attacks

### Availability/Dependability
- Can I still acces the data?
- Will the data be there when i need it?
- Availability violations
	- black friday (benign) (security violation, but it's not an attack)
	- Denial-of-Service (dos) attacks (malicious)

## Derived Properties
 - ACID
	 - Authenticity
	 - Confidentiality
	 - Integrity
	 - Availability
 - Derived
	 - Privacy
		 - you can have confidentiality without having privacy
		 - i.e.
			 - when doing a transaction with the bank, the bank still knows the credit card number, it's confidential to anyone else, but not private since the bank still knows
	 - Anonymity
	 - Non-repudiation
		 - Digital signatures, knowing that it for sure came from who it claims to have came from