# INVERSE PROXY PRACTICE

The aim of this practice is see how inverse proxy works, using different virtual machines

# TECHNOLOGIES

- Nginx
- Docker / Vagrant

# SET UP VIRTUAL MACHINES

## Inverse Proxy

The default file server block of nginx was modified to listen at 80 port,and proxy pass access was added to link it to the virtual machine used as server:

```
server {
    listen 80;
    listen [::]:80;

    server_name example.test www.example.test;

    location / {
        proxy_pass http://192.168.57.11:8080;
    }
}
```

The hosts file must be modified to access to the web server VM, adding:

```
192.168.57.11 w1
```

The host file hosts must be modified to add the VM proxy IP and domain.

## Server w1

Default file of nginx was modified to listen at 8080 port. This way it is assured that host only access to the inverse proxy. A index.html file is added to test the access.

```
server {
    listen 8080;
    listen [::]:8080;

    server_name w1;
    root /var/www/html;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
