# noconda

Guidelines how to move away from Anaconda and use standard tools for installing Python, managing packages and environments. 


## Install Python For Mac users

There is a [long version](noAnacondaMac.md), the tldr version for the impatients is:

- Download and run the installer from [Python.org](https://www.python.org/downloads/)
- Open a terminal 
  > make sure you open the terminal after you have installed Python, otherwise you `$PATH` may not be properly up to date! (you can also source your `.zprofile`).

- If you do not need environments, open a terminal, and type (add the packages you need):
```
$ pip3 install numpy scipy matplotlib astropy jupyterlab
$ jupyter-lab
```
- If you use environments, type (add the packages you need):
```
$ python3 -m venv myEnv
$ source myEnv/bin/activate
(myEnv) $ pip3 install numpy scipy matplotlib astropy jupyterlab
(myEnv) $ jupyter-lab
(myEnv) $ deactivate
```
