# noconda

Guidelines how to move away from Anaconda and use standard tools for installing Python, managing packages and environments. 


## Install Python For Mac users

There is a [long version](noAnacondaMac.md), the tldr version for the impatients is:

- Download and run the installer from [Python.org](https://www.python.org/downloads/)
- Open a terminal 
  > make sure you open the terminal after you have installed Python, otherwise your `$PATH` may not be properly up to date! (you can also source your `.zprofile`). Check that `python3` and `pip3` point to the correct place: `which python3` should return `/Library/Frameworks/Python.framework/Versions/3.12/bin/python3` (where `3.12` is the version of Python you just installed).

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


## Install Python and python packages for Linux users

(This is quite similar to the guidelines for Mac)

There is a [long version](noAnacondaLinux.md), the tldr version for the impatients is:

- You should first get python3 and pip3 installed on your computer. Both should in principle come as a default (pre-installed) on most Linux platforms. One way to test if you have it pre-installed is to just type:

    ```
    $ python
    ```
    as a shell command in a xterm window. 
    If successful, it should also tell you which version of python3 you have as a default.
    
    If not pre-installed, then go to [Python.org](https://www.python.org/downloads/) and follow the instructions.
    
    If you have sudo or root rights this should work with the usual `sudo apt install ...' (Debian, Ubuntu) or 'sudo dnf install ...' (Fedora) depending on your Linux distribution.
    
    If not, you should install it downloading the source code and compiling it. Ask us/IT!
  

- From now on you should be able to install any new python packages just using pip3. 
   - If you do *not* need environments (if you do not know what this means, you probably don't need it), you can install your favourite python package with a simple:
   
       ```
       $ pip3 install my_favourite_python_package
       ```
   - We would thus advise to install the usual suite of astro-useful packages, e.g., :
   
       ```
       $ pip3 install numpy scipy matplotlib astropy jupyterlab ipython
       ```
       
   - If you need/use environments, type (add the packages you need):

       ```
       $ python3 -m venv myEnv
       $ source myEnv/bin/activate
       (myEnv) $ pip3 install numpy scipy matplotlib astropy jupyterlab ipython
       (myEnv) $ jupyter-lab
       (myEnv) $ deactivate
       ```

    - If you wish to upgrade a given package with pip, it's simple

        ```
        pip3 install my_package --upgrade
        ```
    - If you wish to uninstall a package via pip:

        ```
        pip3 uninstall my_package
        ```
    
     - If you wish to install a long-er list of packages, you can also use requirements text files (e.g., requirements.txt) or toml files. We will provide a tutorial on this quite soon.
