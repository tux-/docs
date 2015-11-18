apache2
=======

Example configuration for development
-------------------------------------
Replace username below:
```
<VirtualHost *:80>
	#ServerName www.example.com

	<IfModule mpm_itk_module>
		AssignUserId www-data users
	</IfModule>

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html

	RewriteEngine On
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_URI} !^/icons/.*
	RewriteRule ^/([^/]+/)(.*) /home/username/development/web/sites/$1public/$2 [QSA,L]

	<Directory /home/username/development/web/sites>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Order allow,deny
		Allow from all

		RewriteEngine On
		RewriteCond %{REQUEST_FILENAME} !-f
		RewriteCond %{REQUEST_FILENAME} !-d
		RewriteRule ^([^/]+/)([^/]+/)(.*)$ /$1index.php/$3 [QSA,L]
	</Directory>

	<Directory /usr/share/apache2/icons>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Order allow,deny
		Allow from all
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```
