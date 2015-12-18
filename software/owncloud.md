ownCloud
========

Setup
-----

```bash
sudo vim /var/www/owncloud/config/config.php
# Set trusted domain, public url and datadir.
sudo service apache2 reload

# If already setup and you just want to change the datadir:
sudo mv /var/www/owncloud/data /media/disk/owncloud
sudo chown www-data. /media/disk/owncloud
sudo service apache2 reload
```
