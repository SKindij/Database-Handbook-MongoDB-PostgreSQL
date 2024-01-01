# PostgreSQL Fundamentals

&emsp;Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance constitutes a database cluster.
Each table is a named collection of rows. Each row of a given table has the same set of named columns, and each column is of a specific data type.

## Data Types






## Creating Databases and Tables

&emsp;You can create a new table by specifying the table name, along with all column names and their types:

```sql
CREATE TABLE countries (
    country_id SERIAL PRIMARY KEY,
    country_name VARCHAR(20) NOT NULL,
    prefix_ean VARCHAR(7) NOT NULL
);

CREATE TABLE drink_categories (
  drink_id SERIAL PRIMARY KEY,
  drink_name VARCHAR(10) UNIQUE
);








```



## Inserting and Retrieving Data

```sql
INSERT INTO countries (country_name, prefix_ean)
VALUES
    ('Argentina', '779'),
    ('Armenia', '485'),
    ('Australia', '930'),
    ('Barbados', '500'),
    ('Belgium', '540'),
    ('Britain', '500-509'),
    ('Bulgaria', '380'),
    ('Cuba', '850'),
    ('CzechRepublic', '859'),
    ('Dominican', '000-019'),
    ('Finland', '640-649'),
    ('France', '300-379'),
    ('Georgia', '000-019'),
    ('Germany', '400-440'),
    ('Greece', '520'),
    ('Ireland', '539'),
    ('Italy', '800-839'),
    ('Jamaica', '600-601'),
    ('Mexico', '750-751'),
    ('Norway', '700-709'),
    ('Poland', '590'),
    ('Portugal', '560'),
    ('Scotland', '500'),
    ('Slovakia', '860'),
    ('SouthAfrica', '600-601'),
    ('Spain', '841-843'),
    ('Sweden', '730-739'),
    ('Ukraine', '482'),
    ('USA', '000-019');

INSERT INTO drink_categories (drink_name)
VALUES 
  ('absinthe'),
  ('bourbon'),
  ('brandy'),
  ('champagne'),
  ('cider'),
  ('gin'),
  ('horilka'),
  ('liqueur'),
  ('portwein'),
  ('rum'),
  ('tequila'),
  ('tincture'),
  ('whiskey'),
  ('wine');








```




## Modifying Data








