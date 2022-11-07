# Intermediate-SQL-Queries_Datacamp


## select

SQL, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.

You can think of a relational database as a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or record, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or field, of a table contains a single attribute for all rows in the table. For example, in a table representing employees, we might have a column containing first and last names for all employees.



COUNT(*) tells you how many rows are in a table. However, if you want to count the number of non-missing values in a particular column, you can call COUNT() on just that column.

SELECT COUNT(birthdate)
FROM people;


count the number of distinct values in a column.

SELECT COUNT(DISTINCT birthdate)
FROM people;


LIKE and NOT LIKE

In SQL, the LIKE operator can be used in a WHERE clause to search for a pattern in a column. To accomplish this, you use something called a wildcard as a placeholder for some other values. There are two wildcards you can use with LIKE:

The % wildcard will match zero, one, or many characters in text. For example, the following query matches companies like 'Data', 'DataC' 'DataCamp', 'DataMind', and so on:

```
SELECT name
FROM companies
WHERE name LIKE 'Data%';
```

The _ wildcard will match a single character. For example, the following query matches companies like 'DataCamp', 'DataComp', and so on:

```
SELECT name
FROM companies
WHERE name LIKE 'DataC_mp';
```

You can also use the NOT LIKE operator to find records that don't match the pattern you specify.

Get the names of all people whose names begin with 'B'. The pattern you need is 'B%'.


Get the names of people whose names have 'r' as the second letter. The pattern you need is '_r%'.

Get the names of people whose names don't start with A. The pattern you need is 'A%'.


By default ORDER BY will sort in ascending order

```
SELECT title
FROM films
ORDER BY release_year DESC;
```

gives you the titles of films sorted by release year, from newest to oldest.

```
SELECT sex, count(*)
FROM employees
GROUP BY sex;
```

Commonly, GROUP BY is used with aggregate functions like COUNT() or MAX(). Note that GROUP BY always goes after the FROM clause!

```
SELECT sex, count(*)
FROM employees
GROUP BY sex
ORDER BY count DESC;
```

In SQL, aggregate functions can't be used in WHERE clauses. For example, the following query is invalid:

```
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;
```

This means that if you want to filter based on the result of an aggregate function, you need another way! That's where the HAVING clause comes in. For example,

```
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```


shows only those years in which more than 10 films were released.

```
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
having AVG(budget) > 60000000
```



