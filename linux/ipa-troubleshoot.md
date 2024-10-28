# troubleshoot ipa

check all ipa services:

```
ipactl status
```

check all expired certificates:

```
ipa-healthcheck --source=ipahealthcheck.ipa.certs --failures-only
```

find cert:

```
sudo ipa cert-find
```

get help:

```
ipa help commands | grep find
```

restart ipa:

```
systemctl restart ipa
```

```
ipa --version
```

```
ipactl status
```

```
ipa-healthcheck --source=ipahealthcheck.ipa.certs --failures-only
```

```
sudo ipa cert-find
```

```
openssl x509 -noout -text -in ca.pem
```

sudo

```
ipa-healthcheck
```

/var/log/ipa/healthcheck/

```
ipa-healthcheck --source=ipahealthcheck.meta.services --failures-only
```

cat /etc/sysconfig/network

```
ipa sudorule-find
```

```
less /var/log/sssd/
```

```
ipa sudorule-show
```

checkni ci berie sudo policy z tadeto

```
cat /etc/nsswitch.conf
```

checkni ci tam je tento file

```
~/.ipa/log/cli.log
```

```
ls -l /var/log/sssd/
```

check files sssd_domain, sssd_nss.log, sssd_pam.log

debug logy zmen
/etc/sssd/sssd.conf
systemctl restart sssd

restart timto dole:

```
systemctl restart dirsrv@REALM-NAME.service
```

```
systemctl restart ipa
```

```
ipa topologysuffix-find
```

```
ipa topologysegment-find
```

```
ipa config-show
```

```
ipa server-show
```

```
man ipa-healthcheck
```

```
ipa-healthcheck --list-sources
```

```
ipa-healthcheck --source=ipahealthcheck.ipa.certs --failures-only
```

pherhaps enable compact tree:

```
ipa-compat-manage enable
```

/var/log/dirsrv/slapd-REALM_NAME/errors

```
ipa-replica-manage list -v
```

```
ipa-replica-manage list -v servername
```

```
ipa-replica-manage force-sync --from [server1.example.com](http://server1.example.com/)
```

```
ipa-replica-manage re-initialize --from [server1.example.com](http://server1.example.com/)
```

```
ipa topologysegment-find
```

ipa-healthcheck --source=ipahealthcheck.meta.services

```
ipa-healthcheck --source=[ipahealthcheck.dogtag.ca](http://ipahealthcheck.dogtag.ca/)
ipa-healthcheck --source=ipahealthcheck.ds.backends
ipa-healthcheck --source=ipahealthcheck.ds.config
ipa-healthcheck --source=ipahealthcheck.ds.disk_space
ipa-healthcheck --source=ipahealthcheck.ds.dse
ipa-healthcheck --source=ipahealthcheck.ds.encryption
ipa-healthcheck --source=ipahealthcheck.ds.fs_checks
ipa-healthcheck --source=ipahealthcheck.ds.nss_ssl
ipa-healthcheck --source=ipahealthcheck.ds.ds_plugins
ipa-healthcheck --source=ipahealthcheck.ds.replication
ipa-healthcheck --source=ipahealthcheck.ds.ruv
ipa-healthcheck --source=ipahealthcheck.ipa.certs
ipa-healthcheck --source=ipahealthcheck.ipa.dna
ipa-healthcheck --source=ipahealthcheck.ipa.idns
ipa-healthcheck --source=ipahealthcheck.ipa.files
ipa-healthcheck --source=ipahealthcheck.ipa.host
ipa-healthcheck --source=ipahealthcheck.ipa.meta
ipa-healthcheck --source=ipahealthcheck.ipa.roles
ipa-healthcheck --source=ipahealthcheck.ipa.topology
ipa-healthcheck --source=ipahealthcheck.ipa.trust
ipa-healthcheck --source=ipahealthcheck.meta.core
ipa-healthcheck --source=ipahealthcheck.meta.services
ipa-healthcheck --source=ipahealthcheck.system.filesystemspace
```

/var/log/dirsrv/slapd-REALM_NAME/errors

kerberos/ldap certificate change