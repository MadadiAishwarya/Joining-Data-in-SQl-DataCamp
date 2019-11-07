Subquery inside where:
-- Select average life_expectancy
select avg(life_expectancy)
  -- From populations
  from populations
-- Where year is 2015
where year=2015

-- Select fields
select *
  -- From populations
  from populations
-- Where life_expectancy is greater than
where life_expectancy >
  -- 1.15 * subquery
 1.15* (select avg(life_expectancy)  
   from populations
   where year=2015 )
     and year =2015;
     
     
Subquery inside where (2):
-- 2. Select fields
select name, country_code, urbanarea_pop
  -- 3. From cities
  from cities
-- 4. Where city name in the field of capital cities
where name IN
  -- 1. Subquery
  (select capital
   from countries)
ORDER BY urbanarea_pop DESC;


Subquery inside select
SELECT countries.name AS country, COUNT(*) AS cities_num
  FROM cities
    INNER JOIN countries
    ON countries.code = cities.country_code
GROUP BY country
ORDER BY cities_num DESC, country
LIMIT 9;

/* 
SELECT ___ AS ___,
  (SELECT ___
   FROM ___
   WHERE countries.code = cities.country_code) AS cities_num
FROM ___
ORDER BY ___ ___, ___
LIMIT 9;
*/

/* SELECT countries.name AS country, COUNT(*) AS cities_num
  FROM cities
    INNER JOIN countries
    ON countries.code = cities.country_code
GROUP BY country
ORDER BY cities_num DESC, country
LIMIT 9;
*/

SELECT countries.name AS country,
  (SELECT count(*)
   FROM cities
   WHERE countries.code = cities.country_code) AS cities_num
FROM countries
ORDER BY cities_num desc, country
LIMIT 9;


Subquery inside from:
-- Select fields (with aliases)
select code,count(*) as lang_num
  -- From languages
  from languages
-- Group by code
group by code;

SELECT local_name, subquery.lang_num
  FROM countries,
  	(SELECT code, COUNT(*) AS lang_num
  	 FROM languages
  	 GROUP BY code) AS subquery
  WHERE countries.code = subquery.code
ORDER BY lang_num DESC;


Advanced subquery:
-- Select fields
select name,continent,inflation_rate
  -- From countries
 from countries
  	-- Join to economies
  	inner join economies
    -- Match on code
    on countries.code=economies.code
-- Where year is 2015
where year=2015;

-- Select fields
select max(inflation_rate)as max_inf
  -- Subquery using FROM (alias as subquery)
  FROM (
      select name,continent,inflation_rate
      from countries
      inner join economies
      using(code)
      where year=2015) AS subquery
-- Group by continent
group by continent;

-- Select fields
SELECT name, continent, inflation_rate
  -- From countries
  FROM countries
	-- Join to economies
	INNER JOIN economies
	-- Match on code
	ON countries.code = economies.code
  -- Where year is 2015
  WHERE year = 2015
    -- And inflation rate in subquery (alias as subquery)
    AND inflation_rate IN (
        SELECT MAX(inflation_rate) AS max_inf
        FROM (
             SELECT name, continent, inflation_rate
             FROM countries
             INNER JOIN economies
             ON countries.code = economies.code
             WHERE year = 2015) AS subquery
        GROUP BY continent);
        
 
Subquery challenge:
-- Select fields
SELECT code,inflation_rate, unemployment_rate
  -- From economies
  FROM economies
  -- Where year is 2015 and code is not in
  WHERE year = 2015 AND code not in
  	-- Subquery
  	(SELECT code
  	 FROM countries
  	 WHERE (gov_form = 'Constitutional Monarchy' OR gov_form LIKE '%Republic'))
-- Order by inflation rate
ORDER BY inflation_rate;


Subquery review:WHERE


Final challenge:
-- Select fields
SELECT DISTINCT name, total_investment, imports
  -- From table (with alias)
  FROM countries AS c
    -- Join with table (with alias)
    LEFT JOIN economies AS e
      -- Match on code
      ON (c.code = e.code
      -- and code in Subquery
        AND c.code IN (
          SELECT l.code
          FROM languages AS l
          WHERE official = 'true'
        ) )
  -- Where region and year are correct
  WHERE region = 'Central America' AND year = 2015
-- Order by field
ORDER BY name;


Final challenge (2):
-- Select fields
SELECT region,continent, avg(fertility_rate) AS avg_fert_rate
  -- From left table
  FROM countries AS c
    -- Join to right table
    INNER JOIN populations AS p
      -- Match on join condition
      ON c.code = p.country_code
  -- Where specific records matching some condition
  WHERE year = 2015
-- Group appropriately
GROUP BY region, continent
-- Order appropriately
ORDER BY avg_fert_rate;


Final challenge (3):
-- Select fields
SELECT name,country_code, city_proper_pop, metroarea_pop,  
      -- Calculate city_perc
      city_proper_pop / metroarea_pop * 100 AS city_perc
  -- From appropriate table
  FROM cities
  -- Where 
  WHERE name IN
    -- Subquery
    (SELECT capital
     FROM countries
     WHERE (continent = 'Europe'
        OR region LIKE '%America'))
       AND metroarea_pop IS not null
-- Order appropriately
ORDER BY city_perc desc
-- Limit amount
Limit 10;
