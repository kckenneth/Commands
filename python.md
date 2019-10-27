# Check which python and their path

```
which -a python python3

/Library/Frameworks/Python.framework/Versions/2.7/bin/python
/Library/Frameworks/Python.framework/Versions/3.6/bin/python
```

```
type -a python            # does the same thing
```

# Install by PIP (Preferred Installer Packages) 

```
pip install numpy    # for python2
pip3 install numpy   # for python3 
```

# Upgrade the existing library
1. Uninstall and install approach
```
pip uninstall numpy 
pip install numpy
```
2. Upgrade approach
```
pip install numpy --upgrade      # or
pip install nump -U
```

# Install packages in jupyter notebook
```
!pip install numpy
```

# Ignore warning messages during installation

```
pip install --ignore-installed ${PACKAGE_NAME}
pip install --ignore-installed six
```
# Install fastai==0.7.0
```
!pip3 install fastai==0.7.0      # in jupyter notebook
```

# Keras
```
pip uninstall keras
pip install -I keras==2.2.0
```

Note
Need to downgrade keras from 2.2.4 to 2.2.0 when I got the error while training RCNN
```
ValueError: Shape must be rank 1 but is rank 0 for 'bn_conv1/Reshape_4' (op: 'Reshape') with input shapes: [1,1,1,64], [].
```
# Run the python program in the background
```
nohup python app.py &
```
<a href="https://github.com/kckenneth/Elasticsearch">source</a>

To stop the program, first check which `PID` the program is assigned to. 
```
top
```
note down the `PID` number, if the `PID` is 4046
```
kill -9 4046
```
If you can't find from the `top` command, you can also do so by
```
netstat -tnlp
```


