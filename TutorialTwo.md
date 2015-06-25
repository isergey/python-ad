# Tutorial Two #

This tutorial demonstrates how to search the global catalog. Querying the global catalog is almost identical to querying a normal LDAP server: the difference is that to query a global catalog we pass the `scheme='gc'` parameter to `search()`.

The example below also demonstrates how to load credentials from the operating system. This is done by calling `creds.load()` below. As you can see we do not need to supply a principal name or a password to this call. It does require though that you have a valid Kerberos ticket in your ticket cache.

```
from ad import Client, Creds, activate

domain = 'freeadi.org'

creds = Creds(domain)
creds.load()
activate(creds)

client = Client(domain)
users = client.search('(objectClass=user)', scheme='gc')
for dn,attrs in users:
    name = attrs['sAMAccountName'][0]
    domain = client.domain_name_from_dn(dn)
    print '-> %s (%s)' % (name, domain)
```

Go back to PythonAdTutorial