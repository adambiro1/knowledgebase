# Apache server

man pages:

```
man httpd.conf

man httpd.service
```
## installation and enabling CentOSStream

install on CentOSStream:
```
sudo dnf install httpd
```
start it:
```
sudo systemctl start httpd
```
allow communication to port 80:
```
sudo firewall-cmd --add-port=80/tcp
```
edit config file:

*/etc/httpd/conf/httpd.conf*

add content to the web page in: 

*/var/www/html*

if you do not want to see default page uncomment everything in:

*/etc/httpd/conf.d/welcome.conf*
