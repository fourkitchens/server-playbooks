Ubuntu 10.04 LAMP Dev Server
---------------------------

This server is configured with standard LAMP for a single docroot. It was used for a client that we no longer work with, who had a production server running Ubuntu 10.04. This playbook is no longer maintained. Docroot is at /var/dev.

Use `./run-local-all` to run all the tags, otherwise directly run the parts you
need using:

    ansible-playbook -c local --tags="common,..." ./setup.yml

Packages tagged `common`: Apache, MySQL, PHP.

Other optional tags:

    +--------------------------------------------------------------+
    | drush      | Drupal shell.                                   |
    +--------------------------------------------------------------+
    | memcached  | Memcached daemon and memcache PECL extension    |
    +--------------------------------------------------------------+
