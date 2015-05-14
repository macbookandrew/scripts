#Introduction

A collection of useful scripts/short snippets.

-----

#Linux

##Disk Usage

- `du -ch --max-depth 2 / | sort -hr` Recursively list all folders by size descending—good for finding directories using a lot of space.

##Mount a “mounted-over” mount point

- `mkdir /old-root`
- `mount --bind / /old-root`
- More info: [SuperUser.com thread](http://superuser.com/a/200697)


##SSL Certificates
1. `openssl req -new -newkey rsa:4096 -nodes -sha256 -out keyname.csr -keyout keyname.key -subj "/C=US/ST=State Name/L=City Name/O=Organizational Unit/CN=site url or FQDN"` Create new CSR (4096 bytes) with prefilled information.
2. Cipher suite generator: [http://mozilla.github.io/server-side-tls/ssl-config-generator/](http://mozilla.github.io/server-side-tls/ssl-config-generator/)
