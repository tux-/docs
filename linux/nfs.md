Network File System
===================

Server
------

Check if nfs is installed:
```
sudo dpkg -l|grep nfs
```

Install nfs:
```
apt-get install nfs-kernel-server
```

Manage server shares:
```
vim /etc/exports
```

Share folder as read/write to a single ip:
```
/path/to/share     192.168.1.10(rw)
```

Reload the new added shares:
```
exportfs -ra
```


Client
------

```
apt-get install nfs-common
```

To see what folders a server is exporting:

```
showmount -e servername
```

To mount a remote drive
```
mount -t nfs servername:/path/to/share /mnt/localname/
```

To automatically mount, first do the normal mount, and then type ```mount``` to see the mounts. Values from here can be used to set up the auto mount.

```
vim /etc/fstab
```

```
servername:/path/to/share /mnt/localname/ nfs rsize=8192,wsize=8192
servername:/path/to/share /mnt/localname/ nfs ro,proto=tcp,local_lock=none,vers=4.0,rsize=32768,wsize=32768
```
