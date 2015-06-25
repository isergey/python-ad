# Tutorial One #

The code fragment below demonstrates how to search for users in an Active Directory domain. It show the basic usage of Python-AD: how acquire credentials and how to user the AD client interface.

```
from ad import Client, Creds, activate

domain = 'freeadi.org'
user = 'Administrator'
password = 'Pass123'

creds = Creds(domain)
creds.acquire(user, password)
activate(creds)

client = Client(domain)
users = client.search('(objectClass=user)')
for dn,attrs in users:
    name = attrs['sAMAccountName'][0]
    print '-> %s' % name
```

Go back to PythonAdTutorial