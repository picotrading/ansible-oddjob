oddjob
======

Role which helps to install oddjob - D-Bus service which runs odd jobs on behalf
of client applications.


Example
-------

```
---

# Default usage
- hosts: myhost1
  roles:
    - oddjob

# Example of how to install an additional oddjob helper
- hosts: myhost2
  vars:
    # Install oddjob-mkhomedir package
    oddjob_helper:
      - oddjob-mkhomedir
  roles:
    - oddjob

# Example of how to configure oddjob
- hosts: myhost3
  vars:
    # Simply overwrite this variable with new configuration
    oddjob_config:
      oddjobconfig:
        ...
        ...
  roles:
    - oddjob
```


Role variables
--------------

List of variables used by the role:

```
# Package to be installed (you can force a specific version here)
oddjob_pkg: oddjob

# Helper packages to be installed (you can force a specific version here)
oddjob_helper_pkg: []

# Default jobd config
oddjob_config:
  oddjobconfig:
    'service name="com.redhat.oddjob"':
      'object name="/com/redhat/oddjob"':
        'interface name="com.redhat.oddjob"':
          'method name="listall"':
            'allow min_uid="0" max_uid="0"': null
          'method name="list"':
            allow: null
          'method name="quit"':
            'allow user="root"': null
          'method name="reload"':
            'allow user="root"': null
    'include ignore_missing="yes"': /etc/oddjobd.conf.d/*.conf
    'include ignore_missing="yes"': /etc/oddjobd-local.conf
```


Dependencies
------------

* [Config Encoder Macros](https://github.com/picotrading/config-encoder-macros)


License
-------

MIT


Author
------

Jiri Tyr
