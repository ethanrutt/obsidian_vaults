- When an attacker intercepts valid communication and retransmits it
![[replay_attack.png]]
- [GFG Article](https://www.geeksforgeeks.org/replay-attack/)
- When a protocol is used where there are **no unique transaction IDs,** this can happen
	- Packets can be collected even if they don't know what is inside. So even if it's encrypted, it doesn't matter, all we are doing is sending the exact same packet that we intercepted
	- Sometimes this is paired with a man-in-the-middle attack
	- There is a case that you don't need a man-in-the-middle though, 
		- imagine an ATM. Whenever you send the request, it just performs the action.
			- Send the request to charge someone to the bank and put into my account
			- The ATM doesn't validate the transaction, so if I send the same one, it will do the same thing
# Mitigation
- utilize timestamps to enforce transaction expiration
- include unique transaction identifiers (i.e. nonces) (TCP/IP uses this to solve this problem)
-  implement message authentication codes (MAC) (use some kind of hashing with some of the other data)
	- i.e. hash the ip address, time, etc. 
	- when someone replays, the hash won't match because the time or ip address has changed, so it won't do the request
- Check out [[Authentication Flaws]]
- Find vulnerabilities [[Finding Vulnerabilities]]

#web