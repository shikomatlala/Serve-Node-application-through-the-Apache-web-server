# Daemonize your application with Forever to keep it running
> The next step is to daemonize your application, so that it keeps running in the background.

### 1. Intall Forever
```sh
npm install forever -g
```

# Serve your application through the Apache web server
> 
> You can serve your application through the Apache web server by enabling a virtual host that connects to your application. To do that, follow the steps below.
> 

### 1. Create a custom Virtual Host
> Navigate the following directory
```sh
 cd /etc/httpd/conf.d
``` 

> Create a New File with the name **myapp-http-vhost.conf**

> Open the File and add the following information into that file

```
  <VirtualHost _default_:80>
    ServerAlias *
    DocumentRoot "/home/ec2-user/faultreportresidentbev4/"
    <Directory "/home/ec2-user/faultreportresidentbev4/">
      Require all granted
    </Directory>
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/
  </VirtualHost>
```
>
> Replace DocumentRoot path with the path of your app, in my case it the path as listed here.
>

> Create and Edit the https-vhost.conf file.
```
  <VirtualHost _default_:443>
    ServerAlias *
    SSLEngine on
    SSLCertificateFile "/opt/bitnami/apache/conf/bitnami/certs/server.crt"
    SSLCertificateKeyFile "/opt/bitnami/apache/conf/bitnami/certs/server.key"
    DocumentRoot "/home/ec2-user/faultreportresidentbev4/"
    <Directory "/home/ec2-user/faultreportresidentbev4/">
      Require all granted
    </Directory>
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/
  </VirtualHost>
```
---
### 3. Restart the Apache Server
```sh
sudo systemctl restart httpd
```
