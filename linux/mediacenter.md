Media Center
============

See [Remote Desktop](remotedesktop.md) for setting up remote desktop.

See [Network File Sharing](nfs.md) for setting up connections to file server.

See [Give yourself ssh access without password](ssh.md) for getting password free access.

Install the media center software
---------------------------------

```
sudo apt-get install kodi
```

Install the chrome extension
----------------------------

[Play to kodi](https://chrome.google.com/webstore/detail/play-to-kodi/fncjhcjfnnooidlkijollckpakkebden?hl=en).


Make a simple controller
------------------------

```
apt-get install wakeonlan ssvnc
```

```
ssh media-center.local
ifconfig
```

Note the HWaddr of the WOL network card. And log off the media center.

```
vim /usr/bin/mediacenter
```

```
HWaddr="c0:3f:d5:6a:ef:00"
NetworkName="media-center.local"

action=$(zenity --list \
--height 210 \
--title="Media Center" \
--column "Action" \
'Power on' \
Control \
Reboot \
'Power off')
if [ $? == 1 ]; then exit; fi

if [ "${action}" = "Power on" ]; then
	wakeonlan ${HWaddr};
elif [ "${action}" = "Control" ]; then
	ssvnc -noenc ${NetworkName};
elif [ "${action}" = "Reboot" ]; then
	ssh ${NetworkName} 'sudo reboot'
elif [ "${action}" = "Power off" ]; then
	ssh ${NetworkName} 'sudo shutdown -P now'
fi
```

```
chmod +x /usr/bin/mediacenter
```


Add the controller to a panel
-----------------------------
