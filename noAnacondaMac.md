# How to use Python without Anaconda on MacOS

Antoine Mérand ([amerand@eso.org](mailto:amerand@eso.org)) - May 10, 2024

## Install Python from Python.org
MacOS comes bundled with Python3 located in `/usr/bin/`. This version are perfectly usable, but lags a bit behind: as of this writting, Sonoma 14.4.1 (which came out early 2024) ships with Python 3.9.6 which was release in mid-2021, whereas the latest available version of Python is 3.12 which is newer than MacOS!

Third parties package managers such as [MacPorts](https://www.macports.org/) and [brew](https://brew.sh/) allow to install newer Python versions, but the cleanest is probably to use the installer directly from [Python.org](https://www.python.org/). 

Once you run the installer [downloaded from Python.org](https://www.python.org/downloads/), Python will be installed in `/Library/Frameworks/Python.framework/Versions/3.12/`, assuming 3.12 is the version of Python you installed.

The installer puts some shortcuts in `/Applications/Python 3.12` and creates some shortcuts in `/usr/local/bin`. For calls from the terminal, your `~/.zprofile` will be automatically updated so `/Library/Frameworks/Python.framework/Versions/3.12/bin` is added to your path:
```
# Setting PATH for Python 3.12
# The original version is saved in .zprofile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.12/bin:${PATH}"
export PATH
```

> If you need to set `PYTHONPATH` (this is not needed if you use `pip3` to install packages), you can add these lines in your `~/.zprofile`: 
```
PYTHONPATH="/Library/Frameworks/Python.framework/Versions/3.12/"
export PYTHONPATH
```

### Check paths
To check if Python has installed properly (i.e. it points to the Python installation you just made):
```
% which python3
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3
``` 

> If this is not the case, you may need to open a new terminal or make sure your current terminal has sourced the latest `~/.zprofile` 
```
% source ~/.zprofile
```

## Install/uninstall packages on global installation
To install gloabal packages (i.e. not using environments), use the `pip3` command. You may want to upgrade pip before installing packages:
```
$ pip3 install pip --upgrade
```
Pip has a very easy syntax:
```
$ pip3 install numpy scipy matplotlib astropy
```
To search from packages, use the [Python Package Index (PyPI) webpage](https://pypi.org/): it provides the command line to install packages using `pip`. 

> Note that `pip` points to the 2.7 version on a Mac, it is important to use `pip3` to make sure it points to the Framework version you installed! in cas of doubt, check with `which pip3` 

## Installing and running IPython, Jupyter Notebooks

To install IPython, notebooks or Jupyter Lab, run:
```
$ pip3 install ipython
$ pip3 install notebook
$ pip3 install jupyterlab
```
The binaries will be in `/Library/Frameworks/Python.framework/Versions/3.12/bin` and should be directly accessible in your path by calling `ipython`, `jupyter-notebook`, `jupyter-lab`. You can check by typying `which ipython` for instance. Again, check your `~/.zprofile` and how your 'PATH' includes `/Library/Frameworks/Python.framework/Versions/3.12/bin`

## Upgrading / downgrading / managing packages

To upgrade `numpy` to the latest version, you should use:
```
$ pip3 install numpy --upgrade
```
Conversly, to install a specific version (e.g. to downgrade a package), you can use:
```
$ pip3 install numpy==1.26.3 
```
To uninstall a package, use:
```
$ pip3 uninstall scikit-learn
```
To know all installed packages currently, you can do:
```
$ pip3 list
```
To update all the ugradable packages, there are [no simple solutions](https://stackoverflow.com/questions/2720014/how-to-upgrade-all-python-packages-with-pip) but this will work:
```
$ pip3 --disable-pip-version-check list --outdated --format=json | python3 -c "import json, sys; print('\n'.join([x['name'] for x in json.load(sys.stdin)]))" | xargs -n1 pip3 install -U
```

> You will notice that `pip3` keeps in cache all the versions you have installed in the past. To clean the cache, you can use `pip3 cache purge`.

## Virtual environments

Since 3.3, Python includes `venv` as part of its Standard Library. Check out the [documentation](https://docs.python.org/3/library/venv.html) for extensive explanations. 

To create and activate a virtual environment `myEnv` (which will be stored in the directory `./myEnv` which will created if needed):
```
$ python3 -m venv myEnv
$ source ./myEnv/bin/activate
(myEnv) $ pip3 install ...
...
(myEnv) $ deactivate
$ 
```
When your shell prompt is preceeded by `(myEnv)`, you have a completely local installation in which you can run `pip3` to install packages with different versions. To deactivate the environment, simply type in the shell `deactivate`.

## Upgrading / downgrading Python

If you install and older or newer version of Python from python.org, it will keep the previously installed versions (in `/Library/Frameworks/Python.framework/Versions/`), but since it updates your `~/.zprofile` by appending to your `PATH`, this can lead to weird situations. For instance, `python3` will be the latest version installed, but `notebook` or `jupyter-lab` can be from a version you installed previously! it is recommended you edit your `~/.zprofile` (by typing `open ~/.zprofile` in a terminal) and keep only one version of this snippet:
```
# Setting PATH for Python 3.12
# The original version is saved in .zprofile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.12/bin:${PATH}"
export PATH
```
This will also be the case if you install a lower version. For instance, if you installed 3.11 after you installed 3.12, your `PATH` will point first to `/Library/Frameworks/Python.framework/Versions/3.11/bin`, then to `/Library/Frameworks/Python.framework/Versions/3.12/bin`. This is why keeping only one Python version in your `PATH` by manually updating your `~/.zprofile`
