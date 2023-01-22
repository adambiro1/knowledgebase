# Apache server

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

add content to the web page in: 

*/var/www/html*
