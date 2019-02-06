# T-SQL Basics Cheat Sheet

Lightning fast T-SQL refreshment cheat sheet.

## Select

```sql
-- Syntax
SELECT <column1, column2, column3...>
FROM <table_name>

-- Select everything
SELECT *
FROM dbo.Projects;

-- Select individual columns
SELECT id, name, created_dt
FROM dbo.Projects;

-- Select all distinct values
SELECT DISTINCT *
FROM dbo.Projects;
```

## Where

```sql
-- Syntax
SELECT <column1, column2, column3...>
FROM <table_name>
WHERE <condition>;

-- Filtering records.
SELECT id, name, created_dt
FROM dbo.Projects
WHERE name = 'Alpha';
```

## And, Or, Not

```sql
-- AND Syntax
SELECT <column1, column2, column3..>
FROM <table_name>
WHERE <condition1>
AND <condition2>;

-- Fulfilling multiple conditions
SELECT id, name, created_dt
FROM dbo.Projects
WHERE name = 'Alpha'
AND created_dt > '2019-01-01';
```

```sql
-- OR Syntax
SELECT <column1, column2, column3..>
FROM <table_name>
WHERE <condition1>
OR <condition2>;

-- Fulfilling either condition
SELECT id, name, created_dt
FROM dbo.Projects
WHERE name = 'Alpha'
OR name = 'Omega';
```

```sql
-- NOT Syntax
SELECT <column1, column2, column3..>
FROM <table_name>
WHERE NOT <condition>;

-- Doesn't fulfill condition
SELECT id, name, created_dt
FROM dbo.Projects
WHERE NOT name = 'Alpha';
```

## Insert

```sql
-- Syntax
INSERT INTO <table_name> <column1, column2, column3...>
VALUES <value1, value2, value3...>;

-- Insert into specific columns
INSERT INTO dbo.Projects (id, name, created_dt)
VALUES (1, 'Alpha', '2019-02-05');

-- Specify value for all columns
INSERT INTO dbo.Projects
VALUES (1, 'Alpha', '2019-02-05');
```

## Update

```sql
-- Syntax
UPDATE <table_name>
SET <column> = <value>
WHERE <condition>;

-- Update a project
UPDATE dbo.Projects
SET name = 'Omega'
WHERE id = 1;

-- Update all rows
UPDATE dbo.Projects
SET created_dt = '2019-01-01';
```

## Order By

```sql
-- Syntax
SELECT <column1, column2, column3...>
FROM <table_name>
ORDER BY <column> ASC|DESC;

-- Descending order
SELECT id, name, created_dt
FROM dbo.Projects
ORDER BY created_dt DESC;

-- Multiple Columns
SELECT id, name, created_dt
FROM dbo.Projects
ORDER BY created_dt DESC,
         name;
```

## Null Values

```sql
-- Syntax (Also works for Updates and Deletes)
SELECT <column1, column2, column3...>
FROM <table_name>
WHERE <column> IS [NOT] NULL;

-- All null values
SELECT name, created_dt
FROM dbo.Projects
WHERE created_dt IS NULL;

-- All not null values
SELECT name, created_dt
FROM dbo.Projects
WHERE name IS NOT NULL;
```

## Delete

```sql
-- Syntax
DELETE FROM <table_name> [WHERE <condition>];

-- Delete all records before 01-01-2019
DELETE FROM dbo.Projects 
WHERE created_dt < '01-01-2019';

-- Delete all records
DELETE FROM dbo.Projects;
```

## Top

```sql
-- Syntax
SELECT TOP <num> [PERCENT] <column1, column2, column3...>
FROM <table_name>;

-- Top 10 most recent projects.
SELECT TOP 10 name
FROM dbo.Projects
ORDER BY created_dt DESC;

-- Top 15% projects ordered alphabetically
SELECT TOP 15 PERCENT name
FROM dbo.Projects
ORDER BY name;
```

## Aggregates

### Min and Max

```sql
-- Syntax
SELECT MIN|MAX(column) AS <alias>
FROM <table_name>;

-- Latest created_dt
SELECT MAX(created_dt) AS latest_date
FROM dbo.Projects;

-- Earliest created_dt
SELECT MIN(created_dt) AS earliest_date
FROM dbo.Projects;
```

### Count, Avg and Sum

```sql
-- Syntax
SELECT COUNT|AVG|SUM(column) AS <alias>
FROM <table_name>;

-- Count number of projects created after 01-01-2019
SELECT COUNT(id) AS num_projects
FROM dbo.Projects
WHERE created_dt > '2019-01-01';

-- Avg number of personnel for all projects
SELECT AVG(personnel_count) AS average_personnel
FROM dbo.Projects;

-- Total number of personnel across all projects
SELECT SUM(personnel_count) AS total_personnel
FROM dbo.Projects;
```
