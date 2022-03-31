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



