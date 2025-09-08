Steps to Install & Setup Nginx Server
1. Update system packages
```
sudo apt update -y && sudo apt upgrade -y
```
3. Install Nginx
```
sudo apt install nginx -y
```

4. Start and enable Nginx
```
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

Now, Nginx is running. You can check by visiting:
```
http://<your-ec2-public-ip>
```
4. Configure Firewall (if needed)

If using UFW:
```
sudo ufw allow 'Nginx HTTP'
sudo ufw allow 'Nginx HTTPS'
sudo ufw reload
```

If AWS EC2 Security Group → allow inbound traffic for port 80 (HTTP) and 443 (HTTPS).

5. Configure Nginx Server Block (like VirtualHost in Apache)

Let’s say you want to host a site at /var/www/myapp.
```
sudo mkdir -p /var/www/myapp
sudo chown -R $USER:$USER /var/www/myapp
```

Create a sample index.html:
```
echo '<h1>Welcome to My Nginx Server</h1>' | sudo tee /var/www/myapp/index.html
```

Now create config file:
```
sudo nano /etc/nginx/sites-available/myapp
```

Add:
```
server {
    listen 80;
    server_name IP paste;
    root /var/www/myapp;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Enable site:
```
sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

6.Add records in godady website
Steps to Add Records in GoDaddy
A). Log in

Go to GoDaddy login
.

Open your Domain Manager.

B). Open DNS Management

Click on your domain (e.g., yourdomain.com).

Look for DNS or Manage DNS.

C). Add Records

You usually need at least 2 records:

A Record (Root Domain)

Type: A

Name: @

Value: Your server’s public IP (from AWS EC2, etc.)

TTL: 600 seconds (or default)

This makes yourdomain.com point to your server.

CNAME Record (www Subdomain)

Type: CNAME

Name: www

Value: @ (or yourdomain.com)

TTL: Default

This makes www.yourdomain.com point to yourdomain.com.

D). (Optional) Wildcard Subdomain

If you want all subdomains (like app.yourdomain.com, blog.yourdomain.com) to point to your server:

Type: CNAME

Name: *

Value: @

TTL: Default

E). Save & Wait

Click Save after adding records.

DNS propagation can take 5 min to 48 hours (usually <1 hour).

F). Verify

After waiting a few minutes, check:
```
dig yourdomain.com
dig www.yourdomain.com
```

Or online tool: whatsmydns.net


7. (Optional) Enable HTTPS with Let’s Encrypt
If you have a domain pointing to your server:
install Certbot + Nginx plugin

```
sudo apt install certbot python3-certbot-nginx -y
```
get free SSL certificate + auto-configure Nginx
```
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```


Done! Your Nginx server is ready

---
Extra info:
1. What is Certbot?

Certbot is a tool from the EFF (Electronic Frontier Foundation) that helps you automatically get SSL/TLS certificates from Let’s Encrypt (a free certificate authority).

It also helps configure your web server (like Nginx or Apache) to use HTTPS.

2. Command: Install Certbot
```
sudo apt install certbot python3-certbot-nginx -y
```

certbot → main program for certificate management.

python3-certbot-nginx → plugin that allows Certbot to automatically configure Nginx with HTTPS after getting the certificate.

-y → auto-yes to install.

After this, Certbot is installed on your server.

3. Command: Request Certificate
```
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

This does two things:

Requests a certificate from Let’s Encrypt for the domain names you specify (-d yourdomain.com and -d www.yourdomain.com).

Certbot must be able to reach your domain → so your DNS must point to your server’s public IP.

Configures Nginx automatically to use the certificate (adds SSL block in /etc/nginx/sites-enabled/...).

4. What happens behind the scenes

Certbot proves you own the domain by serving a temporary file via Nginx or DNS (ACME challenge).

If successful, Let’s Encrypt issues a free certificate.

Certbot saves certificates in /etc/letsencrypt/live/yourdomain.com/.

Certbot modifies your Nginx config so your site runs on HTTPS (port 443).

It also sets up auto-renewal (via systemd timer or cron job).

5. Example Nginx Config After Certbot

Before (HTTP only):
```
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    root /var/www/myapp;
}
```

After (Certbot modified):
```
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name yourdomain.com www.yourdomain.com;

    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;

    root /var/www/myapp;
}

```
