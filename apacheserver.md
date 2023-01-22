# Apache server

## installation and enabling

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
