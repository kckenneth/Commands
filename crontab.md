This is a snippet of how to use crontab to run python program automatically. 

1. crontab comes in Linux. Since mac is built upon linux, you don't need to install crontab. 
2. check if you have any crontab file in your system by 

```
crontab -l
```
If you have a file, it will show the file. If not, you need to create the cron file. 

```
crontab -e
```

This will launch the `vi`. 

Click `i` to enter `insert` mode in vi. 
Enter the following

```
# crontab -e
0 17 * * 1-5 cd all_git && /Library/Frameworks/Python.framework/Versions/3.6/bin/python3 /Users/<User>/all_git/options_scanner.py
```
Click "esc" to exit the insert mode.
Type `:wq` to `write and quit` the file. 

What it does it, every day during the weekday `1-5` at 5 o'clock `0 17`, it will run change to the directory and run the python program from the path indicated. 

A few explanations that I found useful. 

https://www.jcchouinard.com/python-automation-with-cron-on-mac/
https://www.hostinger.com/tutorials/cron-job
https://opensource.com/article/17/11/how-use-cron-linux
  
