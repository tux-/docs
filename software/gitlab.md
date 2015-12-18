gitlab
======

Setup
-----

### Gitlab config ###

```bash
sudo vim /etc/gitlab/gitlab.rb
```

```rb
external_url 'http://gitlab.domain.tld:4554'
git_data_dir '/media/disk/gitlab'
unicorn['worker_timeout'] = 600
web_server['external_users'] = ['www-data']
nginx['enable'] = false
```

```bash
sudo gitlab-ctl reconfigure
```

### Apache config ###

Remember to enable all three required modules described in the config below.

```
# This configuration has been tested on GitLab 8.0.0
# Note this config assumes unicorn is listening on default port 8080 and gitlab-git-http-server is listening on port 8181.
# To allow gitlab-git-http-server to listen on port 8181, edit or create /etc/default/gitlab and change or add the following:
# gitlab_git_http_server_options="-listenUmask 0 -listenNetwork tcp -listenAddr localhost:8181 -authBackend http://127.0.0.1:8080"

#Module dependencies
#  mod_rewrite
#  mod_proxy
#  mod_proxy_http
<VirtualHost *:80>
	ServerName gitlab.domain.tld
	ServerSignature Off

	ProxyPreserveHost On

	# Ensure that encoded slashes are not decoded but left in their encoded state.
	# http://doc.gitlab.com/ce/api/projects.html#get-single-project
	AllowEncodedSlashes NoDecode

	<Location />
		# New authorization commands for apache 2.4 and up
		# http://httpd.apache.org/docs/2.4/upgrading.html#access
		Require all granted

		#Allow forwarding to gitlab-git-http-server
		#ProxyPassReverse http://127.0.0.1:8181
		#Allow forwarding to GitLab Rails app (Unicorn)
		#ProxyPassReverse http://127.0.0.1:8080
		ProxyPassReverse http://gitlab.domain.tld:4554/
	</Location>

	#apache equivalent of nginx try files
	# http://serverfault.com/questions/290784/what-is-apaches-equivalent-of-nginxs-try-files
	# http://stackoverflow.com/questions/10954516/apache2-proxypass-for-rails-app-gitlab
	RewriteEngine on
	#Forward these requests to gitlab-git-http-server
	RewriteCond %{REQUEST_URI} ^/[\w\.-]+/[\w\.-]+/repository/archive.* [OR]
	RewriteCond %{REQUEST_URI} ^/api/v3/projects/.*/repository/archive.* [OR]
	RewriteCond %{REQUEST_URI} ^/[\w\.-]+/[\w\.-]+/(info/refs|git-upload-pack|git-receive-pack)$
	RewriteRule .* http://127.0.0.1:8181%{REQUEST_URI} [P,QSA]

	#Forward any other requests to GitLab Rails app (Unicorn)
	RewriteCond %{DOCUMENT_ROOT}/%{REQUEST_FILENAME} !-f [OR]
	RewriteCond %{REQUEST_URI} ^/uploads
	RewriteRule .* http://127.0.0.1:8080%{REQUEST_URI} [P,QSA,NE]

	# needed for downloading attachments
	DocumentRoot /opt/gitlab/embedded/service/gitlab-rails/public

	#Set up apache error documents, if back end goes down (i.e. 503 error) then a maintenance/deploy page is thrown up.
	ErrorDocument 404 /404.html
	ErrorDocument 422 /422.html
	ErrorDocument 500 /500.html
	ErrorDocument 503 /deploy.html

	# It is assumed that the log directory is in /var/log/httpd.
	# For Debian distributions you might want to change this to
	# /var/log/apache2.
	LogFormat "%{X-Forwarded-For}i %l %u %t \"%r\" %>s %b" common_forwarded
	ErrorLog  /var/log/apache2/gitlab.domain.tld_error.log
#  CustomLog /var/log/httpd/logs/gitlab.example.com_forwarded.log common_forwarded
#  CustomLog /var/log/httpd/logs/gitlab.example.com_access.log combined env=!dontlog
#  CustomLog /var/log/httpd/logs/gitlab.example.com.log combined

</VirtualHost>
```
