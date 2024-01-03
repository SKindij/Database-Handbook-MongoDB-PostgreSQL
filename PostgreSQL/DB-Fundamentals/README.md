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

### Temporal
* column keyword: `DATE` | `CURRENT_DATE`
  - value = `yyyy-mm-dd` e.g. 2024-01-02
    + range: from 4713 BC to 5874897 AD
* column keyword: `TIME`
  - value = `HH:MI:SS`
  - range: from 00:00:00 to 24:00:00
* column keyword: `TIMESTAMP`
  - value = 2023-08-22 19:10:25-07
* column keyword: `TIMESTAMPTZ`
  - `SET timezone = 'America/New_York';`
  - value = 2023-08-22 22:10:25-07
* column keyword: `INTERVAL`
  - value = period in years, months, days, hours, minutes, seconds

### Array
* column keyword: `character[]` | `integer[]`

### UUID
_allows to store Universal Unique Identifiers defined by RFC 4122_\
_can be used to hide sensitive data exposed to the public such as values of id_


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

CREATE TABLE retail_chains (
  retail_chain_id SERIAL PRIMARY KEY,
  retail_chain_name VARCHAR(10) UNIQUE
);

CREATE TABLE beverages_data (
  beverage_id SERIAL PRIMARY KEY,
  title VARCHAR(40) NOT NULL,
  category_id SMALLINT REFERENCES drink_categories(drink_id),
  volume DECIMAL(1, 1) NOT NULL,
  in_wish BOOLEAN NOT NULL,
  ratings SMALLINT NOT NULL,
  country_id SMALLINT REFERENCES countries(country_id),
  description TEXT,
  image_url VARCHAR(120),
  created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE beverage_prices (
  beverage_id SMALLINT REFERENCES beverages_data(beverage_id),
  retail_chain_id SMALLINT REFERENCES retail_chains(retail_chain_id),
  price numeric NOT NULL,
  last_updated DATE
);

```
#### A command to delete a table from a database
```sql
DROP TABLE table_name;
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

INSERT INTO retail_chains (retail_chain_name)
VALUES 
  ('Auchan'),
  ('Novus'),
  ('Silpo'),
  ('Rozetka');

INSERT INTO beverages_data (beverage_id, title, category_id, volume, in_wish, ratings, country_id, description, image_url)
VALUES (
 1001, 'Wild Turkey Rare Breed 0.7L', 2, 0.7, false, 5, 29,
 'Тони паленого коричневого цукру і ванілі, трохи цитрусових, сосни і дуба.',
 '/images/beverages/Wild-Turkey-Rare-Breed-07.webp'
);


```




## Modifying Data








