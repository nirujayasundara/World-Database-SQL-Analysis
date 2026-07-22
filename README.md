# World-Database-SQL-Analysis
World Database SQL Analysis
# World Database SQL Analysis

A collection of SQL queries analyzing global demographic data — countries, cities, and languages using MySQL's classic `world` sample database. Built as a junior data analyst exercise simulating realworld requests from clients like travel agencies, real estate firms, health initiatives, and research institutes.

## Overview

Each query answers a specific business or research scenario, from simple lookups (e.g. "what's the capital of Spain?") to aggregate analysis (e.g. average city population by country, population density rankings). The goal was to practice translating plain-language business questions into precise SQL.

## Database

This project uses the **`world`** database, a standard MySQL sample dataset with three core tables:

| Table | Description |
|---|---|
| `country` | Country-level data: name, continent, population, life expectancy, GNP, capital, etc. |
| `city` | City-level data: name, country code, district, population |
| `countrylanguage` | Languages spoken per country, with official status and percentage of speakers |

## Tools

- **MySQL Workbench** — writing and executing queries, viewing results
- **SQL** — `SELECT`, `WHERE`, `JOIN`, `GROUP BY`, `ORDER BY`, `LIMIT/OFFSET`, aggregate functions (`COUNT`, `AVG`)

## Queries Included

1. Count of cities in the USA
2. Country with the highest life expectancy
3. Cities with "New" in their name
4. Top 10 most populous cities
5. Cities with population > 2,000,000
6. Cities starting with "Be"
7. Cities with population between 500,000–1,000,000
8. Cities sorted alphabetically
9. Most populated city in the world
10. City name frequency analysis
11. City with the lowest population
12. Country with the largest population
13. Capital of Spain
14. All cities in Europe
15. Average city population by country
16. Capital cities population comparison
17. Countries with low population density
18. Cities ranked 31st–40th by population

Full query text and explanations are in https://supabase.com/dashboard/project/ykmsbdjmgxixjgkprbuc/sql/e0b381d6-f879-493c-8eac-1b42762bbfed.

## Sample Query

```sql
-- Average population of cities within each country
SELECT co.Name AS CountryName, AVG(ci.Population) AS AvgCityPopulation
FROM city ci
JOIN country co ON ci.CountryCode = co.Code
GROUP BY co.Name
ORDER BY AvgCityPopulation DESC;
```

## Key Learnings

- Writing `JOIN`s to combine city-level and country-level data (e.g. resolving country codes into full names, capital city lookups)
- Using `GROUP BY` with aggregate functions to summarize data per country
- Applying `LIMIT`/`OFFSET` for pagination-style queries
- Handling edge cases in real data, like filtering out zero-population records before finding a minimum

## Notes

Some queries required judgment calls not fully specified by the original scenario (e.g. defining a threshold for "low population density"). These decisions are documented inline in the query file.

---

*Part of a data analytics coursework project focused on SQL fundamentals using the world database.*
