# SQL

## Database Keys

**Foreign key:** A column or group of columns that provides a link between data in two tables.

## Many-to-many relationships
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

### Queries

```sql

/* create view */
CREATE VIEW newtable AS SELECT name, email FROM Table_1 INNER JOIN Table_2 ON Table1.id = Table2.id

/* remove view */
DROP VIEW viewName


/* join views */
SELECT websites.id, websites.url, websites.description, websites.pending, categories.category FROM websites INNER JOIN categories ON websites.url = categories.url

```

### Foreign Keys

The `FOREIGN KEY` restraint is used to prevent actions that would destroy links between tables. A `FOREIGN KEY` refers to the `PRIMARY KEY` of another table.


### Troubleshooting

#### Foreign Key Error Messages

```sql

> Cannot add or update a child row: a foreign key constraint fails.
/* This error occurs because you're trying to update a table that doesn't have a valid value for the selected foreign key.



```