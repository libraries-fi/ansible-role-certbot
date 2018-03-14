Kifi Certbot
============

Creates Let's encrypt certificates.

Requirements
------------

None.

Role Variables
--------------

    certbot_disable_certbot_cron: whether to disable the certbot cron
    that comes with the Debian package. Useful when you want to use
    the cron in the geerlingguy.certbot role instead.

In addition to this all the variables from the geerlingguy.certbot
role are available.

Dependencies
------------

ajsalminen.file_sync
geerlingguy.certbot

Example Playbook
----------------

If you just want to create brand new certificates for your domain:

```
- hosts: webservers

  roles:
    - role: kifi.certbot
      certbot_disable_certbot_cron: yes
      certbot_create_standalone_stop_services:
        - nginx
      certbot_create_if_missing: yes
      certbot_admin_email: example@example.com
      certbot_certs:
        - domains:
            - example.com
```

If you want to copy certificates from already running server in order to setup a clone:

```
- hosts: webservers

  roles:
    - role: kifi.certbot
      site_content_sync: yes
      certbot_host_with_certs: example.com
      certbot_create_standalone_stop_services:
        - nginx
      certbot_create_if_missing: yes
      certbot_admin_email: example@example.com
      certbot_certs:
        - domains:
            - example.com
```

License
-------

MIT

Author Information
------------------

Libraries.fi
