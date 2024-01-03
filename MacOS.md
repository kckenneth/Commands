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

