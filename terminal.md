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


