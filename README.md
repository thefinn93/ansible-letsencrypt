# ansible-letsencrypt
An ansible role to generate TLS certificates and get them signed by LetsEncrypt's CA. This has been
tested on Debian Jessie. If you successfully run it on other systems, please let me know.

# Usage
First, read LetsEncrypt's TOS and EULA. Only proceed if you agree to them.

The following variables are available:

`letsencrypt_agree_tos` (required) needs to be set to `yes` or `true` once you have read and agree to the LetsEncrypt TOS.

`letsencrypt_agree_eula` (required) needs to be set to `yes` or `true` once you have read and agree to the LetsEncrypt EULA.

`letsencrypt_email` (required) needs to be set to your email address. LetsEncrypt wants it.

`letsencrypt_cert_domain` should be set to your domain. It defaults to the value of `ansible_fqdn`

`letsencrypt_install_directory` should probably be left alone, but if you set it, it will change where the letsencrypt program is installed.

# Example Playbook
```
---
 - hosts: tls_servers
   user: root
   roles:
     - role: letsencrypt
       letsencrypt_agree_tos: yes
       letsencrypt_agree_eula: yes
       letsencrypt_email: user@example.net
```
