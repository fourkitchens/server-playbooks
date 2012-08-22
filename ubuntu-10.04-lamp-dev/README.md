Ubuntu 10.04 LAMP Dev Server
---------------------------

This server is configured with standard LAMP for a single docroot. APC is not
installed, rather eAccellerator is built.

Use `./run-local-all` to run all the tags, otherwise directly run the parts you
need using:

    ansible-playbook -c local --tags="common,..." ./setup.yml

Packages tagged `common`: Apache, MySQL, PHP.

Other optional tags:

    +--------------------------------------------------------------+
    | drush      | Drupal shell.                                   |
    +--------------------------------------------------------------+
