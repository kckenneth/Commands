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
