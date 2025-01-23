# sysadmin-recipes

## Add sudo user 

**Ad user**

`adduser newuser`

**Edit sudoers**

`visudo`

Add the newly created user by inserting <username> ALL=(ALL:ALL) ALL

at the end of the user privilege section, as shown in the following example:

**User privilege specification**

root    ALL=(ALL:ALL) ALL

newuser ALL=(ALL:ALL) ALL

## Apache2

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apache2
sudo a2enmod rewrite
sudo systemctl restart apache2
```
## MariaDB

```
sudo apt install mariadb-server
sudo mysql_secure_installation
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

## ufw Firewall

```
sudo apt-get install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw allow 'Apache'
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```

## Add ssh-key deploy to Github

```
ssh-keygen
```

Copy `.pub` to Github section of the project

- Gt clone the project

## Composer

```
wget https://getcomposer.org/installer
sudo php installer --install-dir=/usr/local/bin --filename=composer
rm installer
```

