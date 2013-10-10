# sugar-dev-box

## Requirements

* [VirtualBox](https://www.virtualbox.org)

* [Vagrant 1.1+](http://vagrantup.com)

## Setup

First, build the virtual machine. This might take a few minutes:

    host $ git clone https://github.com/elektronaut/sugar-dev-box.git
    host $ cd sugar-dev-box
    host $ vagrant up

Clone your Sugar fork into the same directory:

    host $ git clone git@github.com:<username>/sugar.git

Vagrant mounts this directory as _/vagrant_ within the virtual machine. Log in with:

    host $ vagrant ssh
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)
    ...
    vagrant@sugar-dev-box:~$

On the VM, run Bundler to install the rest of the dependencies, create the configuration
and populate the database with:

    vm $ cd /vagrant/sugar
    vm $ bundle
    vm $ rake db:migrate
    vm $ rake db:migrate RAILS_ENV=test

## Starting the development server

    host $ vagrant ssh
    vm $ cd /vagrant/sugar
    vm $ sunspot-solr start
    vm $ rails server

The development server is now accessible on [localhost:3000](http://localhost:3000/).

## Running the tests

    host $ vagrant ssh
    vm $ cd /vagrant/sugar
    vm $ RAILS_ENV=test rspec spec

## Recommended Workflow

The recommended workflow is

* edit in the host computer and

* run and test within the virtual machine.

This workflow is convenient because in the host computer you normally have your editor of choice fine-tuned, Git configured, and SSH keys in place.

## Virtual Machine Management

When done just log out with `^D` and suspend the virtual machine

    host $ vagrant suspend

then, resume to hack again

    host $ vagrant resume

Run

    host $ vagrant halt

to shutdown the virtual machine, and

    host $ vagrant up

to boot it again.

You can find out the state of a virtual machine anytime by invoking

    host $ vagrant status

Finally, to completely wipe the virtual machine from the disk **destroying all its contents**:

    host $ vagrant destroy # DANGER: all is gone

Please check the [Vagrant documentation](http://docs.vagrantup.com/v2/) for more information on Vagrant.

## Credits

Based on [rails-dev-box](https://github.com/rails/rails-dev-box) by Xavier Noria

## License

Released under the MIT License.
Original work Copyright (c) 2012-ω Xavier Noria
Modified work Copyright 2013 Inge Jørgensen
