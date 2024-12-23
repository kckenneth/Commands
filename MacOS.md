to check if the mac is 32 or 64 bit

```
getconf LONG_BIT
```

## Check the PATH 

```
echo $PATH

/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin
```

#### Adding additional path to $PATH

```
export PATH=${PATH}:/opt/homebrew/bin

## Check

echo $PATH
/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/opt/homebrew/bin
```


# Install Jupyter Notebook on mac

https://jupyter.org/install
https://brew.sh

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
export PATH=${PATH}:/opt/homebrew/bin
brew install jupyterlab
```

Start the jupyter notebook
```
jupyter notebook
```

# Run jupyter notebook in virtual environment

```
python3 -m venv my-env
source ./my-env/bin/activate

pip install nltk
python uninstall ipykernel
python -m ipykernel install --user --name=my-env     # this will let the virtual environment 'my-env' available as kernel in jupyter notebook

# install tensorflow by pip
# https://www.tensorflow.org/install/pip#macos
```

You'd install all the necessary lib in `my-env`. When you run `jupyter notebook`, you need to separately execute the command in another terminal. You cannot execute `jupyter notebook` inside `my-env` virtual environment. 

After jupyter notebook launch, you can choose the `my-env` kernel`. 

------------

#### Check the content of gz file 

```
gzip -cd part_querycontext.gz| more

* ✧ ・ ゚ {(schatz,2),(laura,2)}
0       {(60,7837),(1,5664),(5,5272),(x80070643,4386),(3,4202),(2,3892),(0,3637),(financing,3127),(car,3030),(interest,2990),(apr,2723),(4,2566),(times,2434),(error,2381),(credit,2229),(balance,1996),(gpt,1679),(10,1679),(road,1638),(6,1634),(9,1583),(20,1582),(percent,1530),(8,1462),(25,1427),(transfer,1409),(02,1306),(05,1099),(phai,1003),(01,989),(st,948),(100,945),(7,915),(btc,908),(gomovies,846),(03,845),(mg,837),(75,801),(point,763),(00,748),(dr,747),(la,740),(ave,739),(15,728),(finance,720),(16,690),(12,689),(delay,666),(movies,665),(30,643),(04,614),(street,598),(auto,595),(eth,570),(ping,555),(drive,544),(400,537),(13,497),(lane,490),(24,472),(malayalam,464),(time,460),(40,460),(nicotine,458),(06,456),(cars,455),(lease,455),(cards,439),(11,432),(aadhaar,428),(degree,425),(50,424),(deals,424),(08,422),(45,415),(xc000007b,398),(22,396),(mm,394),(35,393),(turn,387),(99,382),(carb,373),(07,371),(18,371),(mol,369),(county,361),(usd,355),(month,349),(file,347),(calorie,346),(km,335),(gauge,332),(creek,332),(gio,331),(14,327),(blood,324),(09,308),(ai,305),(ln,305),(download,303)}
0 0     {(0,224),(7,133),(fertilizer,130),(60,97),(1,69),(50,62),(2,44),(potassium,33),(5,26),(with,24),(3,24),(25,23),(22,23),(6,21),(cron,21),(255,21),(skyrimse.exe,20),(24,19),(prodiamine,19),(financing,18),(8,17),(13,16),(4,16),(30,15),(potash,15),(20,14),(pre,13),(rgb,13),(movies,13),(17,13),(apr,12),(color,10),(means,9),(10,9),(0.2,8),(liquid,8),(granular,8),(12,8),(21.5,7),(face,7),(acelepryn,7),(100,6),(兆赫,6),(alcoholic,6),(18,6),(shut,6),(9,6),(flour,6),(porn,6),(62,6),(binary,6),(www.walia.us,5),(15,5),(第一,5),(在线,5),(хайрга,5),(crossword,5),(quadrant,5),(025,5),(error,5),(chess,5),(x7ff7d99a9944,5),(x7ff6d7c45b40,5),(48,5),(score,5),(cars,5),(studio,5),(games,4),(x7ff777547e90,4),(52,4),(221,4),
```
