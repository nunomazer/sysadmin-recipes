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
 
