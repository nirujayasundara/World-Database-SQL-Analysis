
# World Database SQL Analysis

A collection of SQL queries analyzing global demographic data — countries, cities, and languages  using MySQL's classic `world` sample database. Built as a junior data analyst exercise simulating real requests from clients like travel agencies, real estate firms, health initiatives, and research institutes.

Each task below follows a **Business Question → SQL Approach → Key Finding → Recommendation** structure to mirror how analysis is communicated in a real workplace.
https://supabase.com/dashboard/project/ykmsbdjmgxixjgkprbuc/sql/e0b381d6-f879-493c-8eac-1b42762bbfed

<img width="1090" height="691" alt="Screenshot 2026-07-16 131554" src="https://github.com/user-attachments/assets/2c1ec438-2a74-4b27-97ee-c9be3b6c8552" />


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

---

## 1. Count of Cities in the USA

**Business Question:** How many cities are in the United States, to serve as a baseline for demographic analysis?

```sql
SELECT COUNT(*) AS total_us_cities
FROM city
WHERE CountryCode = 'USA';
```

**Key Finding:** `[fill in from your result]` cities recorded in the database for the USA.

**Recommendation:** Use this count as the denominator for any per-city or per-capita comparisons in later USA-focused analysis. If the number seems low relative to real-world city counts, flag that the `world` database only includes larger/notable cities, not every incorporated municipality.

---

## 2. Country with Highest Life Expectancy

**Business Question:** Which country has the highest life expectancy, to help prioritize healthcare resource allocation?

```sql
SELECT Name, LifeExpectancy
FROM country
ORDER BY LifeExpectancy DESC
LIMIT 1;
```

**Key Finding:** `[fill in from your result]` has the highest recorded life expectancy at `[X]` years.

**Recommendation:** Rather than treating this as a target for intervention, use it as a benchmark — compare other countries' life expectancy against this ceiling to identify the biggest gaps and prioritize healthcare funding toward countries furthest below it.

---

## 3. Cities with "New" in the Name

**Business Question:** Which cities worldwide have "New" in their name, for a New Year travel promotion?

```sql
SELECT Name, CountryCode, Population
FROM city
WHERE Name LIKE '%New%';
```

**Key Finding:** `[fill in — number of cities returned, and a few notable examples e.g. New York, New Delhi]`

**Recommendation:** Segment the results by population size before building promotional materials — lead marketing spend with the largest, most recognizable cities (e.g. New York, New Delhi) to maximize campaign reach, and use smaller "New ___" cities as niche/off-the-beaten-path content.

---

## 4. Top 10 Most Populous Cities

**Business Question:** What are the world's 10 most populous cities, for a concise population overview report?

```sql
SELECT Name, CountryCode, Population
FROM city
ORDER BY Population DESC
LIMIT 10;
```

**Key Finding:** `[fill in — list top 3–5 cities and populations]`

**Recommendation:** These top 10 cities represent the highest-density urban markets globally — prioritize them for any analysis requiring maximum population coverage with minimal data points (e.g. quick-turnaround executive summaries).

---

## 5. Cities with Population Larger Than 2,000,000

**Business Question:** Which cities exceed 2 million residents, for real estate investment research?

```sql
SELECT Name, CountryCode, Population
FROM city
WHERE Population > 2000000
ORDER BY Population DESC;
```

**Key Finding:** `[fill in — total count of cities matching, plus range]`

**Recommendation:** Treat this list as the initial investment shortlist, then layer in economic indicators (GNP, government stability) from the `country` table to rank cities by investment attractiveness rather than population alone — a large city isn't automatically a good investment target.

---

## 6. Cities Beginning with "Be"

**Business Question:** Which cities start with the prefix "Be," for a travel blog content series?

```sql
SELECT Name, CountryCode, Population
FROM city
WHERE Name LIKE 'Be%';
```

**Key Finding:** `[fill in — number of matches, notable examples e.g. Beijing, Belgrade, Beirut]`

**Recommendation:** Group results by continent/region before publishing so the blogger can build a geographically diverse series rather than clustering all articles around one region.

