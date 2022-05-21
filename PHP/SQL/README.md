# SQL

## Table of Contents

- [General Knowledge](#general-knowledge)
  - [Relationships](#relationships)
    - [One-to-one](#one-to-one-relationships)
    - [One-to-many](#one-to-many-relationships)
    - [Many-to-many](#many-to-many-relationships)
  - [Queries](#queries)
  - [Creating a User](#creating-a-user-command-line)
  

## General Knowledge

### Relationships

#### One-to-one relationships

A one-to-one relationship refers to the relationship between two tables where there is a record in one table that is associated with exactly one record in another table. An example of this would be where one table's ID column is referenced in another table. This is known as "primary key as foreign key". 

You can either use the same primary key in both tables, or add a new column to one of the tables and make it a foreign key.

#### One-to-many relationships

#### Many-to-many relationships
You have to use a third table to represent the relationship, so you have the following three tables:

```sql 
websites (id, url)
category (id, category)
website_category (website_id, category_id)

website_id is foreign key to category_id 
category_id is foreign key to category_id

Company (id, name ...)
Category (id, name, ...)
Company_Category (company_id, category_id)


Where `company_id` is a foreign key to `Company.id` and `category_id` is a foreign key to `Category.id`.

Website can have more than one category.
Category can have more than one website.
```

## Queries

```sql

/* create view */
CREATE VIEW newtable AS SELECT name, email FROM Table_1 INNER JOIN Table_2 ON Table1.id = Table2.id

/* remove view */
DROP VIEW viewName


/* join views */
SELECT websites.id, websites.url, websites.description, websites.pending, categories.category FROM websites INNER JOIN categories ON websites.url = categories.url

```

## Creating a user (command line)
```sql
/* open MariaDB */
mysql -u root -p /* this will prompt for root password & open command line */

/* in the command line now */
SHOW DATABASES; /* shows all databases */

/* create user */
CREATE USER 'username'@localhost IDENTIFIED BY 'password1';

/* grant permissions */
GRANT ALL PRIVILEGES ON *.* TO 'username'@localhost;
```

## Accessing SQL via command line (MariaDB & Xampp)
```
sudo /opt/lampp/bin/mysql -u root -p

/* if it asks you to upgrade */
cd /opt/lampp/bin
sudo ./mysql_upgrade -u root -p

/* delete a database giving you trouble */
cd /opt/lampp/var/mysql
rm -rf database

/* back up a single database */
mysqldump -u root -p databaseName > databaseName.sql
```
