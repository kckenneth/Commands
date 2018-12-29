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
