Postfix
=======

Debugging
---------

```bash
echo "Test mail from postfix" | mail -s "Test Postfix" admin@example.com
```

See config
----------

```bash
postconf -n
```

```bash
/etc/postfix/main.cf
```

Configure
---------

```bash
dpkg-reconfigure postfix
```

Configure relay host
--------------------

```bash
postconf -e 'relayhost = smtp.example.com'
```

See logs
--------

```bash
tail -f /var/log/mail.log
```
