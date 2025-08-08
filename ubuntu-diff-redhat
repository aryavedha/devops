Package Management :
Task	                 Ubuntu / Debian	        Red Hat / CentOS / Fedora
Install package	       apt install nginx	      yum install nginx (old)
                                                dnf install nginx (new)
Update package list	   apt update	              yum check-update /                                                               
                                                dnf check-update
Upgrade packages	     apt upgrade	            yum update / 
                                                dnf upgrade
Remove package	       apt remove nginx	        yum remove nginx / 
                                                dnf remove nginx
Package info	         apt show nginx	          yum info nginx / 
                                                dnf info nginx

Folder & File Locations :
Purpose	               Ubuntu/Debian	         Red Hat/CentOS
Config files	        /etc/ (same for both)	    /etc/ (same for both)
Apache config	        /etc/apache2/	            /etc/httpd/
Nginx config	        /etc/nginx/	              /etc/nginx/ (same)
Network config (new)  /etc/netplan/	            /etc/sysconfig/network-scripts/
Service scripts	      /etc/init.d/	            /etc/init.d/ (but often uses systemd units)
User home dirs	      /home/username	          /home/username (same)
Logs	                /var/log/	                /var/log/ (same)
Default web root      /var/www/html	            /var/www/html (same)

Service Management :
Both now use systemd, but Red Hat still has some legacy scripts.

Action	Command (Both) :
Start service	systemctl start nginx
Enable at boot	systemctl enable nginx
Check status	systemctl status nginx
Stop service	systemctl stop nginx

(Older RHEL used service nginx start) :

User & Group Management :
Task	           Ubuntu/Debian	            Red Hat/CentOS
Add user	       adduser john (friendly     useradd john (low-level)
Delete user	     deluser john	              userdel john
Change password	 passwd john	              passwd john (same)

Network & Firewall :
Task	                Ubuntu/Debian	                  Red Hat/CentOS
IP check	            ip a	                          ip a (same)
Ping	                ping google.com	                ping google.com (same)
Firewall	            ufw enable / ufw allow 80	      firewalld 
                                                      commands: firewall-cmd --add-port=80/tcp --permanent && firewall-cmd --reload

Root & Sudo :
Ubuntu: root login disabled by default; you use sudo.

RHEL: root login enabled by default during setup (but can disable).

In short :

Package manager is the main difference (apt vs yum/dnf).

Network configs and Apache folder names differ.

Service management is now mostly the same via systemctl.

Ubuntu feels more beginner-friendly, RHEL more enterprise-oriented.
