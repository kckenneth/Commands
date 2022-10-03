These are a few commands that are useful in unix terminal. 

Data is on `.txt` file.

### head and tail
```
$ head -n 5 data.txt
$ tail -n 5 data.txt
```
Calling the top 5 lines or the last 5 lines from the data. 

### wc 
```
$ wc data.txt
$ wc -l data.txt
```
print newline, word, and byte counts for each file. 
`-l` tag will only print the number of lines. 

### Find line of interest and print
When the file is very large, `cat` will be very messy. When we just want to find a few lines of interest, 
1. first find the line number 
2. print the content between the line numbers 

```
vi myFile.txt
/my favorite
```
1. When you call the `vi` on `myFile.txt`, the content from `myFile.txt` will occup as large as your terminal window size allows. 
2. You then press `/` and type the line `my favorite`. 
3. It will then show you the line with `my favorite` if the `myFile.txt` contains the line `my favorite`. If you want to capture the paragraphs or whatever, take note of the line number. Let's say if the line number is `1280` and you want content up to `1295`. 

```
awk "NR >= 1280 && NR <= 1295" myFile.txt
```

### Find the line number for the text of interest
Sometimes the above approach doesn't give you the line number, you need to `grep`. First you need to know the text you're looking for. You might also want to know `+/-` number of lines above and below the text of interest. 

`grep -n -3 "string to search" largeFile.txt`

```
grep -n -3 "// ====== sports " us_web.jabba 
1275-	@__movie_reference `task="query_reference";rule_id="movie_reference"`
1276-];
1277-
1278:// ====== sports ======
1279-
1280-// Natural language patterns for sports domain
1281-
```

The other approach is 
```
vi largeFile.txt
:set number
```

### Insert text at a specific line number 

Once you know the line number where you want to insert the text, you can use `ed` text editor. `ed` is interactive, which means once you call the `ed` command, it's interactive and update the file. 

```
ed myFile.txt
32
```

The first command `ed myFile.txt` will return `32` which indicates the number of character inside `myFile.txt`. You're now in interactive mode. If you want to quit, use 
```
.
w
q
```

In each typing, 
`.`, hit Enter. 
`w`, hit Enter. 
`q`, hit Enter. 

If `myFile.txt` has contents
```
cat myFile.txt
I
am
Ken
```

You want to add new line at line number `2`, use `2i` to indicate the line number `2` and `i` for insertion. 
```
ed myFile.txt
32
2i                    # hit Enter
This is new line      # type "This is new line" and hit Enter
.                     # type "." and hit Enter
w                     # type "w" and hit Enter
q                     # type "q" and hit Enter
```

`myFile.txt` will be updated with a new line. 
```
cat myFile.txt
I
This is new line
am
Ken
```

If you want to add a paragraph, make a file, eg, `toAdd.txt`

```
2i
This is a new line
Will take up space
Hope it can fit
.
w
q
```

Execute as before

```
ed myFile.txt < toAdd.txt
```


Ref: https://www.baeldung.com/linux/insert-line-specific-line-number

### Alias

Sometimes we want to shorten our command. Example, if we want to use `ls -alh`, we can shorten in `alias`. In order to do so, just type 
```
alias ll="ls -alh"
```
This will automatically add the command ```ls -alh``` in alias and can be called as `ll`. So instead of typing the entire ```ls -alh```, we can now just type ```ll```. 

To remove alias, just ```unalias ll```, it will remove the `ll` alias. 


Of course, we might have a multiple list of aliases. In that case, just add those alias list in certain files. You can then activate. Example, you can add the list of aliases in `~/.bashrc`. However, you need to `source ~/.bashrc` everytime you create a shell. Linux source `~/.profile` everytime a new shell is created. So you can add the command such as if the file `~/.bashrc` exists, source it. If `~/.profile` file doesn't exist, create one. `.` is the same as `source`. 

```
vi ~/.profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi 
```

## Change file name sequentially from a certain number 

existing file names: `my001.jpg`, `my002.jpg`, etc to `my111.jpg`, `my112.jpg` etc 

```
n=111;
for file in *.jpg ; do mv  "${file}" basename"${n}".jpg; n=$((n+1));  done

for f in *.jpg; do mv "$f" my${n}.jpg; n=$((n+1)); done
```

## Sort file content based on column 

file.txt contains two values separated by tab
```
apple   1
orange  5
strawberry  10
print text  50
```

-nr : numerical reverse 
-k : column 
```
sort -nr -k2 -t $'\t' file.txt > file_sorted
```

```
cat file_sorted
print text  50
strawberry  10
orange  5
apple   1
```

## add up values on column

```
awk -F'\t' '{s+=$2}END{print s}' file.txt
66
```

