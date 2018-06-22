# python

## pyvenvs
```
# create the pyvenv
python3 -m venv ~/pyvenvs/projname-dev

# souce the environment
# this should add (projname-dev) to your prompt
source ~/pyvenvs/projname-dev/bin/activate
```
## (or virtualenv)
```
# create the virtualenv
virtualenv projname-dev

# source the environment
# this should add (projname-dev) to your prompt
source penv/bin/activate
```
## Install with pip
```
# Install
pip3 install .

# Developer installation of package
pip3 install -e .
pip3 uninstall .

# install specific requirements file
pip3 install -r requirements.txt
```
If your project has dependencies, then "pip install -e ." installs them with pip, while "setup.py develop" installs them with easy_install.  Therefore, "setup.py develop" may cause problems when dependencies use custom git URLs, attached egg identifiers, etc.

## Install with setup.py
```
python3 setup.py install
python3 setup.py develop
python3 setup.py develop --uninstall
```
Develop creates an .egg-link file in the site-packages directory, which points back to the location of the project files. The same path is also added to the easy-install.pth file in the same location. Uninstalling with setup.py develop -u removes that link file again.

## Running Tests
```
# run tests
python3 setup.py test
# run specifically named test
python3 setup.py test --addopts '-k testname'
```
