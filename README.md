# Commands

This is a list of useful commands that I found very handy in time. 

### Check the ssh connection and kill it by PID

```
# ps -aux | grep ssh
kill -9 <PID>
```

if on CentOS
```
# yum install net-tools
# netstat -tnlp
```
if on Ubuntu
```
# apt-get install net-tools
# netstat -tnlp
```
