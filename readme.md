#Introduction

A collection of useful scripts/short snippets.

-----

#Linux

##Disk Usage

1. `du -ch --max-depth 2 / | sort -hr` Recursively list all folders by size descending—good for finding directories using a lot of space.

##SSL Certificates
1. `openssl req -new -newkey rsa:4096 -nodes -sha256 -out keyname.csr -keyout keyname.key -subj "/C=US/ST=State Name/L=City Name/O=Organizational Unit/CN=site url or FQDN"` Create new CSR (4096 bytes) with prefilled information.
2. Cipher suite generator: [http://mozilla.github.io/server-side-tls/ssl-config-generator/](http://mozilla.github.io/server-side-tls/ssl-config-generator/)

-----

#Mac

##Enable/Disable FTP Server (OS X Yosemite)
1. `sudo -s launchctl load -w /System/Library/LaunchDaemons/ftp.plist` Enable the built-in FTP server
2. `sudo -s launchctl unload -w /System/Library/LaunchDaemons/ftp.plist` Disable the built-in FTP server
