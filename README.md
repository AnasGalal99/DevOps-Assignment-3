## 1. Create system user (no login, no home directory)
sudo useradd -r -M -s /sbin/nologin webapp_user

## 2. Create a system group named webapp_support.
sudo groupadd -r webapp_support

## 3. Create a regular user named support1. Ensure this user is added to the webapp_support group as a secondary group.
sudo useradd -m -G webapp_support support1
sudo passwd support1
password: 123321
groups support1 ## to verify 

## 4. Create the following directory tree under /opt/webapp/
sudo mkdir -p /opt/webapp/{bin,config,logs} 

## 5. Change the ownership of the entire /opt/webapp/ directory and all its contents to be owned by the user webapp_user and the group webapp_support
sudo chown -R webapp_user:webapp_support /opt/webapp

## 6. Set directory permissions so that:
## owebapp_user has full read, write, and execute access to everything.
## oMembers of the webapp_support group can:
## ▪ Read and list contents of the config/ and logs/ directories.
## ▪ Read files inside config/ and logs/.
## ▪ Have no access (cannot list, read, or write) to the bin/ directory.
## All other users on the system (others) must have no access to any part of /opt/webapp/.

sudo chmod -R 700 /opt/webapp

sudo chmod 750 /opt/webapp/config

sudo chmod 750 /opt/webapp/logs
