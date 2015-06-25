This page explains the Python-AD installation.

## Prerequisites ##

Python-AD depends on the following software packages. These must be installed before Python-AD can be installed or used.

  * [Python](http://www.python.org/) >= 2.2.
  * [Python-LDAP](http://python-ldap.sourceforge.net/) >= ''unknown''
    * Support for paged results is required.
    * Ensure your OpenLDAP installation has support for SASL/GSSAPI. On Red Hat based distributions this means you need to install the `cyrus-sasl-gssapi` package.
  * [dnspython](http://www.dnspython.org/) >= ''unknown''. Used for looking up DNS SRV records.
  * [PLY](http://www.dabeaz.com/ply/) >= ''unknown''. PLY is used for parsing LDAP search filters.
  * [MIT Kerberos](http://web.mit.edu/Kerberos/) >= 1.3
    * Version 1.6 or higher, which implements [server-side canonicalisation](http://krbdev.mit.edu/rt/Ticket/Display.html?user=guest&pass=guest&id=2652), is greatly recommended.
  * [Nose](http://code.google.com/p/python-nose/) is used for running the unit tests.

## Installation ##

Because Python-AD uses distutils, installation is easy:

```
$ python setup.py build
$ python setup.py install
```

## Testing ##

Python-AD comes with an extensive test suite. To run the tests, you first need the `py.test` tool from the [py library](http://codespeak.net/py/dist/download.html). Follow the steps below to run the tests:

```
$ cp test.conf.example test.conf
$ vi test.conf
$ eval `python env.py`
$ python setup.py test
```

The file `test.conf` contains the test configuration. A lot of options are available for e.g. testing Python-AD against a real Active Directory. Please see inside this file for help on how to enable these tests.