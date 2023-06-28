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
