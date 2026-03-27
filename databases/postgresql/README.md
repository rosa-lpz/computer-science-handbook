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


# Create a Database and Schema using a query
A database can be created by:
* Runnin a SQL script
* Create the database using the pgAdmin and adding flat files to database
* Restore the database using a file (example: DataWarehouseAnalytics.bak)

## Example 1
```sql
/*
=============================================================
Create Database and Schemas
=============================================================
Script Purpose:
    This script recreates the 'data_warehouse_analytics' database.
    In PostgreSQL, database names are typically lowercase.

WARNING:
    This will permanently delete all data in the database.
*/

-- Step 1: Drop and Recreate Database
-- Note: Run these two lines while connected to the 'postgres' or 'template1' database
DROP DATABASE IF EXISTS data_warehouse_analytics;
CREATE DATABASE data_warehouse_analytics;

-- Step 2: Connect to the new database
-- (In psql use: \c data_warehouse_analytics)

-- Step 3: Create Schemas
CREATE SCHEMA IF NOT EXISTS gold;

-- Step 4: Create Tables
CREATE TABLE gold.dim_customers (
    customer_key    INT,
    customer_id     INT,
    customer_number VARCHAR(50),
    first_name      VARCHAR(50),
    last_name       VARCHAR(50),
    country         VARCHAR(50),
    marital_status  VARCHAR(50),
    gender          VARCHAR(50),
    birthdate       DATE,
    create_date     DATE
);

CREATE TABLE gold.dim_products (
    product_key    INT,
    product_id     INT,
    product_number VARCHAR(50),
    product_name   VARCHAR(50),
    category_id    VARCHAR(50),
    category       VARCHAR(50),
    subcategory    VARCHAR(50),
    maintenance    VARCHAR(50),
    cost           INT,
    product_line   VARCHAR(50),
    start_date     DATE
);

CREATE TABLE gold.fact_sales (
    order_number   VARCHAR(50),
    product_key    INT,
    customer_key   INT,
    order_date     DATE,
    shipping_date  DATE,
    due_date       DATE,
    sales_amount   INT,
    quantity       SMALLINT, -- 'tinyint' is not a native PG type; SMALLINT is used
    price          INT
);

-- Step 5: Data Loading
-- Note: 'COPY' requires the database superuser or the 'pg_read_server_files' role.
-- Ensure the PostgreSQL service account has permission to read the file path.

TRUNCATE TABLE gold.dim_customers;
COPY gold.dim_customers
--FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_customers.csv'
FROM 'sql-sales/datasets/csv-files/gold.dim_customers.csv'
WITH (FORMAT CSV, HEADER MATCH, DELIMITER ',');

TRUNCATE TABLE gold.dim_products;
COPY gold.dim_products
--FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_products.csv'
FROM 'sql-sales/datasets/csv-files/gold.dim_products.csv'
WITH (FORMAT CSV, HEADER MATCH, DELIMITER ',');

TRUNCATE TABLE gold.fact_sales;
COPY gold.fact_sales
-- FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.fact_sales.csv'
FROM 'sql-sales/datasets/csv-files/gold.fact_sales.csv'
WITH (FORMAT CSV, HEADER MATCH, DELIMITER ',');


```


## References
* How to Install Postgres and Pgadmin on Ubuntu 24.04 LTS Linux: https://youtu.be/cD32EHVWRXY
* SQL Data Analyst Portfolio Project | Like I Do in My Real Projects: https://youtu.be/2jGhQpbzHes