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
## Continue working
```
# install requirements
pip3 install -r requirements.txt

# setup install
python3 setup.py install

# setup for development
python3 setup.py develop
python3 setup.py develop --uninstall
```
