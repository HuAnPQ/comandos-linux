# https://www.2daygeek.com/setup-nginx-server-blocks-virtual-hosts-in-linuxmint-ubuntu-debian/

# https://www.interserver.net/tips/kb/create-manage-virtual-hosts-nginx/

# Easy to configure compare with IP based
## Good for shared & reseller hosting environment

# 1a) Create Server Blocks (Virtual Hosts) 
sudo mkdir -p /var/www/support.2daygeek.com/public_html
sudo mkdir -p /var/www/dev.2daygeek.com/public_html

# 2a) Change the ownership permission
sudo chown -R username:username /var/www/support.2daygeek.com/public_html
sudo chown -R username:username /var/www/dev.2daygeek.com/public_html

# 3a) Setting-up Proper permission to www directory
sudo chmod -R 755 /var/www/

# 4a) Creating sample page for website’s
nano /var/www/support.2daygeek.com/public_html/index.html
# Example:
<html>
 <head>
 <title>New virtual host created successfully - support.2daygeek.com</title>
 </head>
 <body>
 <h1>New NGINX VirtualHost created successfully - support.2daygeek.com</h1>
 </body>
</html>

# 5a) Creating Virtual Host Files
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/support.2daygeek.com
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/dev.2daygeek.com

# 6a) Modify virtual host configuration
sudo nano /etc/nginx/sites-available/support.2daygeek.com
# Example:
#  Web root location & port listining
	server 
	{
        listen 80;
        root /var/www/support.2daygeek.com/public_html;
        index index.php index.html index.htm;
        server_name support.2daygeek.com;
        access_log /var/www/support.2daygeek.com/public_html/access.log;
        error_log /var/www/support.2daygeek.com/public_html/error.log;

#  Redirect server error pages to the static page
        location / 
	{
	try_files $uri $uri/ /index.php;
        }
        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;
        location = /50x.html 
	{
        root /var/www/support.2daygeek.com/public_html;
        }
	
#  Pass the PHP scripts to FastCGI server
	location ~ \.php$ 
	{
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        try_files $uri =404;
        fastcgi_pass 127.0.0.1:9000;
	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_index index.php;
        include fastcgi_params;
        }
	} 
# End Example

# 7a) Enabling Virtual Hosts
#  Enable Server Blocks (Virtual Hosts) 
sudo ln -s /etc/nginx/sites-available/support.2daygeek.com /etc/nginx/sites-enabled/support.2daygeek.com
sudo ln -s /etc/nginx/sites-available/dev.2daygeek.com /etc/nginx/sites-enabled/dev.2daygeek.com

# 8a) Run configtest
sudo nginx -t

# 9a) Reloading Nginx
sudo service nginx reload

# 10a) Restart Nginx
sudo service nginx restart

# 11a) Adding domain name to hosts file.
nano /etc/hosts
127.0.0.1    	localhost
10.0.2.15       support.2daygeek.com
10.0.2.15       dev.2daygeek.com

# 12a) Flush local DNS cache
/etc/init.d/dns-clean start

# 13a) Access newly setup website
http://support.2daygeek.com & http://dev.2daygeek.com
