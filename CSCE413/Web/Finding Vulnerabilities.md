# Using Nmap to find vulnerabilities
- `nmap` is a powerful network scanning tool for identifying open ports, services, and potential vulnerabilities
- i.e.
```sh
nmap -A -T4 -Pn 111.111.11.11
```
-  This will tell you what ports are open on the ip address `111.111.11.11` as well as the server version and some other stuff
- other more high level tools that will find simple vulnerabilities
	- Nessus
	- OpenVAS
	- Nikto
- monitoring software for your own applications
	- Greenbone
- Advanced search using [[Google Dorks]]

#web #scanning #findingvulnerabilities #nmap