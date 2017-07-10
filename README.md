[![Build Status](http://img.shields.io/travis/cchurch/ansible-role-win-stunnel.svg)](https://travis-ci.org/cchurch/ansible-role-win-stunnel)
[![Galaxy](http://img.shields.io/badge/galaxy-cchurch.win--stunnel-blue.svg)](https://galaxy.ansible.com/cchurch/win-stunnel/)

Win-STunnel
===========

Install and configure [stunnel](https://www.stunnel.org/) on Windows.

Role Variables
--------------

Use the following variables to configure stunnel. Configuration values that
should be a literal `"yes"` or `"no"` should be specified as strings instead of
YAML boolean values.

- `stunnel_global_options`: A dictionary of global options for `stunnel.conf`.
  Default is `{}`, which does not specify any global options.
- `stunnel_services`: A dictionary of services to configure in `stunnel.conf`.
  The value of each service entry should be a dictionary of configuration
  options and values for that service. Default is `{}`, which does not define
  any services. At least one service should be defined.

The following variables may be used for more advanced configuration:

- `stunnel_conf_template`: Specify an alternate template to use to configure
  `stunnel`. The default is `"stunnel.conf.j2"`, which builds a configuration
  based on `stunnel_global_options` and `stunnel_services` defined above.
- `stunnel_download_url`: Specify an alternate URL to download the `stunnel`
  installer; default is
  `"https://www.stunnel.org/downloads/stunnel-5.41-win32-installer.exe"`.
- `stunnel_force_install`: Force installation of `stunnel` even if registry keys
  indicate it is already installed; Default is `false`.

Example Playbook
----------------

The following example playbook installs `stunnel` and adds a service to forward
unencrypted local SMTP connections on port `2525` to `smtp.gmail.com` port `465`:

    - hosts: windows
      roles:
        - role: cchurch.win-stunnel
          stunnel_services:
            'gmail-smtp':
              client: 'yes'
              accept: 2525
              connect: smtp.gmail.com:465
              delay: 'yes'

License
-------

BSD

Author Information
------------------

Chris Church <chris@ninemoreminutes.com>
