
Parent: [[011 OSI Model Layers]]
Subject/Topics: 
Hashtags: #layers #layer/7 #OSI #networking 
Date: 05-01-2023

# Notes:

Layer in which *protocols* and rules are set to determine *how the user should interact* with data sent or received

- GUI (Graphical User Interface)
- DNS (Domain Name System)

## DNS Record Types

DNS isn't just for websites though. 
There are multiple types of DNS records.

### List of most common DNS Record Types:
#### A 
Resolves to IPV4 addresses
	104.26.10.229
#### AAAA 
Resolving to IPV6 addresses
	2606:4700:20::681a:be5
#### CNAME 
Resolves to another domain name
	store.tryhackme.com returns a CNAME record shops.shopify.com
#### MX
Resolves to the address of the servers that handle the email for the queryed domain.
	tryhackme.com -> alt1.aspmx.l.google.com
#### TXT
text-based data
	- list of servers that have the authority to send an email on behalf of the domain.
	- Verify the ownership of the domain name when signing up for third party services


## DNS Request

What happens when you make a DNS request:

1. When requested a domain name, the computer checks its *local cache*, whether the address has been looked up recently. If *not*,  a request to a *Recursive DNS Server* will be made.

2. The server has its own local cache of recently looked up names.  If the request cannot be found locally, it is searched from other DNS servers starting with the Internets's root DNS servers.