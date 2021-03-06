gitlab-vm-lab
=============

This role is intended to automate setting up quickly a Gitlab-CE instance on a Fedora Cloud 34 VM. 
Originally, GitLab does not support setting up the gitlab-ce package on Fedora 34 (the initial repo install script fails). However, we may still use the package for RHEL 8.

Requirements
------------

* `ansible.posix`
* additional packages ..

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
