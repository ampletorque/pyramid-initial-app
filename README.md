VAGRANT:
________

Install Vagrant for your OS from:

    http://www.vagrantup.com/downloads

    $ vagrant init ubuntu/trusty64

use your favorite editor to edit Vagrantfile
add this line to the Vagrant.configure section:

    config.vm.network "forwarded_port", guest: 6543, host: 6543

    $ vagrant up
    $ vagrant ssh
    vagrant@vagrant-ubuntu-trusty-64:~$ cd ~
    vim .profile

add the following line to the bottom:

    export VENV=/vagrant/projects/quick_tutorial/env

back at the command-line..

    vagrant@vagrant-ubuntu-trusty-64:~$ export VENV=/vagrant/projects/quick_tutorial/env

do this the first time. the next time you log in it will be run for you. :)

    vagrant@vagrant-ubuntu-trusty-64:~$ cd /vagrant

This is your shared folder. Vagrant is set up.

PYTHON:
_______

    vagrant@vagrant-ubuntu-trusty-64:~$ sudo apt-get update
    vagrant@vagrant-ubuntu-trusty-64:~$ sudo apt-get upgrade
    vagrant@vagrant-ubuntu-trusty-64:~$ sudo apt-get install python3.4-venv

PYRAMID:
________

    vagrant@vagrant-ubuntu-trusty-64:~$ mkdir projects
    vagrant@vagrant-ubuntu-trusty-64:~$ mkdir quick_tutorial
    vagrant@vagrant-ubuntu-trusty-64:~$ cd projects/quick_tutorial
    vagrant@vagrant-ubuntu-trusty-64:~$ python3 -m venv env --without-pip
    vagrant@vagrant-ubuntu-trusty-64:~$ cd env
    vagrant@vagrant-ubuntu-trusty-64:~$ source bin/activate
    vagrant@vagrant-ubuntu-trusty-64:~$ wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py -O - | $VENV/bin/python
    vagrant@vagrant-ubuntu-trusty-64:~$ $VENV/bin/easy_install "pyramid==1.5.7"
    vagrant@vagrant-ubuntu-trusty-64:~$ $VENV/bin/easy_install nose webtest deform sqlalchemy \
      pyramid_chameleon pyramid_debugtoolbar waitress \
      pyramid_tm zope.sqlalchemy

APP:
____

    vagrant@vagrant-ubuntu-trusty-64:~$ $VENV/bin/pcreate --scaffold starter scaffolds
    vagrant@vagrant-ubuntu-trusty-64:~$ cd scaffolds
    vagrant@vagrant-ubuntu-trusty-64:~$ $VENV/bin/pserve development.ini --reload

open localhost:6543 from your web browser

PYRAMID DEBUG TOOLBAR:
______________________

add line:

    debugtoolbar.hosts = 192.168.1.1 0.0.0.0/0

to development.ini file to allow access to debug toolbar to all IP addresses (in our case due to forwarded port in vagrant). More info at:

    http://docs.pylonsproject.org/projects/pyramid-debugtoolbar/en/latest/index.html#overview
