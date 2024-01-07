# PostgreSQL Fundamentals

&emsp;Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance constitutes a database cluster.
Each table is a named collection of rows. Each row of a given table has the same set of named columns, and each column is of a specific data type.

## 📊 Data Types 🛠️

### 🔘 Boolean ✔️
* column keyword: `boolean` | `bool`
  - value = `true`
    + insert data: `1`, `yes`, `y`, `t`, `true`
  - value = `false`
    + insert data: `0`, `no`, `false`, `f`
  - value = `null`
    + insert data: `space`

### 🅰️ Character 🔤

| Keyword      | B | Description            | Range                              |
|--------------|---|------------------------|------------------------------------|
| `CHAR(n)`    | v | fixed-length character | For shorter length DB pads spaces. |
| `VARCHAR(n)` | v | fixed-length string    | Without unnecessary spaces.        |
|  `TEXT`      | v | variable-length string | With unlimited length.             |

### 🔢 Numeric

| Keyword        | B | Description                | Range                                |
|----------------|---|----------------------------|--------------------------------------|
| `SMALLINT`     | 2 | small-range integer        | from -32,768 to 32,767               |
| `INTEGER`      | 4 | typical choice             | from -2,147,483,648 to 2,147,483,647 |
| `SMALLSERIAL`  | 2 | autoincrementing           | 1, 2, 3, 4, 5, n , ..., 32,767       |
| `SERIAL`       | 4 | auto generate and populate | 1, 2, 3, ..., n, 2,147,483,647       |
| `numeric(p,s)` | v | user-specified precision   | from -3.4 * 10n38 to +3.4 * 10n38    |
| `real`/`float4`| 4 | inexact number             | 6 decimal digits                     |
|`float`/`float8`| 8 | double precision           | 6 decimal digits                     |

### 🕰️ Temporal 📅

| Keyword              | B | Description                  | Range                      |
|----------------------|---|------------------------------|----------------------------|
| `DATE`/`CURRENT_DATE`| 4 | `yyyy-mm-dd` e.g. 2024-01-02 | from 4713 BC to 5874897 AD |
| `TIME`               | 8 | `HH:MI:SS`                   | from 00:00:00 to 24:00:00  |
| `TIMESTAMP`          | 8 | stores date & time           |                            |
| `INTERVAL`           | 16| period in years, months, days | hours, minutes, seconds   |
| `TIMESTAMPTZ`        | 8 | `SET timezone = 'America/New_York';` | 2023-08-22 22:10:25-07 |

### 🎚️ Array 📚
* column keyword: `character[]` | `integer[]`

### 🔑 UUID 🆔
_allows to store Universal Unique Identifiers defined by RFC 4122_\
_can be used to hide sensitive data exposed to the public such as values of id_

- - -

## 🗄️ Creating Database Tables 📊

&emsp;You can create a new table by specifying the table name, along with all column names and their types:

```sql
CREATE TABLE countries (
    country_id SMALLSERIAL PRIMARY KEY,
    country_name VARCHAR(20) NOT NULL UNIQUE,
    prefix_ean VARCHAR(7) NOT NULL
);

CREATE TABLE drink_categories (
  drink_id SMALLSERIAL PRIMARY KEY,
  drink_category VARCHAR(20) NOT NULL UNIQUE
);

CREATE TABLE retail_chains (
  retail_chain_id SMALLSERIAL PRIMARY KEY,
  retail_chain_name VARCHAR(20) NOT NULL UNIQUE
);

CREATE TABLE beverages_data (
  beverage_id SMALLSERIAL PRIMARY KEY,
  beverage_title VARCHAR(40) NOT NULL,
  category_id SMALLINT REFERENCES drink_categories(drink_id) NOT NULL,
  beverage_volume FLOAT NOT NULL,
  beverage_in_wish BOOLEAN NOT NULL,
  beverage_ratings SMALLINT NOT NULL,
  country_id SMALLINT REFERENCES countries(country_id) NOT NULL,
  beverage_description TEXT,
  beverage_image_url VARCHAR(120),
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

DROP TABLE countries, drink_categories, retail_chains, beverages_data, beverage_prices;
```

