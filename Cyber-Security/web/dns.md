# DNS

Simple way of communicating with devices on the internet without remembering complex IP addresses

## Domain Hierarchy

### TLD (Top-Level Domain)

- The most righthand part of a domain name: .com, .bg, .edu, .ru, ...

There are two types of TLD:
| gTLD (Generic Top Level Domain) | ccTLD (Country Code Top Level Domain) |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| tells the domain name's purpose (.edu for education, .org for organisations, ...). | used for geographical purposes (.ca for Canada-based sites, .bg for Bulgaria-based, ...). |

- Link for [over 2000 TLDs](https://data.iana.org/TLD/tlds-alpha-by-domain.txt).

### Second-Level Domain

Example: tryhackme.com, shkolo.bg, nasa.gov

- The text before the "." is the second-level domain.

- Limit: 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

### Subdomain

A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it.

Example: admin.tryhackme.com

- "admin" is the subdomain

It has the same restrictions as the Second-Level Domain.</br>
limited to 63 characters and can only use a-z 0-9 and hyphens</br> (cannot start or end with hyphens or have consecutive hyphens)
You can use multiple subdomains split with periods to create longer names, such as jupiter.servers.tryhackme.com.

- The length must be kept to 253 characters or less.
- There is no limit to the number of subdomains you can create for your domain name.
