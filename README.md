# ansible-letsencrypt
An ansible role to generate TLS certificates and get them signed by Let's Encrypt.

Currently attempts first to use the `webroot` authenticator, then if that fails to create certificates,
it will use the standalone authenticator. This is handy for generating certs on a fresh machine before
the web server has been configured or even installed.

I've tested this on a couple of Debian Jessie boxes, if you test it on other things please let me know
the results (positive or otherwise) so I can document them here/fix the issue.

# Usage
First, read Let's Encrypt's TOS and EULA. Only proceed if you agree to them.

The following variables are available:

`letsencrypt_webroot_path` is the root path that gets served by your web server. Defaults to `/var/www`.

`letsencrypt_email` needs to be set to your email address. Let's Encrypt wants it. Defaults to `webmaster@{{ ansible_fqdn }}`.

`letsencrypt_cert_domains` is a list of domains you wish to get a certificate for. It defaults to a single item with the value of `{{ ansible_fqdn }}`.

`letsencrypt_install_directory` should probably be left alone, but if you set it, it will change where the letsencrypt program is installed.

`letsencrypt_server` sets the auth server. If you're in the early beta you will have received the URL of a server,
set it here.


# Example Playbook
```
---
 - hosts: tls_servers
   user: root
   roles:
     - role: letsencrypt
       letsencrypt_webroot_path: /var/www/html
       letsencrypt_email: user@example.net
       letencrypt_server: https://acme-v01.api.letsencrypt.org/directory  # Only works if your domain is whitelisted
       letsencrypt_cert_domains:
        - www.example.net
        - example.net
```
