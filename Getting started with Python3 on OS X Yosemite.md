# Getting started with Python 3 and virtual environments on OS X Yosemite

Notes on installing Python 3, virtualenv and virtualenvwrapper on OS X Yosemite.

Start by installing XCode from the Apple App store. The latest version (6.4) seems to include command line tools (these used to have to be installed seperately).

Create a ~/.bash_profile file to set the architecture type:

   # Set architecture flags
   export ARCHFLAGS="-arch x86_64"
   test -f ~/.bashrc && source ~/.bashrc

On OSX one way to install python3 is to install [Homebrew](http://brew.sh/) and use

    brew install python3

If you don't want to use Homebrew, you can go to https://www.python.org/downloads/ and download the latest python3 from there. 

I use virtual environments with Python to manage dependencies, so the next step is to install that (using pip3 makes sure you are using python3):

    pip3 install virtualenv

[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) makes using virtualenv much easier:

	pip3 install virtualenvwrapper

Make directories for your projects and virtualenvs if they don't already exist (by default virtualenvwrapper will use ~/.virtualenvs)

	mkdir -p ~/Projects ~/Virtualenvs

Use 'which python3' to find out where your python3 is so you can set it in .bashrc.

Create a ~/.bashrc file to set parameters for virtualenvwrapper:

	# pip should only run if there is a virtualenv currently activated
	export PIP_REQUIRE_VIRTUALENV=true
	# set paths to python & directories
	export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
	export WORKON_HOME=$HOME/Virtualenvs
	export PROJECT_HOME=$HOME/Projects
	source /usr/local/bin/virtualenvwrapper.sh

By setting PIP_REQUIRE_VIRTUALENV=true it prevents pip from running outside of a virtualenv - this might not suit you if you already have work using the systemwide python environment, but is a way to 'force' using virtualenv.

Make your first virtualenv:

	mkproject test1

This will create the ~/Projects/test1 directory and setup the python libraries for that virtualenv in ~/Virtualenvs/test1. It uses python3 because we set the VIRTUALENVWRAPPER_PYTHON to python3. You can use a command line option to change the python version.

Virtualenvwrapper also activates that virtual environment when you create it. To leave the virtualenv use:

	deactivate

To get back into the virtualenv use:

	workon test1

workon allows tab completion to see the available environments.

When the virtualenv is active, anything you pip install will be installed just for that virtualenv, not system wide. Once in the virtualenv, the environment is set to the python version you are using, so you can use either pip3 or pip.

See the [virtualenvwrapper documentation](https://virtualenvwrapper.readthedocs.org/en/latest/) for other commands to manage your virtual environments.

## Try out Jupyter and Pandas

If you want to get started with [Jupyter](https://jupyter.org/) and [Pandas](http://pandas.pydata.org/) you can just install them in your new virtualenv project (this will also install quite a few extra modules that these require):

	pip install jupyter
	pip install pandas

Start jupyter using:

	jupyter notebook
