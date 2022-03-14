ACME
=========

A role to deploy ACME in a Docker container to issue and renew Let's Encrypt certificates.

Requirements
------------

- Docker

Role Variables
--------------

For all variables please see `defaults/main.yml`.

    generic_acme_issue_domain:
    - [ "test.test.com" ]
    - [ "test2.test.com", "test3.test.com" ]

Each list represents one certificate. Multiple domains per certificate are defined like the second entry.

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