https://github.com/thuannvn/ansible-drupal-roles/blob/master/roles/mysql/scripts/mysql_pwd_reset.sh

# Drupal+Nginx+PHP-FPM Deployment
This ansible repo is derived & fixed mysql roles from https://github.com/axai-mx/ansible-drupal-roles
- Requires Ansible 1.8 or newer
- Expects Ubuntu 14.04 or CentOS/RedHat 6.5 hosts

These playbooks (found in sample_yml) deploy a simple all-in-one configuration
of the popular Drupal software platform and CMS, frontend by the Nginx web server
and the PHP-FPM process manager.

The playbooks will configure MySQL, Drupal, Nginx, and PHP-FPM. When the run
is complete, you can access server (http://192.168.88.88/) to begin the Drupal
configuration. You can also edit your `hosts` file to access the server with a
domain name.

Then run the playbook with a remote server instead of a vagrant VM you need to
create a `hosts` file and a `site.yml` file and then run the `ansible-playbook`
command, like this:

    ansible-playbook -i hosts site.yml

There are example hosts and site.yml files in the sample_yml folder.

## TODO

Here are some ideas for ways that these playbooks could be extended:

- Use our own nginx.conf based on (epoll, multi_accept, file_cache):
  - http://www.slashroot.in/nginx-web-server-performance-tuning-how-to-do-it
  - http://www.codestance.com/tutorials-archive/nginx-tuning-for-best-performance-255
  - https://github.com/h5bp/server-configs-nginx/blob/master/nginx.conf
  - https://www.digitalocean.com/community/tutorials/how-to-optimize-nginx-configuration
- add xhprof to the php role
- test debian support
- handle Drupal upgrades automatically.
- add goaccess with geoip (http://dev.maxmind.com/geoip/legacy/install/country/)

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.

## Other Defined Roles

### php7-fpm

PHP 7 for ubuntu 14.04.

### hhvm

HHVM serves as a replacement for php-fpm role. It is already configured as a
fastcgi server. HHVM is only compiled for 64bit machines and right now this role
is only for ubuntu 14.04.

### syslog

The syslog module disables the watchdog (dblog) module and enables the syslog
module for each of your sites. It depends on your sites already being installed.
It will also configure syslog (`/etc/rsyslog.conf`) to log all drupal events
to `/var/log/drupal.log`

### mailer

A role to allow the server to send emails. It uses postfix and the default
distribution configuration.

### solr

A role to run solr using the provided jetty example, which is the recommended 
method instead of using tomcat or full jetty.

http://lucene.472066.n3.nabble.com/difference-between-apache-tomcat-vs-Jetty-td4096680.html
