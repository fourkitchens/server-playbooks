Server Playbooks
========================

A collection of Ansible playbooks for use in setting up various servers.
Playbooks are a series of configuration steps and specifications for how the
server should be configured.

Executing the playbooks
---------------------------

### Setup Ansible

Playbooks require [Ansible][1] to execute them. It's really easy to setup, and
you can choose between running it on the same machine you're configuring, or a
remote machine. For a remote machine, all Ansible needs is the ability to establish
an SSH connection to it.

Generally, if you're looking for a quick time-saver for a one-time build of a
server, then you should set up Ansible and execute the playbook on the target
server. If you're a more serious server administrator who wants to maintain
clusters of machines, you should setup Ansible on a separate controller machine
or your personal machine.

You may refer to the setup guide on the Ansible homepage, however here are the
steps for setting it up on Ubuntu and immediately configuring it to use
localhost as the target server, the simplest configuration option:

    sudo aptitude -y install git python-jinja2 python-yaml python-paramiko python-software-properties
    add-apt-repository -y ppa:rquillo/ansible/ubuntu
    aptitude update
    aptitude install ansible
    echo "localhost" > /etc/ansible/hosts

You can now test by typing:

    ansible -c local -m ping all

You should see:

    127.0.0.1 | success >> {
      "ping": "pong"
    }

### Run the play

The plays are organized into directories, so for example, __ubuntu-12.04-lamp-dev__
contains all the settings and configuration for the Ubuntu 12.04 LAMP Dev server
build. At the moment this is the only one, but more could be added soon.

You must copy the __vars/default-settings.yml__ file to the base folder of the
play, and then edit it with your specific requirements. It's really easy to
understand and contains all the configuration that will be customized from the
default Ubuntu package setting.

    cd ubuntu-12.04-lamp-dev
    cp ./vars/settings-default.yml ./settings.yml

You have some options when executing a play. For example, you may want a LAMP
server but not drush or an ftp server. The parts of the play that setup these
optional packages are tagged as such.

By executing the following, it will setup only the commonly used components:

    ansible-playbook -c local --tags="common" ./setup.yml

You can add drush and ftp by doing:

    ansible-playbook -c local --tags="common,drush,ftp" ./setup.yml

Conventions used in playbooks
---------------------------

- The setup.yml file contains the main sequence of actions and tasks.
- When a configuration file is introduced by the playbook, i.e. isn't
  a pre-existing one, it's found in the __files__ subdirectory and is transferred
  using the 'copy' action.
- Files that already exist on the server, that we are modifying, are found
  in __templates__ and have Jinja2-style variable substitution. They are
  transferred using Ansible's 'template' action.
- Every value in a configuration file that is modified from the default will
  contain a variable substitution, so you know that looking in the
  __vars/settings-default.yml__ file will give you a complete overview of all the
  configuration that is modified from the server package default.

Ubuntu 12.04 LAMP Dev Server
---------------------------

Found in folder __/ubuntu-12.04-lamp-dev__

Packages tagged 'common': Apache, MySQL, APC cache, PHP.

Other optional tags:

    +--------------------------------------------------------------+
    | drush      | Drupal shell.                                   |
    +--------------------------------------------------------------+
    | ftp        | VSFtp daemon                                    |
    +--------------------------------------------------------------+
    | nodejs     | node.js and npm (latest from ppa)               |
    +--------------------------------------------------------------+
    | redis      | redis server                                    |
    +--------------------------------------------------------------+
    | css        | SASS, Susy, Compass, Respond-to                 |
    +--------------------------------------------------------------+
    | dotcloud   | The CLI for interacting with dotcloud hosting   |
    +--------------------------------------------------------------+

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