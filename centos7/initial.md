## CentOS7 Minimal Setup
Real programmers do NOT need any graphical environment.
This page shows the way to setup the minimal CentOS7.
The latest minimal installation media is available 
[here](http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso).

### Hostname, YUM Repository
```
hostnamectl set-hostname pc123.morifuku.com
yum install epel-release
```
### Networking, Security

Note that: the following steps make your centos7 "unsecured".
```
yum install net-tools
nmcli c add type ethernet ifname enp0s8 con-name enp0s8
nmcli c add type ethernet ifname enp0s9 con-name enp0s9
nmcli c add type ethernet ifname enp0s10 con-name enp0s10
nmcli c mod enp0s8 ipv4.method manual ipv4.addresses 192.168.1.3/24
nmcli c mod enp0s9 ipv4.method manual ipv4.addresses 192.168.2.3/24
nmcli c mod enp0s10 ipv4.method manual ipv4.addresses 192.168.3.3/24
nmcli c up enp0s8
nmcli c up enp0s9
nmcli c up enp0s10
systemctl stop firewalld
systemctl disable firewalld
vi /etc/selinux/config
reboot
```
/etc/selinux/config
```
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
```

### NTP, Time Zone
```
vi /etc/chrony.conf
systemctl start chronyd
systemctl enable chronyd
systemctl status chronyd
chronyc tracking
ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
```
/etc/chrony.conf
```
#server 0.centos.pool.ntp.org iburst
#server 1.centos.pool.ntp.org iburst
#server 2.centos.pool.ntp.org iburst
#server 3.centos.pool.ntp.org iburst
server ntp.nict.jp iburst
```
