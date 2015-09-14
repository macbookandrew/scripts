#Introduction

A collection of useful scripts/short snippets.

-----

#Linux

## Copy folder/file structure
- `find src/ -type d -exec mkdir -p dest/{} \; \ -o -type f -exec touch dest/{} \;`
	- Find directory (`-d`) under (`src/`) and create (`mkdir -p`) them under `dest/` or (`-o`) find files (`-f`) and `touch` them under `dest/`.

##Disk Usage

- `du -ch --max-depth 2 / | sort -hr` Recursively list all folders by size descending—good for finding directories using a lot of space.

##Find Version Number in All Files
- `find /home/ -name plugin.php -exec grep -H 'Version:' \{} \;` Search through entire subdirectory of `/home` for the version number of a plugin’s PHP file and show filename/path.
- `find /home/ -name plugin.php -exec grep -H 'Version:' \{} \; | grep -v 'Version: 2.0.0'` Search through entire subdirectory of `/home` all copies not matching version 2.0.0.
- Related: one-step command to update a plugin from a local folder: `cd ./  && sudo rm -r ./wp-content/plugins/plugin-folder && cp -r ~/public_html/plugin-folder ./wp-content/plugins/ && chown -R user:group ./wp-content/plugins/plugin-folder` (edit the intial `cd ./`, `plugin-folder`, and `user:group` to match as needed)

##Firewall: block a specific port to everybody except localhost
- `/sbin/iptables -I INPUT -p tcp --destination-port 2079 -j DROP && /sbin/iptables -I INPUT -s 127.0.0.1 -p tcp --destination-port 2079 -j ACCEPT && service iptables save`
    - Change port number as necessary
    - Originally used on CentOS 6; not tested on other distros

##Mount a “mounted-over” mount point

- `mkdir /old-root`
- `mount --bind / /old-root`
- More info: [SuperUser.com thread](http://superuser.com/a/200697)

##String Modification
- `sed "s/$/,new-field/" input.csv > output.csv` Add a field to the end of each row in a CSV file


##SSL Certificates
1. `openssl req -new -newkey rsa:4096 -nodes -sha256 -out keyname.csr -keyout keyname.key -subj "/C=US/ST=State Name/L=City Name/O=Organizational Unit/CN=site url or FQDN"` Create new CSR (4096 bytes) with prefilled information.
1. `openssl x509 -req -days 3650 -in keyname.csr -signkey keyname.key -out keyname.crt` Self-sign a CSR for 10 years
1. `openssl pkcs12 -export -out domain.name.pfx -inkey domain.name.key -in domain.name.crt` Convert to PFX for use on IIS servers
1. Cipher suite generator: [http://mozilla.github.io/server-side-tls/ssl-config-generator/](http://mozilla.github.io/server-side-tls/ssl-config-generator/)


-----

#Mac

##Enable/Disable FTP Server (OS X Yosemite)
1. `sudo -s launchctl load -w /System/Library/LaunchDaemons/ftp.plist` Enable the built-in FTP server
2. `sudo -s launchctl unload -w /System/Library/LaunchDaemons/ftp.plist` Disable the built-in FTP server

##Set symlink permissions
- `chmod -h <symlink-name>`

##Flush DNS Cache
- OS X 10.10.4+ (Yosemite): `dscacheutil -flushcache; sudo killall -HUP mDNSResponder`
- OS X 10.10.0-10.10.4 (Yosemite): `sudo discoveryutil udnsflushcaches`
- OS X 10.9 (Mavericks): `dscacheutil -flushcache; sudo killall -HUP mDNSResponder`
- OS X 10.7–10.8 (Lion–Mountain Lion): `sudo killall -HUP mDNSResponder`
- OS X 10.5–10.6 (Leopard–Snow Leopard): `sudo dscacheutil -flushcache`
