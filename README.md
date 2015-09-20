# Nginx Virtual Hosts role

This Ansible role configures virtual hosts for [Nginx][], in the manner
that Debian intends it. It does *not* install Nginx or handle basic
configuration for it. For that, this role depends on the
[`geerlingguy.nginx` role][geerlingguy].

[Nginx]: http://nginx.org/
[geerlingguy]: https://github.com/geerlingguy/ansible-role-nginx

Role Variables
--------------

    nginx_virtual_hosts: []

A list of hashes containing configuration information for virtual hosts.

Dependencies
------------

As noted above, this role depends on `geerlingguy.nginx` role, to handle
installing and configuring Nginx.

Example Playbook
----------------

    - hosts: servers
      roles:
        - geerlingguy.nginx
        - slaarti.nginx-vhosts
      vars:
        - nginx_virtual_hosts:
          - name: "default"
            listen: "80 default"

License
-------

Unlicense; see the LICENSE file.

Author Information
------------------

Chris Pinard <slaarti@gmail.com>
