# Apache HTTPD Web Server Installation & Configuration on Linux

## Project Overview

This project demonstrates how to install and configure the Apache (HTTPD) Web Server on a Linux system.

The project includes:

- Installing Apache HTTP Server
- Starting and enabling the service
- Creating a custom document root
- Setting ownership and permissions
- Configuring Apache
- Configuring SELinux
- Verifying web server functionality

---

## Technologies Used

- Rocky Linux / RHEL / CentOS
- Apache HTTP Server (httpd)
- SELinux
- Linux Terminal

---

## Project Architecture

Client Browser
       |
       |
Apache HTTP Server
       |
Custom Document Root (/webdata)
       |
index.html

---

## Installation

### Install Apache

```bash
sudo yum install httpd -y
```

### Start Service

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

### Verify

```bash
systemctl status httpd
```

---

## Create Custom Document Root

```bash
sudo mkdir /webdata
```

### Change Ownership

```bash
sudo chown apache:apache /webdata
```

### Set Permissions

```bash
sudo chmod 750 /webdata
```

---

## Create Sample Web Page

```bash
sudo vi /webdata/index.html
```

```html
<!DOCTYPE html>
<html>
<head>
<title>Apache Web Server</title>
</head>

<body>

<h1>Apache HTTP Server Successfully Configured</h1>

<p>Linux Web Server Project</p>

</body>
</html>
```

---

## Configure Apache

Edit:

```
/etc/httpd/conf/httpd.conf
```

Change

```
DocumentRoot "/var/www/html"
```

to

```
DocumentRoot "/webdata"
```

Also update

```
<Directory "/webdata">

AllowOverride None
Require all granted

</Directory>
```

---

## Restart Apache

```bash
sudo systemctl restart httpd
```

---

## Configure SELinux

```bash
sudo semanage fcontext -a -t httpd_sys_content_t "/webdata(/.*)?"

sudo restorecon -Rv /webdata
```

---

## Verify

```bash
systemctl status httpd

curl http://localhost
```

or

```
http://localhost
```

---

## Project Output

Apache serves the custom webpage from the new document root.

---

## Skills Demonstrated

- Linux Administration
- Apache HTTP Server
- SELinux
- File Permissions
- Web Server Configuration
- System Services
- Linux Networking

---

## Author

Chaitanya Maskikar

RHCSA | CCNA | Linux Administrator | AWS | Cloud
