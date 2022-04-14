ACME
=========

A role to deploy ACME in a Docker container to issue and renew a Let's Encrypt certificate.<br>
***Please consider that this playbook is defined to deploy only one certificate!***

Requirements
------------

- Docker

Role Variables
--------------

For all variables please see `defaults/main.yml`.

    generic_acme_issue_domain:
    - example.tld

    generic_acme_priv_key_path

If you already have a private key to generate Let's Encrypt certificates, you can import your private key by set the path to your key.

Dependencies
------------

None

Example Playbook
----------------

    ---
    - hosts: all
      roles:
        - generic_acme_role