---

## 7. Cities with Population Between 500,000–1,000,000

**Business Question:** Which mid-sized cities (500K–1M population) are candidates for infrastructure development?

```sql
SELECT Name, CountryCode, Population
FROM city
WHERE Population BETWEEN 500000 AND 1000000
ORDER BY Population DESC;
```

**Key Finding:** `[fill in — count of cities in this band]`

**Recommendation:** Mid-sized cities are often under-invested relative to megacities but have more room to scale efficiently — recommend the planning committee prioritize the higher end of this range (closer to 1M) first, since they're closer to needing capacity upgrades.

---

## 8. Cities Sorted Alphabetically

**Business Question:** Provide an alphabetically sorted list of city names to support a geography lesson.

```sql
SELECT Name, CountryCode, Population
FROM city
ORDER BY Name ASC;
```

**Key Finding:** Full alphabetical listing generated — `[fill in — total row count]` cities.

**Recommendation:** For classroom use, consider pairing this with the City Name Frequency Analysis (Task 10) so students can also discuss *why* certain names repeat globally (colonial naming patterns, common geographic terms, etc.).

---

## 9. Most Populated City in the World

**Business Question:** Which single city has the highest population, to guide top-tier investment strategy?

```sql
SELECT Name, CountryCode, Population
FROM city
ORDER BY Population DESC
LIMIT 1;
```

**Key Finding:** `[fill in from your result]`, population `[X]`.

**Recommendation:** Use this city as the anchor case study for the investment firm's strategic planning, but pair it with growth-rate data (not available in this table) before committing capital — the largest city today isn't necessarily the fastest-growing.

---

## 10. City Name Frequency Analysis

**Business Question:** How often does each city name recur globally, to support a geography lesson on naming patterns?

```sql
SELECT Name, COUNT(*) AS occurrence_count
FROM city
GROUP BY Name
ORDER BY Name ASC;
```

**Key Finding:** `[fill in — most frequently repeated name(s) and count]`

**Recommendation:** Highlight the most-repeated names as discussion points for the class — they often reveal colonial history, migration patterns, or shared linguistic roots (e.g. multiple cities named "San Jose" or "Springfield").

---

## 11. City with the Lowest Population

**Business Question:** Which city has the smallest recorded population, for a census bureau's demographic overview?

```sql
SELECT Name, CountryCode, Population
FROM city
WHERE Population > 0
ORDER BY Population ASC
LIMIT 1;
```

**Key Finding:** `[fill in from your result]`

**Recommendation:** Note in the census report that this figure excludes cities with zero/missing population data — flag those as a data quality gap rather than implying they have no residents, so the bureau doesn't misinterpret incomplete records as real demographic findings.

---

## 12. Country with Largest Population

**Business Question:** Which country has the highest total population, for a global economic research analysis?

```sql
SELECT Name, Population
FROM country
ORDER BY Population DESC
LIMIT 1;
```

**Key Finding:** `[fill in from your result]`

**Recommendation:** Recommend the research institute cross-reference this with GNP and GNP-per-capita (also in the `country` table) — population size alone doesn't indicate economic strength, and combining the two paints a more accurate picture of market potential.

---

## 13. Capital of Spain

**Business Question:** What is the capital of Spain, to ensure travel itinerary accuracy?

```sql
SELECT ci.Name AS Capital
FROM country co
JOIN city ci ON co.Capital = ci.ID
WHERE co.Name = 'Spain';
```

**Key Finding:** Madrid.

**Recommendation:** This join pattern (`country.Capital` → `city.ID`) should be reused as a template for verifying any capital city in the itinerary — build it into a reusable query or view so the travel agency can quickly validate destinations for other countries without rewriting the join each time.

---

## 14. Cities in Europe

**Business Question:** Which cities are located in Europe, to support a cultural exchange program?

```sql
SELECT ci.Name AS CityName, co.Name AS CountryName, ci.Population
FROM city ci
JOIN country co ON ci.CountryCode = co.Code
WHERE co.Continent = 'Europe'
ORDER BY ci.Population DESC;
```

