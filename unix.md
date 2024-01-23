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

### Find file containing string 

```
grep -nrw "driving"
```

-n : line number 
-r : recursive
-w : match whole world, eg driving

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

## Delete line in a range 

```
sed '1,5d' myFile.txt
```

## Print line in a range 

https://stackoverflow.com/questions/83329/how-can-i-extract-a-predetermined-range-of-lines-from-a-text-file-on-unix 

```
sed -n '16224,16482 p' myFile.txt > new-file
```

Where 16224,16482 are the start line number and end line number, inclusive. This is 1-indexed. -n suppresses echoing the input as output, which you clearly don't want; the numbers indicate the range of lines to make the following command operate on; the command p prints out the relevant lines


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

## Change file name from a string to another 

foo-bar-file.txt --> fool-file.txt 

```
for file in *.txt; do mv $file ${file//-bar/}; done
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

## count the frequency of a string 

### Note: Better use a single quote with awk command

In `awk`,

`$0` = the entire string 
`$1` = the first word 

`apple is a fruit.`  
`$0` = `apple is a fruit.`   
`$1` = `apple`  

```
cat test.txt 

apple	fruit
orange	fruit
lemon	fruit
apple	fruit
apple	device
samsung	device
```

Count the frequency of a string `fruit`. This is the easier way to count the unique words. 

```
awk '{print $2}' test.txt | sort | uniq -c

2 device
4 fruit
```

Using Array, this is longer, but much control on what you want. 

```
awk -F'\t' '{count[$2]++} END {for (word in count) print word, count[word]}' test.txt 

fruit 4
device 2
```

count[$2] will keep counting up the same string. This is kind of like a dictionary. If we know which `word` we're looking for, eg `fruit`, we could also execute 

```
awk -F'\t' '{count[$2]++} END {for (word in count) { if (word == "fruit") { print word, count[word]}}}' test.txt

fruit 4
```

## Count on condition 

```
cat test.tsv |awk -F'\t' '$4=="tv_intent"{cnt[$6]++} END{for(i in cnt) print i"\t"cnt[i]}'|sort -t$'\t' -k2 -nr

common	144
general	49...
```

## Check if the column is empty 

https://stackoverflow.com/questions/43790965/print-only-if-field-is-not-empty 

since awk commands are formed as `condition { actions }`, and the default action is to print, this can be condensed to just `awk '$4' test.txt` 

```
cat test.txt
1   apple   $0.2    walmart
2   orange    $0.15  walmart
3   strawberry  $0.2 
4   lemon   $0.05 
5   lychee  $0.3    new york mart
```

If checking the 4th column, if the value is empty,

```
awk -F'\t' '($4==""){print $2}' test.txt | sort

lemon
strawberry
```

If checking the 4th column, if there's a value,

```
awk -F'\t' '$4' test.txt | sort

apple
lychee
orange
```

## display nth line 

https://www.theunixschool.com/2012/12/how-to-print-every-nth-line-in-file-in.html 

showing every 2nd line 
```
awk '!(NR%2)' file.txt 

orange  5
print text  50
```

## print the nth line 

https://stackoverflow.com/questions/6022384/bash-tool-to-get-nth-line-from-a-file

printing 10th line
```
sed '10q;d' file.txt
```

## print all lines into a single line 

```
file.txt
apple
orange juice
strawberry
```

This will print all lines into a single line, delimited by a vertical `|`

```
awk '{printf "%s|",$0}' file.txt > single.txt
```

```
single.txt

apple|orange juice|strawberry|
```

## print line number 

```
awk -v OFS='\t' '{print NR,$0}' file.txt > new.txt
```

```
new.txt

1 \t apple
2 \t orange juice
3 \t strawberry
```

## print the number of fields (NF) or last field 

Since NF is the number of field, using the `$` will print the last field. For penultimate field, use `$(NF-1)`

```
awk -F'\t' '{print $NF}'
awk -F'\t' '{print $(NF-1)}'
```

## check the value 

```
awk -F'\t' '$2 >= 10 {print $1 $2}' file.txt 

strawberry  10
print text  50
```

## Remove fileB content from fileA 

fileA
```
how to join sql 
why sql statement
how to parse values
apple
eat orange 
```

fileB 
```
join sql
to parse
```

```
fgrep -vf fileB fileA

why sql statement
apple 
orange
```

If want to remove exact match, use `-x`

```
fgrep -xvf fileB fileA
```

## Extract common content/same string between fileA and fileB 

```
fileA 
apple 
orange
sort dictionary
nectar mattresses

fileB 
orange
nectar
apple

fgrep -Fxf fileA fileB
apple
orange
```

-F : plain strings (not regex)
-x : exact match 
-f : check line by line 

## compare FileA and FileB and get match or non-match 

https://stackoverflow.com/questions/32481877/what-are-nr-and-fnr-and-what-does-nr-fnr-imply 

```
cat file1.txt 
lemon	12
strawberry	30
watermelon	15
mango	15

