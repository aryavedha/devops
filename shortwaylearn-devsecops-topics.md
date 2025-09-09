- Ingress = rules for traffic routing
- Ingress Controller = the actual “traffic cop” that enforces those rules
---
- S3 = good for object storage, logs, backups, static assets.
- EFS/FSx = better if you need multiple instances to mount and share files like a normal disk
---
- DNS provider (e.g., GoDaddy, Route53, Cloudflare)
- DNS = Converts domain names into IP addresses through a hierarchy of servers
- 
Suppose you type:
```
blog.yourdomain.com
```

- DNS flow:

Browser → OS → DNS Resolver → Root → .com TLD → Authoritative NS.

Authoritative NS says:
```
blog.yourdomain.com → 203.0.113.25
```

Browser then opens connection to 203.0.113.25

- DNS Record Types (Common Ones)

A record → Domain → IPv4 address

AAAA record → Domain → IPv6 address

CNAME record → Alias → Another domain

MX record → Mail server for your domain

TXT record → Extra info (SPF, DKIM, verification)

NS record → Nameservers (pointing to authoritative DNS servers)

---
