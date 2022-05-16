# ACME

A role to deploy ACME in a Docker container to issue, renew and deploy a Let's Encrypt certificate.<br>
By default the role is designed to deploy certificates to a nginx for reverse proxy purpose like in role `generic_reverse_proxy_role` but can also be used for other purposes.<br><br> 
***Note*** Please consider that this playbook is defined to deploy only one certificate!

## Requirements

- Docker

## Role Variables

For all variables please see `defaults/main.yml`.

### Mandatory

    generic_acme_issue_domain:
    - example.tld

List of domains for which the certificate is valid. The first entry will be used for the name of the certificate.

## Additional information

The default deployment method of this role is a docker hook to deploy the certificate to a container.<br>

If you want to deploy your certificate to a container the destination container needs to have label with your certificate name.

## Dependencies

None

## Example Playbook
    ---
    - hosts: all
      roles:
        - generic_acme_role
      vars:
        generic_acme_issue_domain:
          - example.tld

[examples/deploy-acme.yml](examples/deploy-acme.yml):
Deploy a certificate for example.tld to a nginx container with label `example.tld`.

    ---
    - hosts: all
      roles:
        - generic_acme_role
      vars:
        generic_acme_issue_domain:
          - example.com
          - example.org
        generic_acme_priv_key_path: /home/user/account.key
        generic_acme_container_additional_env:
            DEPLOY_DOCKER_CONTAINER_LABEL: "sh.acme.autoload.domain=example.com"
            DEPLOY_DOCKER_CONTAINER_KEY_FILE: "/etc/ssl/certsexample.org/key.pem"
            DEPLOY_DOCKER_CONTAINER_CERT_FILE: "/etc/ssl/certs/example.org/cert.pem"
            DEPLOY_DOCKER_CONTAINER_CA_FILE: "/etc/ssl/certs/example.org/ca.pem"
            DEPLOY_DOCKER_CONTAINER_FULLCHAIN_FILE: "/etc/ssl/certs/example.org/full.pem"
            DEPLOY_DOCKER_CONTAINER_RELOAD_CMD: "systemctl restart apache2"
            DEPLOY_DOCKER_CONTAINER_FQDN: "example.com"

[examples/deploy-acme-apache.yml](examples/deploy-acme-apache.yml):
Deploy a certificate for example.com and example.org apache container with label `example.com`.
