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
```

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
 
