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


