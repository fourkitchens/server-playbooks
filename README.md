Server Playbooks
========================

A collection of Ansible playbooks for use in setting up various servers.

Executing the playbooks
---------------------------

### Setup Ansible

Playbooks require [Ansible][1] to execute them. It's really easy to setup, and
you can choose between running it on the same machine you're configuring or a
remote machine - as long as you can establish an SSH connection between them, it
will work fine.

Generally, if you're looking for a quick time saver for a one-time build of a
server, then you should set it up and run it on the target server. If you're a
more serious server administrator who wants to maintain clusters of machines,
you should setup Ansible on a separate controller machine or your personal machine.

You may refer to the setup guide on the Ansible homepage, however here are the
steps for setting it up on Ubuntu 12.04 and immediately configuring it to use
localhost as the target server, the simplest configuration option:

    sudo aptitude -y install git python-jinja2 python-yaml python-paramiko
    git clone git://github.com/ansible/ansible.git
    cd ./ansible
    git checkout 0.4.1
    source ./hacking/env-setup
    sudo mkdir /etc/ansible
    sudo echo "127.0.0.1" > /etc/ansible/hosts

You can now test by typing:

    ansible -c local -m ping all

You should see:

    127.0.0.1 | success >> {
        "ping": "pong"
    }

###

Once Ansible is setup, you can execute the play in one of two ways, depending
on whether you want it to run on the current machine or against a remote one.

The playbook is configured to run against all hosts, this is easily configurable
but executing the following will run it against everything in /etc/ansible/hosts:

    ansible-playbook ./setup.yml

To run the play on the current machine that you've got Ansible setup on, a variable
needs to be set. There is a simple two line bash script that takes care of this
and executes the play, so you can just do:

    cd <playbook dir>
    ./run-local

Conventions used in playbooks
---------------------------

- The setup.yml file contains the main sequence of actions.

- When a configuration file is introduced by the playbook, i.e. isn't
  a pre-existing one, it's found in the /files subdirectory and is transferred
  using the 'copy' action.
- Files that already exist on the server, that we are modifying, are found
  in /templates and have Jinja2-style variable substitution. They are
  transferred using Ansible's 'template' action.
- Every value in a configuration file that is modified from the default will
  contain a variable substitution, so you know that looking in the
  vars/settings-default.yml file will give you a complete overview of all the
  configuration that is modified from the server package default.

Ubuntu 12.04 LAMP Dev Server
---------------------------

Packages: Apache, MySQL, APC cache, PHP, Drush

This server is configured for multiple developers who need to work on many
projects simultaneously. The most notable piece of configuration is the way
Apache is setup, it has a variable document root. This allows a developer to
organise their home folder in the following way:

    /home/username/www/project1
    /home/username/www/project2
    /home/username/www/project3

And access each of the sites by going to URLs formatted as follows:

    http://username.project1.example.com/
    http://username.project2.example.com/
    http://username.project3.example.com/

[1]: http://ansible.github.com/ "Ansible"