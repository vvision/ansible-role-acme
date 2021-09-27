# ansible-role-acme

Installs acme.sh on Debian servers.
Also allow configuration of both OVH DNS API and GANDI DNS API,
as well as issuing certificate with this 2 modes.

## Requirements

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    acme_code_version: HEAD

Code version to use when installing acme.sh from its git repository.
Available options are `HEAD`, a tag name (3.0.0), a branch name or a SHA1 hash.

    acme_account_email:

Email to register account to Let's Encrypt.
Used by `--accountemail` when installing acme.sh.

    acme_install_dir: /home/acme/acme

Directory to install acme.sh scripts.
Used by `--home` when installing acme.sh.

    acme_config_folder: /home/acme/acme-config

Directory to store acme.sh configuration.
Used by `--config-home` when installing acme.sh.

#### OVH DNS Configuration

OVH DNS configuration is optional and disabled by default.

As described in [acme.sh - How to use OVH domain api](https://github.com/acmesh-official/acme.sh/wiki/How-to-use-OVH-domain-api).
To automate the whole process, it is assumed that we already have application key, application secret and consumer key.

Configuration will be persisted in both `/etc/environment` file and `/etc/profile.d/` directory.

    acme_configure_ovh_dns_api: false

Whether to configure OVH DNS API environment variables.

    acme_ovh_end_point: ovh-eu

OVH DNS API endpoint.

    acme_ovh_application_key:

Application key for OVH DNS API.

    acme_ovh_application_secret:

Application secret for OVH DNS API.

    acme_ovh_consumer_key:

Consumer key for OVH DNS API.

#### Gandi DNS Configuration

Gandi DNS configuration is optional and disabled by default.

Configuration will be persisted in both `/etc/environment` file and `/etc/profile.d/` directory.

As described in [acme.sh - 18. Use Gandi LiveDNS API](https://github.com/acmesh-official/acme.sh/wiki/dnsapi#18-use-gandi-livedns-api).

    acme_configure_gandi_dns_api: false

Whether to configure Gandi DNS API environment variables.

    acme_gandi_livedns_key:

Gandi LiveDNS API key.

#### Certificate configuration

Certificate configuration is optional and disabled as `certs_to_issue` is empty by default.

    is_test: false

Whether to use Let`s Encrypt test/staging server.

    acme_dest_folder: /etc/ssl/live

Directory to store acme.sh configuration.

    cert_file_name: cert.pem

Filename for certificate file.

    key_file_name: privkey.pem

Filename for key file.

    fullchain_file_name: chain.pem

Filename for fullchain file.

    certs_to_issue:

List of certificate to issue. Empty by default.
Example:

````
certs_to_issue:
  - {
    domains: [ test-cert-1.example.com, test-cert-2.example.com ],
    install_dir: test-cert.example.com,
    key_length: 4096,
    dns: dns_gandi_livedns,
    reloadcmd: service apache2 force-reload
  }
````

Parameters are explained below.

###### Certificate configuration

    domains: [ test-cert-1.example.com, test-cert-2.example.com ]

List of domains to issue.

    install_dir: test-certs

In which directory to install certificates. Built like ``<acme_dest_folder>/<install_dir>``

    key_length: 4096

Key length.

    dns: dns_gandi_livedns

Choose between ``dns_gandi_livedns`` and ``dns_ovh``.

    reloadcmd: service apache2 force-reload

Command to be executed after certificate renewal.

## Dependencies

None.

## License

MIT

## Author Information

This role was created in 2021 by Victor Voisin.
