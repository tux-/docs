ssh
===

Some variable names used in this file:

* ```sshtarget``` The remove machine that you ssh to.
* ```sshalias``` A local alias name for the ssh target.
* ```luser``` Your local user name.
* ```ruser``` Your remote user name.
* ```iserver``` An internal server on a remote network.
* ```iuser``` User name on the internal remoter server.

Install ssh
-----------

```bash
apt-get install ssh
```

Give yourself ssh access without password
-----------------------------------------

```bash
cd
ssh-keygen
# Enter on all questions (use default value).
scp .ssh/id_rsa.pub sshtarget:/home/ruser/mykey.key
ssh sshtarget
cat mykey.key >> .ssh/authorized_keys
# If the file does not exist, just move the uploaded file there
mv mykey.key .ssh/authorized_keys
# If the file existed, clean up the uploaded file
rm mykey.key
```


Configure connect to remote machine with custom settings
--------------------------------------------------------

```bash
vim .ssh/config
# Add the following lines:
host sshalias
user ruser
hostname sshtarget
GSSAPIAuthentication=no
```


Ssh to remote and execute command
---------------------------------
```bash
ssh sshalias "touch /tmp/sshtest"
```


Getting access to a webserver on an internal net
------------------------------------------------
```bash
ssh -L 8080:iserver:80 sshalias
```

This can also be run in the background by adding:
```bash
-f -N
# Remember to kill it when done:
ps -ax|grep iserver
# find the pid and kill it.
kill -9 pid
```


Mounting a filesystem on a server on another network
----------------------------------------------------
```bash
vim .ssh/config
# Add the following:
host iserver
user iuser
ProxyCommand ssh sshalias "nc -q 1 %h %p"

# Create the mount point:
sudo mkdir /mnt/iserver/
sudo chown luser. /mnt/iserver/
# You can then use sshfs to mount like this:
sshfs iserver:/home/iuser/ /mnt/iserver/
```


Forward X output from one computer to another
---------------------------------------------
```bash
ssh -t sshalias ssh -X yourremotemachinename
```

Forward X output from a machine behind a router
-----------------------------------------------
You need two terminals:
```bash
Terminal 1: ssh -N -L 9997:yourremotemachinename:22 yourusernameonremoterouter@remoteipaddress
Terminal 2: ssh -p 9997 -Xv remoteusernameonyoulocalmachine@localhost
```
