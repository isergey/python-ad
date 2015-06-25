# Tutorial Three #

The example below demonstrates how to query a specific server in a domain. Normally Python-AD uses ''serverless binding'', which means that Python-AD will select a suitable domain controller for you automatically. Sometimes this is not desirable and you want to target a specific domain controller instead. The example below implements the search user functionality again, but now it specifically targets the domain controller with the PDC emulator role.

```
from ad import Client, Creds, Locator, activate

domain = 'freeadi.org'
user = 'Administrator'
password = 'Pass123'

creds = Creds(domain)
creds.acquire(user, password)
activate(creds)

locator = Locator()
pdc = locator.locate(domain, role='pdc')

client = Client(domain)
users = client.search('(objectClass=user)', server=pdc)
for dn,attrs in users:
    name = attrs['sAMAccountName'][0]
    print '-> %s' % name
```

Go back to PythonAdTutorial