Users
=====

Give yourself password less sudo access
---------------------------------------

```
sudo visudo
```

For all members of users:
```
%users  ALL=(ALL:ALL) NOPASSWD: ALL
```

For specific user:
```
username ALL=(ALL:ALL) NOPASSWD: ALL
```
