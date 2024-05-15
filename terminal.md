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

https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html

```
-a file
True if file exists.

-b file
True if file exists and is a block special file.

-c file
True if file exists and is a character special file.

-d file
True if file exists and is a directory.

-e file
True if file exists.

-f file
True if file exists and is a regular file.

-g file
True if file exists and its set-group-id bit is set.

-h file
True if file exists and is a symbolic link.

-k file
True if file exists and its "sticky" bit is set.

-p file
True if file exists and is a named pipe (FIFO).

-r file
True if file exists and is readable.

-s file
True if file exists and has a size greater than zero.

-t fd
True if file descriptor fd is open and refers to a terminal.

-u file
True if file exists and its set-user-id bit is set.

-w file
True if file exists and is writable.

-x file
True if file exists and is executable.

-G file
True if file exists and is owned by the effective group id.

-L file
True if file exists and is a symbolic link.

-N file
True if file exists and has been modified since it was last read.

-O file
True if file exists and is owned by the effective user id.

-S file
True if file exists and is a socket.

file1 -ef file2
True if file1 and file2 refer to the same device and inode numbers.

file1 -nt file2
True if file1 is newer (according to modification date) than file2, or if file1 exists and file2 does not.

file1 -ot file2
True if file1 is older than file2, or if file2 exists and file1 does not.

-o optname
True if the shell option optname is enabled. The list of options appears in the description of the -o option to the set builtin (see The Set Builtin).

-v varname
True if the shell variable varname is set (has been assigned a value).

-R varname
True if the shell variable varname is set and is a name reference.

-z string
True if the length of string is zero.

-n string
string
True if the length of string is non-zero.

string1 == string2
string1 = string2
True if the strings are equal. When used with the [[ command, this performs pattern matching as described above (see Conditional Constructs).

‘=’ should be used with the test command for POSIX conformance.

string1 != string2
True if the strings are not equal.

string1 < string2
True if string1 sorts before string2 lexicographically.

string1 > string2
True if string1 sorts after string2 lexicographically.

arg1 OP arg2
OP is one of ‘-eq’, ‘-ne’, ‘-lt’, ‘-le’, ‘-gt’, or ‘-ge’. These arithmetic binary operators return true if arg1 is equal to, not equal to, less than, less than or equal to, greater than, or greater than or equal to arg2, respectively. Arg1 and arg2 may be positive or negative integers. When used with the [[ command, Arg1 and Arg2 are evaluated as arithmetic expressions (see Shell Arithmetic).
```

## Count number of lines for specific files 

```
# all file types
find . -type f -name '*.*'  -not -path  "./.git/*" -exec wc -l {} +

# only .cc file types
find . -type f -name '*.cc'  -not -path  "./.git/*" -exec wc -l {} +
```
