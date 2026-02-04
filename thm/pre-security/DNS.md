# Pre-Security / DNS

## What is DNS (Domain Name System) - simple way to communicate with devices on the internet without remembering complex numbers. Used insead of IP (4 sets of digits from 0-255 separated by a period)


## 
- TLD (Top-Level Domain) - most righthand part of a domain name, for example ".com".
- Second-Level Domain - domain name imited to 63 characters + the TLD and can only use a-z 0-9 and hyphens.
- Subdomain - A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it.
## Record
- A: IPv4 - for example 104.26.10.229
- AAAA: IPv6 - for example 2606:4700:20::681a:be5
- CNAME: alias - These records resolve to another domain name
- MX: These records resolve to the address of the servers that handle the email for the domain you are querying
- TXT: TXT records are free text fields where any text-based data can be stored
- NS: serwery nazw

## DNS request
Client → Recursive Resolver → Authoritative → answer → cache (Time To Life)

## Tools
- nslookup / dig

## 5 Common Problems
1) Bad Record / Wrong Type
2) Cache and TTL
3) No Propagation / Old Resolver
4) Bad CNAME (Loop)
5) Bad NS / Delegation
