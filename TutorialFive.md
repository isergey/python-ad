# Tutorial Five #

This tutorial demonstrates how to create a new user in Active Directory. Adding objects to AD can be done with the `add()` method of the AD client. However this by itself is not enough: AD will not allow you to create an account without a password. The solution is to create the account in the disabled state first, then set a password, and finally enable the account. This is illustrated below:

```
import sys
from ad import Client, Creds, Locator, activate
from ad import AD_USERCTRL_NORMAL_ACCOUNT, AD_USERCTRL_ACCOUNT_DISABLED

domain = 'freeadi.org'
user = 'Administrator'
password = 'Pass123'

if len(sys.argv) != 3:
    sys.stderr.write('Usage: useradd <username> <password>\n')
    sys.exit(1)
username = sys.argv[1]
userpass = sys.argv[2]

creds = Creds(domain)
creds.acquire(user, password)
activate(creds)

client = Client(domain)
result = client.search('(sAMAccountName=%s)' % username)
if len(result) > 0:
    sys.stderr.write('Error: user %s already exists\n' % username)
    sys.exit(1)

dn = 'cn=%s,cn=users,%s' % (username, client.dn_from_domain_name(domain))
attrs = []
attrs.append(('cn', [username]))
attrs.append(('sAMAccountName', [username]))
princ = '%s@%s' % (username, domain)
attrs.append(('userPrincipalName', [princ]))
ctrl = AD_USERCTRL_NORMAL_ACCOUNT | AD_USERCTRL_ACCOUNT_DISABLED
attrs.append(('userAccountControl', [str(ctrl)]))
attrs.append(('objectClass', ['user']))
client.add(dn, attrs)

client.set_password(princ, userpass)

mods = []
ctrl = AD_USERCTRL_NORMAL_ACCOUNT
mods.append(('replace', 'userAccountControl', [str(ctrl)]))
client.modify(dn, mods)
```

Go back to PythonAdTutorial