Server Playbooks
========================

A collection of Ansible playbooks for use in setting up servers.

Ubuntu 12.04 LAMP Dev Server
--------------------------

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
