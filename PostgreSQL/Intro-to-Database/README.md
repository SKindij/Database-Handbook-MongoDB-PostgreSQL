# Introduction to PostgreSQL

> PostgreSQL is a powerful, open source object-relational database system that uses and extends the SQL language combined with many features that safely store and scale the most complicated data workloads. The origins of PostgreSQL date back to 1986 as part of the POSTGRES project at the University of California at Berkeley and has more than 35 years of active development on the core platform.

### SQL - Structured Query Language
+ **DDL** (Data Definition Language)
  - CREATE, ALTER, DROP
+ **DML** (Data Manipulation Language)
  - SELECT, INSERT, UPDATE, DELETE
+ **TCL** (Transaction Control Language)
  - COMMIT, ROLLBACK, SAVEPOINT
+ **DCL** (Data Control Language)
  - GRANT, REVOKE, DENY


- - -

For learning PostgreSQL and SQL, it's recommended to set up a local development environment or use an online environment where you can directly interact with the database. 

Here are some alternatives:
+ **Local Development:**
  - Install [PostgreSQL](https://www.postgresql.org/) on your computer.
  - Use a SQL client such as [pgAdmin](https://www.pgadmin.org/) or 🦷 DBeaver to interact with the database.
+ **Online Database Services:**
  - Consider using online database services that provide a web-based interface for managing databases.
  - Examples include 🐘 ElephantSQL and 🌟 Aiven.
+ **Interactive Tutorials:**
  - Explore online platforms and tutorials that provide interactive SQL learning environments.
  - Websites like 🎓 SQLZoo and 📊 Mode Analytics offer hands-on SQL exercises.
+ **Cloud Platforms:**
  - Utilize cloud platforms like ☁️ AWS, ☁️ Google Cloud, or ☁️ Microsoft Azure to create PostgreSQL instances and manage databases through their web consoles.

- - -

## Some PostgreSQL Hosting

### 🐘 [ElephantSQL](https://www.elephantsql.com/) 🔧

#### Features
+ Shared and dedicated instances
+ Automated backups and continuous monitoring
+ 99.95% SLA uptime for dedicated plans

#### Plans & Pricing
_Shared high perfomance server_

* Tiny Turtle
  + free
  + 20 Mb data
  + 5 concurent connections
* Simple Spider
  + 5 $
  + 500 Mb data
  + 10 concurent connections
* Crazy Cat
  + 10 $
  + 1 000 Mb data
  + 15 concurent connections

### 🤖 [CleverCloud](https://www.clever-cloud.com/product/postgresql/) 🔧
_Deploy fully managed PostgreSQL databases with monitoring, backups and migration tools._

#### Plans & Pricing
* DEV
  + 0 $
  + RAM shared
  + Disk size 256 Mb
  + Connection 5
* XXS Small
  + 6 $
  + RAM 512 Mb
  + Disk size 1 000 Mb
  + Connection 45
* XXS Medium
  + 7 $
  + RAM 512 Mb
  + Disk size 2 000 Mb
  + Connection 45

### 🚀 [Scalingo](https://scalingo.com/databases/postgresql) 🔧

#### Plans & Pricing
* Sandbox
  + 0 $
  + RAM 128 Mb
  + Storage 256 Mb
  + Connection 10
* Srarter
  + 8 $
  + RAM 10 000 Mb
  + Storage 2000 Mb
  + Connection 30

### 🌊 [DigitalOcean](https://www.digitalocean.com/products/managed-databases-postgresql?utm_medium=affiliates&utm_source=impact&utm_campaign=1244749&utm_content=&irgwc=1&irclickid=Vs1XB3RXLxyPRK-U45VhKWK4UkHxqw1%3AeUnx040) 🔧
_Worry-free PostgreSQL hosting_

It offers a $500 free credit for utilizing their PostgreSQL database services. This substantial amount allows you to test your project extensively, and even use the services for free over an extended period.

* Starting at $15/month for single node clusters

### 🌐 [Kamatera](https://try.kamatera.com/1nvps/?tcampaign=36074_462945&brand=kamatera&bta=36074) 🔧

#### Server Configuration
* S1
  + 4 $
  + 1024 Mb per RAM
  + 20 GB SSD Storage
  + 5 Tb Internet Traffic
* S2
  + 6 $
  + 2048 Mb per RAM
  + 20 GB SSD Storage
  + 5 Tb Internet Traffic
* S2
  + 12 $
  + 2048 Mb per RAM
  + 30 GB SSD Storage
  + 5 Tb Internet Traffic

### 🏗️ [Heroku](https://www.heroku.com/postgres) 🔧

#### Plans & Pricing
* Mini
  + 5 $
  + 0 Bt RAM
  + 1 GB Storage
  + 20 connections
* Basic
  + 9 $
  + 0 Bt RAM
  + 10 GB Storage
  + 20 connections
