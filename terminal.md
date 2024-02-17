### Create symbolic link

```
## ln -s existing_source_file optional_symbolic_link

$ ln -s /data/real_data.txt /home/kchen
```

### Check which file takes the largest space 

```
cd /
du -sh * | sort -hr | head -n10
bash-4.2# du -sh * | sort -hr | head -n10
22G	source
21G	data
13G	contextualtagger

cd source                                    # cd into the largest directory
du -sh * | sort -hr | head -n10
```

### bash flags

https://ss64.com/bash/syntax-file-operators.html

```
The following operators return TRUE if..

 -a    file exists  This is identical in effect to -e.
       The -a form has been deprecated and its use is discouraged.
 -b    file is a block device
 -c    file is a character device  [ -b "/dev/sda2" ]
 -d    file is a directory
 -e    file exists
 -f    file is a regular file (not a directory or device file)
 -G    group-id of file same as yours
 -g    set-group-id (sgid) flag set on file or directory
          If a directory has the sgid flag set, then a file created within that directory belongs to the group
          that owns the directory, not necessarily to the group of the user who created the file.
 -h    file is a symbolic link
 -k    sticky bit1 set
 -L    file is a symbolic link
 -N    file modified since it was last read
 -O    you are owner of file
 -p    file is a pipe  [ -p /dev/fd/0 ]
 -r    file has read permission (for the user running the test)
 -S    file is a socket
 -s    file is not zero size
 -t    file (descriptor) is associated with a terminal device.
 -u    set-user-id2 (suid) flag set on file
 -w    file has write permission (for the user running the test)
 -x    file has execute permission (for the user running the test)

 -nt   file f1 is newer than f2   f1 -nt f2
 -ot   file f1 is older than f2   f1 -ot f2
 -ef   files f1 and f2 are hard links to the same file   f1 -ef f2
    
 !     "not" -- reverses the sense of the tests above (returns true if condition absent).
```

