## IPv6 網站架設 && 憑證

[Install Let's Encrypt on CentOS 7 running apache | Snel.com](https://www.snel.com/support/install-lets-encrypt-centos-7/)

sudo yum install epel-release mod_ssl certbot

mod_ssl for apache

- `certbot certonly --webroot -w /var/www/html -d mydomainname.dynv6.net --email mymail@student.nqu.edu.tw --agree-tos`