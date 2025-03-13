# WinSrv-Centos-Fix
Since June 30, 2024 Centos 7 has been EOL or "end of life". For this reason, and for reasons of corporate laziness, all of the Centos Yum package mirrors have been moved to different servers, hosted by kind hackers, and not Red Hat. Below are modifications addressing this issue for the inctructions at [redhat.com](https://www.redhat.com/sysadmin/linux-active-directory).

If you are not enrolled in the Admin Windows Server Class at Kirkwood, this repo may not be right for you.

## Before "Packages to install" section (Run in Linux terminal):

```sudo nano /etc/yum.repos.d/CentOS-Vault.repo```  To open an editor.
(Or, if you do not have nano installed / do not want to use nano, replace 'nano' with 'vi'. Beware that vi has unintuitive keybinds.

Type your root (administrator) password to successfuly execute the above sudo command, and press enter.

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

Then press Ctrl+X and Enter to save the file.

Next run the following commands:
```
sudo yum clean all
sudo yum makecache
sudo yum update
```

Note: If using the exact Centos 7 version that Professor Lampe specified, the above source specification is the correct config. Otherwise you can check the version you've installed and adjust the version numbers accordingly with any of the following commands. (Do not confuse Linux kernel version with Centos version):
````cat /etc/*elease````
```hostnamectl```

Congratulations, you have just removed and added a repository source to your Linux package manager. Modifying and adding sources is a common task for intermediate-level linux tasks, especially for distros like Debian/Ubuntu or Centos/RHEL. Learning how package managers work is a vital part of your Linux journey. 

## Alternative method:
Centos is a linux distro that has been discontinued by RedHat. It is always wise to avoid old liux distros that have dropped support, for security reasons as well as package update reasons (you probably want new versions of most programs). Centos Stream is the new distro which serves as the upstream of RHEL. I chose to go the Centos 10 method to complete my midterm projec; Centos Stream 10 to be exact. There is not much different about using the updated centos. Some cli tools may be a bit different, but off the top of my head, I can't think of an example.

Package names:
If you go the Centos stream route, and are using the instructions provided in the redhat.com link above and in the midterm .docx file, there is a single package name you must modify during the yum install portion.
The package ```policycoreutils-python``` has changed to ```policycoreutils-python-utils```.
The new install command would be:
```yum install sssd realmd oddjob oddjob-mkhomedir adcli samba-common samba-common-tools krb5-workstation openldap-clients policycoreutils-python```
