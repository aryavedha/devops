
- In practice, when people say "SSL certificate", they actually mean TLS certificate. The term "SSL" just stuck around historically
- SSL = old, broken.
- TLS = modern, secure.
- Handshake = trust + key exchange + encryption setup

---

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
- A daemon is a background service or process that performs specific tasks automatically
- A daemon is simply a background service that keeps your DevOps tools and automation workflows alive and responsive
---
What is PCI patching in DevOps?

PCI patching refers to the process of keeping systems, applications, and dependencies up-to-date with security patches to meet PCI DSS (Payment Card Industry Data Security Standard) requirements — especially for any infrastructure that handles cardholder data (CHD) or sensitive authentication data (SAD).

In DevOps terms — it’s automated, continuous, and auditable patch management built into your CI/CD and infrastructure pipelines

PCI patching in DevOps = automating OS, dependency, and container security updates within 30 days of release, validating via scanning, and storing logs as audit evidence

---
