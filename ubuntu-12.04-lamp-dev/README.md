Ubuntu 12.04 LAMP Dev Server
---------------------------

Use `./run-local-all` to run all the tags, otherwise directly run the parts you
need using:

    ansible-playbook -c local --tags="common,..." ./setup.yml

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

Packages tagged `common`: Apache, MySQL, APC cache, PHP.

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
