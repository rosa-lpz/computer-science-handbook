# PostgreSQL

## Installation
* https://www.postgresql.org/download/linux/debian/

PostgreSQL is available in all Debian versions by default. However, Debian "snapshots" a specific version of PostgreSQL that is then supported throughout the lifetime of that Debian version. The PostgreSQL project maintains an Apt repository with all supported of PostgreSQL available.
 
### Included in Distribution

Debian includes PostgreSQL by default. To install PostgreSQL on Debian, use the apt (or other apt-driving) command:
```bash
apt install postgresql
```
### PostgreSQL Apt Repository

If the version included in your version of Debian is not the one you want, you can use the PostgreSQL Apt Repository. This repository will integrate with your normal systems and patch management, and provide automatic updates for all supported versions of PostgreSQL throughout the support lifetime of PostgreSQL.

The PostgreSQL Apt repository supports the current versions of Debian:

    trixie (13.x)
    bookworm (12.x)
    bullseye (11.x)
    forky (testing)
    sid (unstable)

on the following architectures:

    amd64
    arm64
    ppc64el

Automated repository configuration: 
```bash
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```
To manually configure the Apt repository, follow these steps: 
```bash
# Import the repository signing key:
sudo apt install curl ca-certificates
sudo install -d /usr/share/postgresql-common/pgdg
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc

# Create the repository configuration file:
. /etc/os-release
sudo sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list"

# Update the package lists:
sudo apt update
```

Install PostgreSQL: (replace "18" by the version you want) 
```bash
sudo apt install postgresql-18
```

## PostgreSQL pgAdmin
* https://www.pgadmin.org/download/pgadmin-4-apt/
* 
```bash
# Setup the repository
#

# Install the public key for the repository (if not done previously):
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only: 
sudo apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

### Change password
Execute
```bash
sudo -u postgres psql
```
output
```bash
postgres=#
```
Then type:
```bash
postgres=# alter user postgres with password 'add_password'
ALTER ROLE
postgres=# quit
```

### References
* How to Install Postgres and Pgadmin on Ubuntu 24.04 LTS Linux:https://youtu.be/cD32EHVWRXY