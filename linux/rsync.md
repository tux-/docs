rsync
=====

Example 1
---------

rsync all files except hidden from local to remote over ssh.

```bash
rsync -e ssh --delete --exclude '.*' -rltv /localdir/ user@server:/remotedir/
```
