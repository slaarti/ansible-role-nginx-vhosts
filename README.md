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
Each virtual host can (and sometimes must) have the following elements,
most of which are just arguments to statements of the same name:

*   `name`: **Required.** Used in the name of the configuration file.

*   `listen`: **Optional.** Can be either a single string or a list of
    strings. If you pass a list here, each list item gets its own `listen`
    statement.

*   `server_name`: **Required.** Can be either a single string or a list
    of strings. If a list, then list items will be space-separated in
    a single `server_name` statement.

*   `root`: **Required.**

*   `index`: **Optional.**

*   `error_page`: **Optional.**

*   `access_log`: **Optional.**

*   `error_log`: **Optional.**

*   `return`: **Optional.**

*   `extra_parameters`: **Optional.** A string for you to put in whatever
    other miscellaneous config you require for this server. If you need
    more than one line, you can use the `|` block literal notation.

*   `locations`: **Optional.** Takes a list of hashes. Each list item is
    a `location` stanza. The hash uses the following elements, most of
    which work the same way as already described:

    *   `url`: **Required.** The URI that this location is for.

    *   `root`: **Optional.** (Note that this is different from at the
        vhost level, where it's required.)

    *   `alias`: **Optional.**

    *   `index`: **Optional.**

    *   `error_page`: **Optional.**

    *   `access_log`: **Optional.**

    *   `error_log`: **Optional.**

    *   `return`: **Optional.**

    *   `extra_parameters`: **Optional.** A string for you to put in
        whatever other miscellaneous config you require for this location.
        If you need more than one line, you can use the `|` block literal
        notation.

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
