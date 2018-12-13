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

### SSH key 

More <a href=https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys>Details.</a>  
Create ssh private and public key
```
$ ssh-keygen -f ~/.ssh/id_rsa -b 2048 -t rsa 
```
This will create id_rsa and id_rsa.pub keys. 

Copy public key to a remote host  
If you want to ssh without password, you need to copy the public key to a remote host. 
```
$ ssh-copy-id username@remote-host
```
Block ssh password login in the remote host, in remote host, change the `PasswordAuthentication` to `no`. If commented by `#`, uncomment. 
```
# sudo nano /etc/ssh/sshd_config

PasswordAuthentication no
```

On Ubuntu/Debian:
```
# sudo service ssh restart
```
On CentOS/Fedora:
```
# sudo service sshd restart
```

### Hardening the server

You need to protect your server from multiple attacks. Even if you setup the ssh and password, there always will be bot attack. `Fail2Ban` is an daemon app you'd install in your remote server to block multiple failed attempts.  

- This is from DigitalOcean how to <a href=https://www.linode.com/docs/security/securing-your-server/>Setup</a>.  
- This is my detailed <a href=https://github.com/kckenneth/Hardening/blob/master/README.md>Setup</a>.  

### Lock user account after failed login attempt

You need to change the Linux PAM (Pluggable Authentication Module)

The following 3 lines are required to implement the account lock after failed login attempt. These lines will be implemented separately. 
```
auth        required       pam_faillock.so preauth silent audit deny=3 unlock_time=300
auth        [default=die]  pam_faillock.so authfail audit deny=3 unlock_time=300
account     required       pam_faillock.so
```
#### Explanation 
- `audit` enables user auditing 
- `deny=3` is after 3 failed login attempt 
- `unlock_time=300` 5 minutes will be locked after 3 failed login attempt 

Go to the following two files. But you'll be implementing in `system-auth` first. Then repeat the process in `password-auth` as well. 
```
$ vi /etc/pam.d/system-auth
$ vi /etc/pam.d/password-auth 
```

```#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth        required      pam_env.so
**auth        required      pam_faillock.so preauth silent audit deny=3 unlock_time=300**
auth        sufficient    pam_fprintd.so
auth        sufficient    pam_unix.so nullok try_first_pass
**auth        [default=die]  pam_faillock.so  authfail  audit  deny=3 unlock_time=300**
auth        requisite     pam_succeed_if.so uid >= 1000 quiet
auth        required      pam_deny.so

account     required      pam_unix.so
account     sufficient    pam_localuser.so
account     sufficient    pam_succeed_if.so uid < 500 quiet
account     required      pam_permit.so
**account     required      pam_faillock.so**
```
stars-coded lines are what you need to add into the existing modules. You can either use with or without `even_deny_root` which will deny the root login after 3 failed login attempt. 
```
auth        required      pam_faillock.so preauth silent audit deny=3 unlock_time=300
auth        required      pam_faillock.so preauth silent audit deny=3 even_deny_root unlock_time=300
```
However when I tried `even_deny_root`, it completes block ssh root login even with the correct password. So I avoid using that. 

To activate the configuration 
```
# systemctl restart sshd  [On SystemD]
# service sshd restart    [On SysVInit]
```

#### To check the failed login attempt
```
# faillock --user root

root:
When                Type  Source                                           Valid
2018-12-12 22:37:21 RHOST 218.92.1.151                                         V
2018-12-12 22:32:17 RHOST 218.92.1.151                                         I
2018-12-12 22:32:19 RHOST 218.92.1.151                                         I
2018-12-12 22:37:23 RHOST 218.92.1.151                                         V
2018-12-12 22:38:03 RHOST 218.92.1.151                                         V
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
### Docker

More <a href=https://github.com/kckenneth/Docker/blob/master/README.md>Here</a>.

### Internet TCP

tested on Mac
```
$ netstat -p TCP

Active Internet connections
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
tcp4       0      0  localhost.29961        localhost.60258        ESTABLISHED
tcp4       0      0  localhost.60258        localhost.29961        ESTABLISHED
tcp4       0      0  10.0.0.3.60257         counteract.rocke.10005 SYN_SENT 
```

Checking the AS (Autonomous System)

```
$ dig stanford.edu

;; ANSWER SECTION:
stanford.edu.		1473	IN	A	171.67.215.200
```
Check the `ANSWER SECTION` and note the IP. Use the IP to look up the AS with netcat `nc` command. 
```
$ nc whois.cymru.com 43
171.67.215.200

AS | IP | AS Name
32 | 171.67.215.200 | STANFORD - Stanford University, US
```
Find the Owner of the IP address, AS, prefix
```
$ whois -h whois.ra.net 171.67.215.200

route:      171.64.0.0/14
descr:      AS32 proxy-registered route by Cogent
origin:     AS32
remarks:    Proxy-registered route object
remarks:    for Cogent customer
notify:     neteng@cogentco.com
mnt-by:     MAINT-AS174
changed:    neteng@cogentco.com 20031230
source:     RADB
```

Check the network configuration
```
$ ifconfig
```

Check the hop
```
$ traceroute -a stanford.edu
```


