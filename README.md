# WinSrv-Centos-Fix
Since June30, 2024 Centos 7 has been EOL or "end of life". For this reason, and for reasons of corporate laziness, all of the Centos Yum package mirrors have been moved to different servers, hosted by kind hackers, and not Red Hat. Below are modifications addressing this issue for the inctructions at [redhat.com](https://www.redhat.com/sysadmin/linux-active-directory).

## Before "Packages to install" section (Run in Linux terminal):

```sudo nano /etc/yum.repos.d/CentOS-Vault.repo```  To open an editor

Type your root (administrator) password to successfuly execute the above sudo command

Paste in the following:
```
[base]
name=CentOS-7 - Base
baseurl=https://vault.centos.org/7.9.2009/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[updates]
name=CentOS-7 - Updates
baseurl=https://vault.centos.org/7.9.2009/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[extras]
name=CentOS-7 - Extras
baseurl=https://vault.centos.org/7.9.2009/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```

Then press Ctrl+X and Enter to save the file

Next run the following commands:
```
sudo yum clean all
sudo yum makecache
sudo yum update
```

