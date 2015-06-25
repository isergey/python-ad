Python-AD is an open source project release under the MIT license. You are invited to participate. Participating is not only limited to developers. There are many tasks you can do, such as:

  * Run Python-AD on a wide varieties of platforms and/or windows versions.
  * Improve or write the documents.
  * Report bugs


## Source Code Access ##

We use the Mercurial version control system. As Google Code does not provide support for this, we are using the excellent [freeHg](http://freehg.org/) service. The repository is located at

  * [http://freehg.org/u/geertj/python-ad](http://freehg.org/u/geertj/python-ad)

To check out the latest code, use:

```
  $ hg clone http://freehg.org/u/geertj/python-ad
```


## Mailing Lists ##

We use Google Groups for communication between users and developers. The group is located at

  * [python-ad group](http://groups.google.com/group/python-ad)

## Setting up your Development Environment ##

Before you can start developing on python-ad, you need to set up your development environment. You require at least the following tools:

  * [Nose](http://code.google.com/p/python-nose/) is used for testing. Python-AD is heaving using test driven development. New patches / features are not accepted unless there is a corresponding test case.
  * You will need an Active Directory domain to test your changes. Unfortunately this requires you to have a Windows server license. Unless you already have such a license, the most convenient way to get this is probably to buy yourself a  [MSDN Subscription](http://msdn.microsoft.com/en-us/subscriptions/default.aspx). There are multiple subscriptions available, but the cheapest one (the Operating System Subscription) already allows you download and run any Microsoft operating system for test and development purposes.
  * You will need an environment to install your Active Directory domain in. The recommended way is to use virtualization software (I would recommend KVM) to create multiple virtual machines on a single virtual network. The virtual network should provide no DNS / DHCP services as those are provided by AD. For convenience this network can be NAT'ed to the outside world. The best way to install your AD environment is to install at least two domain controllers so that you can test that scenario.