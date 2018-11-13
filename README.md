# Commands

This is a list of useful commands that I found very handy in time. 

### Check if the OS is 32 or 62 bit

Ubuntu
```
# file /sbin/init
```
CentOS
```
# file /lib/systemd/systemd

/lib/systemd/systemd: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=74584540f9e94865453495ad93b2954e7b07f5c6, stripped
```

### Check the ssh connection and kill it by PID

```
# ps -aux | grep ssh
kill -9 <PID>
```
if on Ubuntu
```
# apt-get install net-tools
# netstat -tnlp
```
if on CentOS
```
# yum install net-tools
# netstat -tnlp
```
### Export PATH

Better explanation on how <a href=https://stackoverflow.com/questions/13978654/export-path-in-profile-on-mac>export PATH works</a>. 

To quickly check the path
```
# echo $PATH
```

