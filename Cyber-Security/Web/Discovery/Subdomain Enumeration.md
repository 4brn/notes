## SSL/TLS Certificates

When an SSL/TLS (Secure Sockets Layer/Transport Layer Security) certificate is created for a domain by a CA (Certificate Authority), CA's take part in what's called "Certificate Transparency (CT) logs". These are publicly accessible logs of every SSL/TLS certificate created for a domain name. The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used.

- [https://crt.sh](http://crt.sh/) and [https://ui.ctsearch.entrust.com/ui/ctsearchui](https://ui.ctsearch.entrust.com/ui/ctsearchui) offer a searchable database of certificates that shows current and historical results.

## OSINT

- Search Engines 
- [Sublist3r](https://github.com/aboul3la/Sublist3r)

## DNS Bruteforce

Bruteforce DNS enumeration is the method of trying many different possible subdomains from a pre-defined list.
- [dnsrecon](https://www.kali.org/tools/dnsrecon/)

## Virtual Hosts

Subdomains aren't always hosted in publically DNS results. They could be kept on a private DNS server or the developers machine (/etc/hosts 
OR c:\windows\system32\drivers\etc\hosts file).

Because web servers can host multiple websites from one server when a website is requested from a client, the server knows which website the client wants from the **Host** header. We can utilise this host header by making changes to it and monitoring the response to see if we've discovered a new website.
