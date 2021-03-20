# heroku-godaddy-setup

## At Heroku
- Main application: add domain including the "www" (www.example.com)
- Subdomains (other Heroku application): add domain excluding the "www" (api.example.com)
- For both of these applications take note of the given DNS Targets

## At GoDaddy
Add the following CNAME rows:
- Main application: "www" && the DNS Target (replace the default "@" row and its value)
- Subdomain: "*" && the DNS Target
- Set TTL at 600 seconds for testing, once in operation back to default (or not)
- Add forwarding at the bottom of the page: use the https protocol and provide the full domain name (www.example.com). Leave the other options as-is. 
 
## Now configure the SSL
- Go to https://punchsalad.com/ssl-certificate-generator/ to generate SSL keys. These keys are valid for 90 days and then have to be renewed, albeit for being free. Enter 3 domain names (seperated by comma): 1) example.com 2) www.example.com and 3) *.example.com for the subdomains. Then toggle the DNS option, and then generate the pub/priv keys.
- On the result page for each domain (main vs. wildcard) a Domain TXT record is given. Literally follow the instructions on that page (e.g. on GoDaddy add the TXT records), make sure the DNS is updated (by pressing "check DNS" on the page). Once done press "verify domain" and wait a few seconds for the changes to propagate.
- Open Heroku, and for both applications: Add Certificate > Import keys > select all domains. 


Everything should be fully setup now. It might be the case that the DNS Targets at the domain sections have changed after adding the SSL, if so: update your GoDaddy CNAME DNS Targets. To check if this all has worked its recommended to clear browser cache + open a CMD Prompt and enter `ipconfig/flushdns`






