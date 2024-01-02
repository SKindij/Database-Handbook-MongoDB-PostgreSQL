# PostgreSQL Fundamentals

&emsp;Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance constitutes a database cluster.
Each table is a named collection of rows. Each row of a given table has the same set of named columns, and each column is of a specific data type.

## Data Types

### Boolean
* column keyword: `boolean` | `bool`
  - value = `true`
    + insert data: `1`, `yes`, `y`, `t`, `true`
  - value = `false`
    + insert data: `0`, `no`, `false`, `f`
  - value = `null`
    + insert data: `space`

### Character
* column keyword: `CHAR(n)`
  - value = fixed-length character with space padded
    + _If string is shorter than length of column, DB pads spaces._
* column keyword: `VARCHAR(n)`
  - value = variable-length character string
* column keyword: `TEXT`
  - value = variable-length character string
    + _It is a character string with unlimited length._

### Numeric
* column keyword: `SMALLINT`
  - value = 2-byte signed integer
    + range: from -32,768 to 32,767
* column keyword: `INT`
  - value = 4-byte integer
    + range: from -2,147,483,648 to 2,147,483,647
* column keyword: `SERIAL`
  - value = automatically generate and populate
    + range: 1, 2, 3, 4, 5, ..., n
* column keyword: `float(n)`
  - value = precision n up to 8 bytes
    + range: from float(1) to float(24)
* column keyword: `real` | `float8`
  - value = precision 4-byte
    + range: floating-point number
* column keyword: `numeric` | `numeric(p,s)`
  - value = exact number | money
    + range: with p digits with s number after the decimal point

### 













- - -

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