## Inserting Data

```sql
INSERT INTO countries (country_name, prefix_ean)
VALUES
    ('Argentina', '779'),
    ('Britain', '500-509'),
    ('Germany', '400-440'),
    ('Mexico', '750-751'),
    ('Spain', '841-843'),
    ('Ukraine', '482'),
    ('USA', '000-019');

INSERT INTO drink_categories (drink_category)
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

INSERT INTO beverages_data (beverage_id, beverage_title, category_id, beverage_volume, 
 beverage_in_wish, beverage_ratings, country_id, beverage_description, beverage_image_url)
VALUES (
 1001, 'Wild Turkey Rare Breed 0.7L', 2, 0.7, false, 5, 29,
 'Тони паленого коричневого цукру і ванілі, трохи цитрусових, сосни і дуба.',
 '/images/beverages/Wild-Turkey-Rare-Breed-07.webp'
),
(
 1002, 'Wild Turkey Longbranch 0.7L', 2, 0.7, false, 5, 29,
 'Смак з відтінками димних солодощів, червоних яблук і карамелі.',
 '/images/beverages/Wild-Turkey-Longbranch-07.webp'
),
(
 1003, 'Wild Turkey 101 0.7L', 2, 0.7, false, 5, 29,
 'Смак ванілі, меду, карамелі, тютюну і тростинного цукру. Аромат ванілі, дуба, апельсина.',
 '/images/beverages/Wild-Turkey-101-07.webp'
),
(
 1004, 'Wild Turkey 0.7L', 2, 0.7, true, 5, 29,
 'Аромат ірису, меду, карамелі і обпаленого дуба. Делікатний, солодкуватий, трохи маслянистий смак.',
 '/images/beverages/Wild-Turkey-07.webp'
),
(
 1005, 'Wild Turkey Rye 0.7L', 2, 0.7, false, 5, 29,
 'Аромат має ванільно-пряні, дубові, цитрусові акценти. У смаку грушеві тони в компанії карамелі.',
 '/images/beverages/Wild-Turkey-Rye-07.webp'
);


```

## Retrieving Data

### show all information from the table

```sql
SELECT * FROM countries
ORDER BY country_id ASC

SELECT * FROM drink_categories
ORDER BY drink_id ASC

SELECT * FROM beverages_data
ORDER BY beverage_id ASC 

```

#### find out certain information by a specific id
```sql
-- choose the data we need
SELECT bd.beverage_title, c.country_name, dc.drink_category
FROM beverages_data bd
-- combine beverages_data table with fields of other tables
JOIN countries c ON bd.country_id = c.country_id
JOIN drink_categories dc ON bd.category_id = dc.drink_id
-- Filter by specific beverage_id
WHERE bd.beverage_id = {id_of_beverage};
```

#### request for a specific drink category
```sql
-- choose the data we need
SELECT bd.beverage_title, bd.beverage_volume, bd.beverage_description
FROM beverages_data bd
-- combine beverages_data table with fields of other tables
JOIN drink_categories dc ON bd.category_id = dc.drink_id
-- Filtering by a specific drink category
WHERE dc.drink_category = '{your_drink_category}';

```

#### get unique countries from which drinks are presented

```sql
SELECT DISTINCT c.country_name
FROM beverages_data bd
JOIN countries c ON bd.country_id = c.country_id;
```


#### price request in retail chains by drink ID
```sql
SELECT rc.retail_chain_name, bp.price, bp.last_updated
FROM beverage_prices bp
JOIN retail_chains rc ON bp.retail_chain_id = rc.retail_chain_id
WHERE bp.beverage_id = {your_beverage_id};
```

#### complex query with multiple conditions
```sql
SELECT beverage_title as Nazva, rc.retail_chain_name as Store, bp.price as "Ціна", bd.beverage_volume as "Міра"
FROM beverages_data bd
JOIN beverage_prices bp ON bd.beverage_id = bp.beverage_id
JOIN retail_chains rc ON bp.retail_chain_id = rc.retail_chain_id
WHERE bd.beverage_title like 'Wild%' AND bp.price > 0 and bp.price < 900
ORDER BY bp.price ASC;
```

## Modifying Data








