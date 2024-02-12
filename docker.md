## Docker container volumne 

```
-v <current directory in the host>:<directory in the container>
```

```
sudo docker run -it --name build_container -v `pwd`:/workspace -v $HOME:/root -v /var/lib/sia/:/var/lib/sia --cap-add=SYS_PTRACE --security-opt seccomp=unconfined docker.ouroath.com:4443/ylinux/ylinux7:7.9.14 bash
```

whatever path you're on, `pwd`, the content of the `pwd` will be available in the `build_container` `/workspace` directory. 

## Docker default path

Docker default path is `/var/lib/docker`. You can check if the space is enough in the path. If not, you can create a softlink `/var/lib/docker` to where there's enough space. 

```
df -h

Filesystem            Size  Used Avail Use% Mounted on
devtmpfs               47G     0   47G   0% /dev
tmpfs                  47G     0   47G   0% /dev/shm
tmpfs                  47G  2.4M   47G   1% /run
tmpfs                  47G     0   47G   0% /sys/fs/cgroup
/dev/mapper/sys-root  9.8G  5.9G  3.4G  64% /
/dev/sda2             488M  220M  233M  49% /boot
/dev/mapper/sys-var   4.0G  2.7G  1.4G  66% /var
/dev/mapper/sys-home  354G   33G  321G  10% /home
/dev/mapper/sys-tmp   4.0G   33M  4.0G   1% /tmp
```

There's only `1.4G` available in `/var`. But there's `321G` available in `/home`. So tricking the docker that when it installs its own default path `/var/lib/docker`, we're directing to `/home/`. To do so

```
sudo rm -rf /var/lib/docker
sudo mkdir -p /home/docker
sudo ln -s /home/docker /var/lib/docker       # ln -s <actual directory> <link to actual dir in turquoise color>
```

In short, the `/home/docker` is the actual directory where the physical file exists. The shortcut `/var/lib/docker` is an alias that will direct to the actual `/home/docker` directory. So when you list them in `/home/docker` directory, you'd see like this. 

```
ls -a
lrwxr-xr-x   1 kchen08  staff    37B Feb 12 17:37 /var/lib/docker -> /home/docker
-rw-r--r--   1 kchen08  staff    27B Feb 12 17:37 testing.txt
```

The shortcut `/var/lib/docker` has the `l` for link. 

# docker container

If you start the container and want to exit the container without stopping the container running, execute one after another in shell 

```
ctrl+p ctrl+q
```

## Docker image pruning 

```
# We build docker image daily and need to prune useless images.
  sudo docker image prune -f -a --filter "until=168h" #7*24=168h
```

## Checking inside docker without logging in

```
cat local | sudo docker exec -i test_qis_us_prod bash -c '/qis/tools/scrape.py -E' > /tmp/health_check_result_us.txt
```

## Removing dead, removal in progress containers

```
sudo ls -alh /var/lib/docker/containers                 # check the containers id
sudo rm -rf /var/lib/docker/containers/<container_ID>
sudo service docker stop                                # need to restart the docker
sudo service docker start
```
