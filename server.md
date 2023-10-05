Connecting to servers

When we connect to servers, we use `ssh username@<hostname>`. In order to shorten the name, we can update in DNS directory `/etc/hosts` file. 

### server side
Yes, you need to be able to get access to the server side first so that you can lookup the IP address. If you know the IP address in advance, you don't need to. 
```
nslookup <hostname>

Server:		XX.XXX.252.18
Address:	XX.XXX.252.18#53

Name:	dev07.xxx.xxxxxx.xxx.xxx.xxxx.xxx      # <hostname>
Address: xx.xxx.xxx.xxx                      # <---- the address you need
Name:	dev07.xxx.xxxxxx.xxx.xxx.xxxx.xxx
Address: xxxx:xxxx:efxx:x::xxxx
```

### host side
```
vi /etc/hosts

xx.xxx.xxx.xxx  <hostname>  <nickname>
```

`esc` --> `:wq!`

You can then 
```
ssh <nickname>
```

### To check which port the server is currently running 

```
netstat -tnlp

[root@577e724c1a35 data]# netstat -tnlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:18000           0.0.0.0:*               LISTEN      5076/ydisc          
tcp        0      0 0.0.0.0:4080            0.0.0.0:*               LISTEN      4168/traffic_manage 
tcp        0      0 0.0.0.0:18001           0.0.0.0:*               LISTEN      5076/ydisc          
tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN      4168/traffic_manage 
tcp        0      0 0.0.0.0:6789            0.0.0.0:*               LISTEN      5076/ydisc   
```
If you want to kill the process, use this `kill -9 <PID>`

### .ssh/config 

Instead of setting up at the `/etc/hosts`, you can also set up in `~/.ssh/config` 

```
Host <nickname>
 HostName <hostname>
```

### Check which ports are being used 

```
sudo lsof -i -P -n | grep LISTEN
master     2409        root   13u  IPv4     45923      0t0  TCP 127.0.0.1:25 (LISTEN)
master     2409        root   14u  IPv6     45924      0t0  TCP [::1]:25 (LISTEN)
sshd       9148        root    3u  IPv4 200069285      0t0  TCP *:22 (LISTEN)
sshd       9148        root    4u  IPv6 200069287      0t0  TCP *:22 (LISTEN)
```

### Check which processes are being run and kill 

```
ps aux | grep "python"
sudo kill -u yahoo kill -s SIGINT xxxxx

OR

top            # to check the PID
kill -9 <PID>
```

### Check how many processes are spun off from the parent script by `ps wafux`

```
bash-4.2# ps wafux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root     19344  0.0  0.0  13428  1956 pts/4    Ss   20:18   0:00 bash
root     21030  0.0  0.0  53328  1760 pts/4    R+   21:10   0:00  \_ ps wafux
root     27972  0.0  0.0  13424   872 pts/2    Ss+  Feb13   0:00 bash
root     27124  0.0  0.0  13424   864 pts/1    Ss+   2022   0:00 bash
root         1  0.0  0.0  13292   780 pts/0    Ss+   2021   0:03 /bin/bash /tmp/bin/init_startup.sh --region apac --enable_prod true --enable_bucket none
root        50  0.0  0.0   8568   576 ?        Ss    2021   7:41 /home/y/sbin/ycron -s
root     20852  0.0  0.0   8568   504 ?        S    21:04   0:00  \_ /home/y/sbin/ycron -s
root     20855  0.0  0.0   9568  1136 ?        Ss   21:04   0:00      \_ /bin/sh /home/y/var/qis/server/bin/run_fetcher.sh
root     20859  0.0  0.0 131472  4356 ?        S    21:04   0:00          \_ sudo /usr/bin/python3 /home/y/var/qis/server/src/source_fetcher.py -f /home/y/var/qis/server/fetche
root     20860  0.0  0.0 197844 18088 ?        Sl   21:04   0:00              \_ /usr/bin/python3 /home/y/var/qis/server/src/source_fetcher.py -f /home/y/var/qis/server/fetcher
root     20867  0.0  0.0  86816 19660 ?        S    21:04   0:00                  \_ /usr/local/bin/perl -w /usr/local/bin/yinst install qp_data_configs -br test -dryrun -tag s
root     21028  0.8  0.0 319256 24136 ?        Sl   21:10   0:00                      \_ /usr/bin/python -tt /bin/repoquery --qf %{VERSION}-%{RELEASE} yinst
root        51  0.0  0.0   5972   292 pts/0    S+    2021   0:00 tail -f /dev/null
```

