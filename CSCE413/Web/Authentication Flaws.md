- leaking sensitive user info through query parameters
- `https://example.com/profile?user_id=1234` might be your own
- `https://example.com/profile?user_id=5678` might be another students, and just by modifying URL you can access it if they have poor security
- Levels of Auth
	- i.e.
		- People not in tamu can't access tamu canvas
		- but tamu students can access
			- inside canvas there are also more levels
				- i.e.
					- I can't grade my own work or access professor resources
	- In [[Replay Attacks]] these work when both the sender and the replayer have the same authentication or privilege
# Mitigation
- **Server-side** access control
- Avoid exposing sensitive data in URL's
- The more that you let the user enter information, the more insecure your system is and the more control they have. 
- Use session tokens for authentication instead of query parameters
	- unique tokens for each user
- Scan with [[Finding Vulnerabilities]]

#web #auth