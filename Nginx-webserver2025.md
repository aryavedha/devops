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
    server_name _;
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
6. (Optional) Enable HTTPS with Let’s Encrypt

If you have a domain pointing to your server:
```
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```


Done! Your Nginx server is ready