**Key Finding:** `[fill in — total count of European cities returned]`

**Recommendation:** Prioritize mid-to-large cities with universities or established international programs (not directly in this table, but worth cross-referencing) over the largest capitals alone — this spreads student placements more evenly and reduces oversubscription to a handful of major hubs.

---

## 15. Average Population by Country

**Business Question:** What is the average city population within each country, for comparative demographic analysis?

```sql
SELECT co.Name AS CountryName, AVG(ci.Population) AS AvgCityPopulation
FROM city ci
JOIN country co ON ci.CountryCode = co.Code
GROUP BY co.Name
ORDER BY AvgCityPopulation DESC;
```

**Key Finding:** `[fill in — countries with highest/lowest averages]`

**Recommendation:** Caution the research team that countries with only one or two cities listed will show skewed averages (a single large capital inflates the "average"). Recommend filtering to countries with a minimum number of cities (e.g. `HAVING COUNT(*) >= 5`) before drawing conclusions about national urban trends.

---

## 16. Capital Cities Population Comparison

**Business Question:** How do capital city populations compare across countries, for a global urban demographics study?

```sql
SELECT co.Name AS CountryName, ci.Name AS CapitalCity, ci.Population
FROM country co
JOIN city ci ON co.Capital = ci.ID
ORDER BY ci.Population DESC;
```

**Key Finding:** `[fill in — largest and smallest capital cities by population]`

**Recommendation:** Segment findings by continent or income level (via GNP) rather than presenting a single global ranking — capital city size is influenced heavily by whether a country is centralized (one dominant capital) or decentralized (population spread across multiple major cities), and a flat ranking can mislead readers about a country's overall urbanization.

---

## 17. Countries with Low Population Density

**Business Question:** Which countries have low population density, for agricultural development research?

```sql
SELECT Name,
       Population,
       SurfaceArea,
       ROUND(Population / SurfaceArea, 4) AS PopulationDensity
FROM country
WHERE SurfaceArea > 0
ORDER BY PopulationDensity ASC
LIMIT 20;
```

**Key Finding:** `[fill in — lowest-density countries and their density values]`

**Recommendation:** Before recommending agricultural investment, cross-check candidate countries against climate/arable land data (not present in this database) — low population density alone doesn't mean land is farmable; some of the lowest-density countries are deserts, tundra, or otherwise unsuitable for agriculture.

---

## 18. Cities Ranked 31st–40th by Population

**Business Question:** Which cities rank 31st–40th globally by population, for a market research firm looking beyond top-tier cities?

```sql
SELECT Name, CountryCode, Population
FROM city
ORDER BY Population DESC
LIMIT 10 OFFSET 30;
```

**Key Finding:** `[fill in — cities and populations in this band]`

**Recommendation:** These "second-tier" global cities often have lower market saturation and entry costs than the top 30 — recommend the firm evaluate this tier specifically for expansion opportunities where competition is lower but population scale is still substantial.

---

## Key Learnings

- Writing `JOIN`s to combine city-level and country-level data (e.g. resolving country codes into full names, capital city lookups)
- Using `GROUP BY` with aggregate functions to summarize data per country
- Applying `LIMIT`/`OFFSET` for pagination-style queries
- Handling edge cases in real data, like filtering out zero-population records before finding a minimum
- Translating raw query output into business-relevant recommendations, not just numbers

## Overall Recommendations

- **Data quality first:** Several tasks (e.g. #11, #15) surfaced records with missing or zero population values — any downstream analysis should account for this rather than treating gaps as true zeros.
- **Pair population with context:** Population alone (city size, country size) is rarely sufficient for business decisions — GNP, life expectancy, and continent/region data should be combined with population metrics for more actionable insights.
- **Reusable query patterns:** The capital-city join (Task 13) and continent-filtered join (Task 14) are patterns worth saving as reusable views if this analysis is extended to more countries or repeated regularly.

---

*Part of a data analytics coursework project focused on SQL fundamentals using the world database.*
