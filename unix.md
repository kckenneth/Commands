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




