Remote Desktop
==============

Terminal Server
---------------

Great for file servers etc, where the client is not logged in.

```
apt-get install xrdp
```

xUbuntu Desktop Server
----------------------

Great for media center and such where you want to share the desktop session, and the client machine is logged in.

```
apt-get install vino
vino-preferences
```

Autostart: Settings -> Session and Startup -> Application Autostart -> Add:
```
Name: vino
Description: Remote Desktop Sharing
Command: /usr/lib/vino/vino-server
```


Client
------

Install Remmina Desktop Client
```
apt-get install remmina
```
