## install virtualenv
First install the virtualenv, this can elimite the misuse of python2 and python3.

```bash
$ pip3 virtualenv
```
this will install the virtualenv under python3.

## create a virtual environment
Then create a virtual environment.

```
$ virtualenv /path/to/env
```
this will create a virtual environment with a new python in the path. The version will be default the same as the pip version you used to install `virtualenv`. Here it will be the python3.

## activate 
Then activate the virtual env:

```
$ cd /usr/bin/virtual
$ source bin/activate
```
This will activate you virtual environment. The `python` command will be the version in the virtualenv. You do not need to specify the version for next.

To disable it, just run `$ deactivate` to clear the virtual env from bash source file.

## start using
Now you can just install some module using `pip install xx` and `python xx` to run something.

Make a new scrapy project:

```
$ scrapy startproject newproject
```