cat file2.txt 
strawberry
banana
apple
```

#### get the FileB content not present in FileA

NR = total record number  
FNR = file number of row 

1. first, recording the 1st column `$1` of file1.txt in an array `a`. 
2. second, `($1 in a)`, the `$1` is the 1st column value of file2.txt. The `$1` is checked if it's present in the array `a`. 
3. `!` is negating. 
 
```
awk -F'\t' 'NR==FNR {a[$1]++;next;}!($1 in a)' file1.txt file2.txt 
banana
apple
```

#### get the FileA content not present in FileA 1st column 

```
awk -F'\t' 'NR==FNR {a[$1]++;next;}!($1 in a)' file2.txt file1.txt 
lemon	12
watermelon	15
mango	15
```

## Remove a string by pattern 

```
cat test1.txt 
grill menu	context
mexican grill menu	organization
grill menu in orlando	context

awk -F'\t' '!/^grill menu\t/' test1.txt
mexican grill menu	organization
grill menu in orlando	context
```


## add new column by awk 

add `-v` for OFS. 

```
cat test.txt 
orange 

awk -F'\t' -v OFS='\t' '{print $0,"","apple","s"}' test.txt 
orange  apple s 
```

## replace character with another character by sed 

streaming editor, a character to be replaced bounded by two forward slashes `//`

```
cat test.txt
apple),toOrange(0)(),

cat test.txt | sed -e 's/)/-/g'
apple-,toOrange(0-(-,

cat test.txt | sed -e 's/)/-/' 
apple-,toOrange(0)(),

cat test.txt | sed -e 's/)/\//g'
apple/,toOrange(0/(/,

cat test.txt | sed -e 's/)/\//' 
apple/,toOrange(0)(),
```

#### replace 's apostrophe s by sed

use the double quote 

```
cat test.txt | sed -e "s/'s/%27/g"
argentina%27 women national football team
brazil%27 woman
```

#### remove `^M` caret M 

In view mode, `vi`, sometimes Unix file can have a caret M at the end of the string. To remove

```
sed -e "s/\r//g" file > newfile
```

## To lower string by awk 

https://stackoverflow.com/questions/2264428/how-to-convert-a-string-to-lower-case-in-bash 

```
awk '{print tolower($0)}' fileA > fileA_lower
```

## To trim string by awk 

https://stackoverflow.com/questions/9175801/how-to-remove-leading-and-trailing-whitespaces 

```
cat test.txt 
  john wick
apple
orange
  lemon    juice

awk '{$1=$1}1' test.txt 
john wick
apple
orange
lemon juice
```


## To delete files except one file 

https://unix.stackexchange.com/questions/153862/remove-all-files-directories-except-for-one-file 

```
$ shopt -s extglob 
$ rm -- !(file.txt)
```

## Override place name aliases 

```
#!/bin/bash

kbplace=$1
overrideList=$2

function check_place_name {
  kb=$1
  over=$2

  declare -A overdict
  declare -A overalias
  declare -A checked

  i=0
  while IFS=$'\t' read -r key value attrk attrv; do
    if [[ $key && $value ]]; then
      overdict[$key]+=${value}$'\n'
      overalias[$value]+=${key}$'\n'

      i=$[$i+1]
    fi
  done < $over

  echo ${i} " total number of place_name to override successfully loaded"

  counter = 0
  while IFS=$'\t' read -r term data; do
    if [[ ! -z $data ]]; then
      temp=$(echo $data | cut -d $'\001' -f2)
      if [[ $temp = yk:* ]]; then
        wiki=$(echo $temp | cut -c4-)
      else
        wiki=$temp
      fi

      if [[ -z ${overalias[$term]} ]]; then
        echo -e "${term}\t${data}" >> yk.place_name_kept
        counter=$[$counter+1]
      fi

      if [[ ! -z $wiki ]]; then
        if [[ ${overdict[$wiki]} ]]; then
          echo "wiki:" $wiki

          #first time referent checking and creating entity with a list of aliases
          if [[ -z ${checked[$wiki]} ]]; then
            while IFS=$'\n' read -r line; do
              if [[ $line ]]; then
                echo -e "${line}\t${data}" >> yk.place_name_override
              fi
            done < <(echo "${overdict[$wiki]}")
            checked+=([$wiki]=1)
          fi
        fi
      fi
    fi
  done < $kb
}

check_place_name kbplace $overrideList
```

### Delimiter

If you want to add a caret delimiter `^`, in terminal, press `ctrl+v`. That will make the caret ready on screen. `^`. Then press whichever delimiter you want. If you want `^C`, you'll do like this

```
ctrl+v --> ctrl+c
```

For `^B`, you can directly do by `ctrl+b`. 
