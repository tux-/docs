nginx
=====

Example configuration for development
-------------------------------------
Replace username below:
```
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	server_name domain.name;

	location ~ ^(.*?)index\.php$ {
		fastcgi_pass unix:/var/run/php5-fpm.sock;
		fastcgi_index index.php;
		fastcgi_param SCRIPT_FILENAME $sitedir/index.php;
		fastcgi_param PATH_INFO $pathinfo;
		include fastcgi_params;

	}
	location ~ ^/([^/]+)/admin/(.*)$ {
		set $sitedir /home/username/development/web/sites/admin/public;
		set $pathinfo $2;
		root $sitedir;
		index index.html index.php;
		try_files /$2 /index.php;
	}
	location ~ ^/([^/]+)/(.*)$ {
		set $sitedir /home/username/development/web/sites/$1/public;
		set $pathinfo $2;
		root $sitedir;
		index index.html index.php;
		try_files /$2 /index.html /index.php;
	}
}
```
