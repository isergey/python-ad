# Tutorial Four #

This tutorial demonstrates how to search the rootDSE of a domain controller. The following things are important when querying the rootDSE

  * You indicate you want to search the rootDSE by setting the `base` argument to `''` (the empty string).
  * The `scope` argument needs to be `'base'`, anything else will not work.
  * You must give a `server=xxx` argument to specify which server's rootDSE you want to query (rootDSE's are not replicated and so each domain controller has its own copy).

```
from ad import Client, Creds, Locator, activate

domain = 'freeadi.org'
user = 'Administrator'
password = 'Pass123'

levels = \
{
    '0': 'windows 2000',
    '1': 'windows 2003 interim',
    '2': 'windows 2003'
}

creds = Creds(domain)
creds.acquire(user, password)
activate(creds)

locator = Locator()
server = locator.locate(domain)

client = Client(domain)
result = client.search(base='', scope='base', server=server)
assert len(result) == 1
dn, attrs = result[0]
level = attrs['forestFunctionality'][0]
level = levels.get(level, 'unknown')
print 'Forest functionality level: %s' % level
```

Go back to PythonAdTutorial