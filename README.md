# sysadmin-recipes

## References

- [Initial setup Ubuntu server](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04)

## Add sudo user 

**Ad user**

`adduser <newuser>`

`usermod -aG sudo <newuser>`

OR Edit sudoers

`visudo`

Add the newly created user by inserting <username> ALL=(ALL:ALL) ALL

at the end of the user privilege section, as shown in the following example:

**User privilege specification**

root    ALL=(ALL:ALL) ALL

newuser ALL=(ALL:ALL) ALL

## Nginx

```bash
sudo apt update
sudo apt install nginx
systemctl status nginx
```

### References

- https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04


## Apache2

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apache2
sudo a2enmod rewrite
sudo systemctl restart apache2
sudo adduser <user> www-data
```

## MariaDB

```
sudo apt install mariadb-server
sudo mariadb-secure-installation
sudo systemctl start mariadb.service
sudo systemctl status mariadb
```

## PHP

```
sudo apt-get install -y php php-cli php-mysql php-mbstring php-bcmath php-zip php-gd php-curl php-xml php-intl php-fpm
ls /etc/php/8.3/
cd /etc/php/8.3/fpm/pool.d/
sudo nano www.conf
```

Review this lines:

```
user = www-data
group = www-data

listen = /run/php/php8.3-fpm.sock
```

Save and run

`sudo systemctl restart php8.3-fpm`

### PHP-FPM x Nginx

> Nginx server block

```bash
server {
        listen 80;
        listen [::]:80;

        server_name DOMAIN;

        root /var/www/PROJECT/public;

        index index.php;

        access_log /var/log/nginx/DOMAIN-access.log;
        error_log  /var/log/nginx/DOMAIN-error.log error;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location = /favicon.ico { access_log off; log_not_found off; }
        location = /robots.txt  { access_log off; log_not_found off; }

        error_page 404 /index.php;

        location ~ \.php$ {
                fastcgi_pass unix:/var/run/php/php8.4-fpm.sock;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
                include fastcgi_params;
        }

        location ~ /\.(?!well-known).* {
                deny all;
        }
}
```

```bash
systemctl reload nginx
```

#### References 

- https://www.digitalocean.com/community/tutorials/php-fpm-nginx

## ufw Firewall

```
sudo apt-get install ufw
sudo ufw app list
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 'Apache Full'
sudo ufw allow 'Nginx Full'
sudo ufw enable
sudo ufw status
```

## Node

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.<version>/install.sh | bash

# copy as 2 lines
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

nvm install node
```

Any trouble to find nvm command:

```
source ~/.bashrc

or

source ~/.nvm/nvm.sh
```


## Add ssh-key deploy to Github

```
ssh-keygen
```

Copy `.pub` to Github section of the project

## Composer

```
wget https://getcomposer.org/installer
sudo php installer --install-dir=/usr/local/bin --filename=composer
rm installer
```

## SSL - HTTPS - Certbot

```
sudo apt install certbot python3-certbot-apache

# check is running
sudo systemctl status certbot.timer

# check autorenew
sudo certbot renew --dry-run
```

### References

- https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04

## Laravel project

### Mariadb database and user

```
sudo mysql -u root

#or

sudo mysql -u root -p
```

```
CREATE DATABASE 'yourDB';
SHOW DATABASES;

CREATE USER 'user1'@localhost IDENTIFIED BY 'password1';
SELECT User FROM mysql.user;

GRANT ALL PRIVILEGES ON yourdb.* TO 'user1'@localhost;
FLUSH PRIVILEGES;
SHOW GRANTS FOR 'user1'@localhost;
```

### Laravel steps

- git clone
- composer install
- cp .env.example .env
- chown -R <user>:www-data .


