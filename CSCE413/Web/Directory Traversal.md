- Scenario
	- vulnerable file download endpoint
	- `GET /download?file=../../../../etc/shadow`
- Result
	- attacker can access hashed password entries from the `/etc/shadow` file
- Mitigation
	- To restrict file access to `/var/www/html`
	- Edit apache config file `<Directory> "/var/www/html"> Options -Indexes`
	- Set document root in apache
	- Restart apache to apply changes `sudo systemctl restart apache`

- Setup server that just serves requests with no file checking 
- can use netcat to send requests
- use `GET yes.html` to get legitimate files that we are supposed to get
- use `GET ../no.html` to get files in the filesystem that we are not supposed to be able to access using `../` syntax

## Web Vulnerabilities in Practice
- Use web vulnerability scanners
- Embedding sites inside another website
- happens in practice
- [Prof Report](https://arxiv.org/abs/2109.06068)
## Google Dorks
- Google indexes the entire internet including vulnerable pages
- How to find vulnerabilities
	- i.e.
		- `intitle: "index of" "parent directory" "ftp"` - searches for FTP directories (means anyone can access Filesystem)
		- `inurl: "admin" filetype:php` - Searches for PHP admin pages
		- `inurl: "wp-config.php"` - wordpress config files
		- `filetype:sql "password"` - sql files with exposed passwords
		- `inurl:"/viewsource/"` - Searches for vulnerable pages with exposed source code
	- Choose relevant search term for your target
	- use advanced search operators `intitle`, `inurl`, `filetype`, `intext`
- See [[Google Dorks]] for more in depth explanation
- Check out this resource [Google Dorking CheatSheet](https://github.com/chr3st5an/Google-Dorking)

#web #googledorks